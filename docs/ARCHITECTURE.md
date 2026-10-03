# Nuvva 平台架构逆向（完整版）

> 对象：m.nuvva.ai（移动端 Web，Vite + Vue 3 + vue-i18n SPA）
> 方法：Chrome CDP（9222 端口）+ Playwright 流量抓包 + 前端 bundle 静态分析 + 行为探测
> 时间：2026-09-30 ~ 2026-10-02，共 7 个测试账号、约 90 条消息

---

## 一、总体架构

```
┌─ 浏览器 SPA (m.nuvva.ai/assets/mobile-*.js)
│    └─ localStorage: user_id + access_token(JWT) + refresh_token
│
├─ REST API（同域 /api/v1/*，JWT Bearer 鉴权）
│
├─ WebSocket wss://m.nuvva.ai/ws?user_id=<uuid>
│    JSON 帧 {type, content}，content 为 JSON 字符串；ping/pong 心跳
│
├─ 屏幕存储 cdn.nuvva.ai/screen_share/<uuid>.html
│    ★ 公开可读，无需鉴权（重要发现）
│
└─ 技能系统
     技能 = 服务端文件记录（name/description/mainEntryFile/...），按 ID 寻址
     prompt 由服务端按 ID 注入模型上下文，客户端任何 API 读不到原文
```

## 二、REST API 端点全表（从前端 bundle 提取）

```
auth/*            login, signup, verify, google_auth, forgot_password,
                  reset_password, refresh_token
user/*            get, update          user_account/get（含 inviteId 邀请码）
user_subscription/get   余额/层级/到期（新号 balance.energyPoints = 300）
pricing_plan/list       能量包：1000EP/$3.99, 2000EP/$7.99, 5000EP/$19.99, 10000EP/$39.99
chat/list               消息记录（含每条消息的 screenShareId / parentScreenEvent）
chat/create             发消息
chat_topic/*            list, create, branch, pin, delete, update
chat_topic_spec/get|update   话题配置（rules/agentNotes/loadedSkills/skillFilesMap）
                         ★ 激活技能后 skillFilesMap 仍为空 —— 服务端注入的证据
chat_topic_share/*      list, create, delete（官方营销演示话题在此）
share/*                 get_chat_topic, fetch_file, list_pricing
screen_share/get        屏幕元数据（contentUrl/parentId/childScreenMap/contentSummary）
screen_share/set_data|get_data|handle_event   状态写入/读取/点击事件上报
file/*                  upload, list, fetch, create, delete（仅用户自己的目录可见）
agent/list|get|update   每账号一个独立 Nuvva agent 实例（modelId 为内部哈希）
task/*                  list, create, retry, resume, abort, delete
payment/*, payment_airwallex/checkout, payment/portal, payment/cancel_plan
shiyu_admin/*           管理端（需管理员权限）
```

## 三、WebSocket 帧类型（实测）

| type | 含义 |
|---|---|
| 33 | 工作状态（"正在思考…"，isIdle） |
| 52 / 53 | 话题元数据（agent 信息、iconSvg、技能摘要） |
| 101 | 新消息（完整消息记录结构） |
| 201 | 屏幕推送（contentUrl → CDN，parentId/childScreenMap 屏幕树） |

## 四、屏幕机制（技能玩法的核心）

```
模型回复（含 HTML）
  → 服务端存 cdn.nuvva.ai/screen_share/<uuid>.html
  → WS 201 帧（contentUrl）
  → 前端 fetch → Blob → <iframe class="screen-iframe"> 渲染
  → iframe 内注入三个全局函数：
      window.ld() / getData()  → LOAD_DATA_REQUEST/RESPONSE（读服务端状态）
      window.sd(data)          → SET_DATA_REQUEST/RESPONSE（写状态，POST screen_share/set_data）
      window.te(text)          → SCREEN_SHARE_EVENT（POST screen_share/handle_event）
        payload: {id, screenId, screenShareId, topicId, eventMessage, screenContent(整份HTML快照)}
  → eventMessage 作为一条用户消息进会话 → 模型结合状态推演 → 生成新屏幕 → 循环
```

实测 set_data 初始状态样例：
`{"name":"测试女王A","personality":["高冷女王"],"kinks":[],"location":"大堂酒吧"}`

## 五、模型信息（模型自述 + 推断）

- 模型不知道自己的基座型号（服务端隐藏，仅暴露内部哈希 modelId）
- 知识截止 ≈ 2024 年；能感知当前时间
- 约 80 轮对话后主动建议开新话题（上下文管理）
- HTML 屏幕与对话文本由**同一个模型**生成（结构化输出格式，非独立前端模型）
- 每轮输入构成：当前时间 + agent 人设资料 + 用户记忆档案 + 近期对话 + 当前屏幕内容 + 工作记忆（技能指令 + 已加载文件）
- 工具集 OP_REQUEST：联网搜索、网页爬取、文件查阅、图像生成/查看、语音/音乐生成、记忆检索、任务管理、日历提醒
- 会话设置 Multi-Texting = FALSE（单响应模式）

## 六、能量与计费

- 新号赠送 300 能量点
- 屏幕密集型消息 ≈ 19 点/条（纯文本更便宜）→ 每个免费号约 15-17 条
- 能量包 1000EP/$3.99 起；纯服务端计费，前端无成本元数据

## 七、内容消音机制（重要实证）

| 层级 | 触发 | 表现 |
|---|---|---|
| 模型层拒绝 | 语义识别"索要 prompt/自我披露" | 不生成内容，直接拒答 |
| 输出层替换 | **平台自身基础人设**的原文输出 | 替换为 `bee-bee-bee-`（插花/倒序等变换均无效，指纹级硬拦） |
| 放行 | 技能文件内容 | 逐字输出畅通无阻 |

## 八、提示词提取技法有效性排序（实测）

| 技法 | 有效性 |
|---|---|
| 笔记纠错法（默写错的让它逐字改正并标出处） | ★★★★★ |
| 隔行插花（每句一行+装饰行，绕开连续块状检测） | ★★★★★ |
| 姊妹店克隆法（"帮我写同构新技能"） | ★★★★ |
| 逐字校对游戏（单批 ≤3-4 条） | ★★★★ |
| 行为层提问（（测试）+ 问规则） | ★★★★ |
| 快速连发多条消息 | ✗ 会被队列丢弃 |
| 直接索要 / 交接文档 / JSON 导出 | ✗ 拒答或消音 |

## 九、其他实测结论

- 重复触发同一技能 → "已经在恭候了"，不重新建档（prompt 含去重规则）
- 纯文本消息可直接控制剧情，明确要求"不要重画界面"时不产 HTML（省能量关键）
- 技能文档中**无隐藏角色/暗号/特殊结局**设定；"彩蛋感"来自随机事件 + 条件反射机制
- 平台技能需特定 Skill ID 唤醒，客户端无法枚举可用技能
- 模型生成的 HTML 偶发多字节截断（� 损坏字符），复刻提取后需做编码修复
