《绯红会所》女DOM_美化协议


## 目录

01 整体风格规范 ｜ 02 开机动画 ｜ 03 封面页 ｜ 04 角色创建界面 ｜ 05 主剧情界面 ｜ 06 女王档案界面 ｜ 07 客人档案界面 ｜ 08 道具库界面 ｜ 09 会所地图界面 ｜ 10 委托任务面板 ｜ 11 调教室特殊UI效果 ｜ 12 弹窗与消息提示 ｜ 13 通用文字动效集 ｜ 14 快捷菜单（≡） ｜ 15 响应式适配 ｜ 16 运行说明与HTML结构参考 ｜ 17 色彩与字体速查表



## 第一部分：整体风格规范

视觉基调与开场动效
第一部分：整体风格规范
视觉基调
• 主背景色： 暖棕酒红 #2a1a1a —— 比纯黑暖得多，暖光映照下的丝绒质感，暧昧不压抑
• 面板底色： 深玫瑰棕 #3d2424 —— 卡片/弹窗背景，温暖有层次
• 一级底色： 酒红棕 #5a2e2e —— 次级面板，hover 态
• 主色/金： 玫瑰金 #d4a373 —— 标题、按钮、重要数据，奢华不刺眼
• 亮金： 暖金 #e8c99b —— 高亮态、发光
• 激情色： 酒红 #8b3a3a —— 情色场景、调教标记、危险感
• 亮红： 玫瑰红 #b84a4a —— 高潮强调、心跳动效
• 辅助色： 丝绒紫 #6b3a4b —— 点缀、次级状态
• 正文色： 暖米白 #f0e6d8 —— 主要阅读文字，温暖柔和
• 次文色： 米灰金 #b8a88a —— 次要说明、标签、时间
• 发光效果： 玫瑰金按钮使用 box-shadow: 0 0 15px rgba(212, 163, 115, 0.35) 暖光晕染
• 卡片透明度： rgba(61, 36, 36, 0.9) + backdrop-filter: blur(10px) 玻璃丝绒感
字体规范
• 标题字体： 'Playfair Display', 'Noto Serif SC', serif —— 优雅奢华，衬线体有会所感
• 正文字体： 'Noto Serif SC', 'Songti SC', serif —— 中文阅读舒适
• 点缀字体： 'Dancing Script', cursive —— 仅用于品牌名/特殊装饰字，手写体增添暧昧感
• 数字/代码字体： 'Cormorant Garamond', serif —— 优雅衬线数字
动效原则
• 所有过渡使用 transition: all 0.35s cubic-bezier(0.25, 0.46, 0.45, 0.94) —— 优雅缓慢有余韵
• 入场动效用 fadeIn、slideUp 类，时长 0.5-0.8s，丝滑不突兀
• 文字动效优先：呼吸光晕、渐入浮现、丝绒晕染、烛光摇曳
• 禁止生硬弹跳和快速闪烁；所有动效应如丝绒般顺滑、暧昧、有呼吸感
• 情色场景使用更慢、更柔的呼吸光效，配合微热的暖色调叠加



## 第二部分：开机动画

整体流程：暗金色微光 → 城市夜景缓缓浮现 → 镜头下降到会所门口 → 门推开暖光倾泻 → 化妆间镜像 → 「绯红会所」标题 → 进入按钮。
第 0.5 秒：
屏幕中央一点暖金色微光，慢慢扩大、弥散，像火柴点燃的光晕。
第 1.5 秒：
微光中渐显城市夜景轮廓——是俯瞰视角，灯火璀璨，夜色迷蒙。
画面缓缓下降，像从高空落向地面，最终定格在一栋暗金低调的建筑门口。
铜制门牌上刻着「绯红会所 · The Lust Gallery」几个字，字体优雅，泛着暖光。
门前立着两个西装保镖的剪影。
第 4 秒：
厚重的暗红实木大门缓缓推开，温暖昏黄的灯光从里面倾泻而出。
隐约可以看到水晶吊灯的折射光、丝绒窗帘的褶皱、还有——晃动的人影。
画面推入大门，穿过光线，越来越快……
第 5.5 秒：
画面突然定格在一面化妆镜上。
镜子里映出模糊的女性身影，桌上摆着皮鞭、项圈、口红。
一行优雅的手写字缓缓浮现：「今晚，你是女王。」
字体：Dancing Script 22px，玫瑰金 #d4a373，带柔和光晕。
第 7 秒：
标题浮现——「绯红会所」
Playfair Display 42px，居中，玫瑰金，暖光呼吸光晕。
副标题手写字——「The Lust Gallery」
第 8 秒：
◆ 玫瑰点缀 ◆
按钮出现——「踏入回廊」
玫瑰金描边 + 透明底，hover 时暖金色从中间扩散填充，文字变深酒红。
点击按钮后：
开屏层向右上缓缓滑出 + 渐隐，封面页从左下放大浮现，丝滑过渡，无任何白屏或跳转。
动画 CSS 片段
// css
/* 开屏容器 */
.splash-screen {
position: fixed;
inset: 0;
background: #1a0f0f;
display: flex;
flex-direction: column;
align-items: center;
justify-content: center;
z-index: 9999;
transition: all 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94);
overflow: hidden;
}
.splash-screen.fade-out {
opacity: 0;
transform: translate(10%, -10%) scale(1.1);
pointer-events: none;
}
/* 初始光晕 */
.opening-glow {
width: 4px; height: 4px;
background: #d4a373;
border-radius: 50%;
box-shadow: 0 0 20px #d4a373, 0 0 60px #d4a373;
animation: glowExpand 1.5s ease-out forwards;
}
@keyframes glowExpand {
0% { transform: scale(1); opacity: 0; }
50% { opacity: 1; }
100% { transform: scale(80); opacity: 0.05; }
}
/* 标题呼吸光 */
@keyframes roseGoldBreathe {
0%, 100% { text-shadow: 0 0 10px rgba(212,163,115,0.5), 0 0 20px rgba(212,163,115,0.2); }
50% { text-shadow: 0 0 20px rgba(212,163,115,0.7), 0 0 40px rgba(212,163,115,0.4), 0 0 60px rgba(184,74,74,0.2); }
}
.title-breathe {
animation: roseGoldBreathe 3s ease-in-out infinite;
}
/* 手写体渐入 */
.script-fade {
font-family: 'Dancing Script', cursive;
color: #d4a373;
opacity: 0;
animation: scriptIn 1.5s ease-out 0.5s forwards;
font-style: italic;
}
@keyframes scriptIn {
from { opacity: 0; transform: translateY(10px); letter-spacing: 4px; }
to { opacity: 1; transform: translateY(0); letter-spacing: 2px; }
}
/* 门推开光线效果 */
.door-light {
position: absolute;
top: 50%; left: 50%;
width: 0; height: 200vh;
background: linear-gradient(90deg, transparent, rgba(232,201,155,0.3), transparent);
transform: translate(-50%, -50%) rotate(15deg);
animation: doorOpen 1.2s ease-out forwards;
pointer-events: none;
}
@keyframes doorOpen {
0% { width: 0; opacity: 0; }
50% { opacity: 1; }
100% { width: 200vw; opacity: 0; }
}
/* 进入按钮 */
.enter-btn {
padding: 16px 56px;
background: transparent;
border: 1px solid #d4a373;
color: #d4a373;
font-family: 'Playfair Display', serif;
font-size: 16px;
letter-spacing: 6px;
cursor: pointer;
transition: all 0.5s ease;
position: relative;
overflow: hidden;
opacity: 0;
animation: btnIn 0.8s ease-out 7.5s forwards;
}
@keyframes btnIn {
from { opacity: 0; transform: translateY(20px); }
to { opacity: 1; transform: translateY(0); }
}
.enter-btn::before {
content: '';
position: absolute;
top: 0; left: 50%;
width: 0; height: 100%;
background: linear-gradient(90deg, #d4a373, #e8c99b);
transition: all 0.5s ease;
transform: translateX(-50%);
z-index: -1;
}
.enter-btn:hover {
color: #2a1a1a;
letter-spacing: 8px;
box-shadow: 0 0 30px rgba(212,163,115,0.5);
}
.enter-btn:hover::before {
width: 100%;
}
❦ 视觉之规 · 卷五终 · 封面页请待续卷 ❦



## 第三部分：封面页

从开机动画背后丝滑浮现，整体居中，优雅暧昧：
• 背景： 暖棕酒红径向渐变 radial-gradient(ellipse at center, #3d2424 0%, #1a0f0f 70%)，中央有极淡的丝绒纹理（CSS noise 低透明度）
• 背景粒子： 缓慢漂浮的金色光点（像灰尘在暖光中漂浮），大小 1-4px，随机位置，缓慢上升 + 左右漂浮
• 品牌名： 「绯红会所」Playfair Display 44px，玫瑰金 #d4a373，居中，呼吸光晕
• 手写副标题： 「The Lust Gallery」Dancing Script 20px，暖金色，位于品牌名下方略偏右
• 装饰线： 标题上下各一条优雅的弧线装饰（CSS 伪元素 + border-radius）
slogan： 「今夜，你是女王。」米灰金色，14px，letter-spacing 4px
• 按钮： 「踏入会所」按钮，与开屏一致。点击后封面页向上淡出 + 轻微模糊，角色创建页从下方丝滑浮入



## 第四部分：角色创建界面

整体布局
单页优雅表单，分五大区块，一次性完整填写，全部完成后点击「确认登场」进入游戏。
背景是暖棕渐变，每个区块都是丝绒质感卡片，圆角稍大（12-16px），有暖光投影。
区块一：女王基础档案
艺名：文本输入框（玫瑰金边框发光，placeholder「你的女王名号」）
年龄：数字输入框（小巧精致）
外貌描述：多行文本域（暖棕底、玫瑰金边框，4行高）
性格类型：标签多选（高冷女王 / 温柔御姐 / 狡黠魅惑 / 暴虐施虐 / 反差萌）



（续）

区块二：角色定位
角色定位（单选卡片）：纯支配型 / 支配为主偶尔臣服 / 互换型 / 喜欢被挑战后反杀
体位偏好（单选）：上位 / 下位 / 都喜欢
称呼偏好（标签多选）：主人 / 女王 / 妈咪 / 姐姐 / 女士 / 老师 / 宝贝
区块三：性偏好设定
三列标签组，全部多选：
施虐偏好：打屁股/鞭打、乳头折磨、边缘控制、羞辱play、道具惩罚、强制高潮、滴蜡冰play、捆绑束缚、口交控制、骑乘支配
受虐偏好：被打屁股、被强吻、被强制高潮、被羞辱、被捆绑、被内射、被多人轮、后庭开发
其他偏好：公开露出、群交、内射、道具play、角色扮演、身体开发、失禁潮吹、精液play
区块四：登场设定
初始场景（单选卡片）：化妆间 / 大堂 / 酒吧区 / VIP包厢
初始时间段（单选）：傍晚 / 黄金时段 / 深夜
底部居中大按钮：「确认登场」——玫瑰金渐变底 + 深酒红色字，letter-spacing 6px，hover时暖光晕扩大。
点击按钮后：角色创建页向右下渐隐 + 微缩，剧情主界面从左上放大浮现 + 暖光过渡，无缝进入第一幕。
❦



## 第五部分：主剧情界面

整体布局
单页优雅表单，分五大区块，一次性完整填写，全部完成后点击「确认登场」进入游戏。
背景是暖棕渐变，每个区块都是丝绒质感卡片，圆角稍大（12-16px），有暖光投影。
区块一：女王基础档案
艺名：文本输入框（玫瑰金边框发光，placeholder「你的女王名号」）
年龄：数字输入框（小巧精致）
外貌描述：多行文本域（暖棕底、玫瑰金边框，4行高）
性格类型：标签多选（高冷女王 / 温柔御姐 / 狡黠魅惑 / 暴虐施虐 / 反差萌）
区块二：角色定位
角色定位（单选卡片）：纯支配型 / 支配为主偶尔臣服 / 互换型 / 喜欢被挑战后反杀
体位偏好（单选）：上位 / 下位 / 都喜欢
称呼偏好（标签多选）：主人 / 女王 / 妈咪 / 姐姐 / 女士 / 老师 / 宝贝
区块三：性偏好设定
三列标签组，全部多选：
施虐偏好：打屁股/鞭打、乳头折磨、边缘控制、羞辱play、道具惩罚、强制高潮、滴蜡冰play、捆绑束缚、口交控制、骑乘支配
受虐偏好：被打屁股、被强吻、被强制高潮、被羞辱、被捆绑、被内射、被多人轮、后庭开发
其他偏好：公开露出、群交、内射、道具play、角色扮演、身体开发、失禁潮吹、精液play
区块四：登场设定
初始场景（单选卡片）：化妆间 / 大堂 / 酒吧区 / VIP包厢
初始时间段（单选）：傍晚 / 黄金时段 / 深夜
底部居中大按钮：「确认登场」——玫瑰金渐变底 + 深酒红色字，letter-spacing 6px，hover时暖光晕扩大。
点击按钮后：角色创建页向右下渐隐 + 微缩，剧情主界面从左上放大浮现 + 暖光过渡，无缝进入第一幕。
❦
第五部分：主剧情界面
整体布局
顶部优雅导航栏 + 中央叙事区 + 底部选项/输入区。
整体暖调，文字区有柔和的暖光叠层，营造烛光阅读感。
顶部导航栏
（规范描述协议中包含CSS结构，如.top-nav等样式定义，已完整保留）

剧情文本区
采用优雅字体，逐段浮现，具备暖光氛围。
包含环境描写、人物对话、心理活动、调教场景、权力博弈、身体反应。

底部选项区
固定在底部，背景带高斯模糊，支持A/B/C快捷选项与D自定义输入。
❦
第六部分：女王档案界面
界面布局
弹窗式，单栏优雅卡片。
顶部：圆形头像（丝绒边框+金色光晕）+ 艺名 + 称号标签
属性区：声望值 + 体力值 + 兴奋值 + 敏感度，各带优雅进度条
信息区：年龄、外貌、性格、定位、称呼、初始场景
底部：身体开发进度（乳头/后庭/喉咙/潮吹能力）
查看卷二（第七至九部分）





## 第六部分：女王档案界面

弹窗式，单栏优雅卡片。
顶部：圆形头像（丝绒边框+金色光晕）+ 艺名 + 称号标签
属性区：声望值 + 体力值 + 兴奋值 + 敏感度，各带优雅进度条
信息区：年龄、外貌、性格、定位、称呼、初始场景
底部：身体开发进度（乳头/后庭/喉咙/潮吹能力）



## 第七部分：客人档案界面

界面布局
弹窗式，顶部搜索栏 + 客人列表卡片。
每张卡片：头像 + 姓名 + 身份标签 + 好感进度条 + 调教程度徽章。
点击卡片展开详情：外貌描述、性格、性癖、调教记录、历史互动摘要。
Tab 分类：常客（回头客）/ 新客 / VIP / 对手（男dom / 强势sub）
样式 CSS
// css
.guest-tabs {
display: flex;
gap: 4px;
margin-bottom: 16px;
background: rgba(26, 15, 15, 0.6);
padding: 4px;
border-radius: 10px;
}
.guest-tab {
flex: 1;
padding: 8px;
text-align: center;
font-size: 12px;
color: #8b7a68;
cursor: pointer;
border-radius: 8px;
transition: all 0.35s ease;
font-family: 'Playfair Display', serif;
letter-spacing: 1px;
}
.guest-tab.active {
background: rgba(212, 163, 115, 0.15);
color: #d4a373;
}
.guest-tab .count {
font-size: 10px;
color: #b84a4a;
margin-left: 3px;
}
.guest-card {
background: rgba(26, 15, 15, 0.6);
border: 1px solid rgba(107, 58, 75, 0.3);
border-radius: 12px;
padding: 14px;
margin-bottom: 10px;
cursor: pointer;
transition: all 0.35s ease;
display: flex;
gap: 14px;
align-items: center;
}
.guest-card:hover {
border-color: rgba(212, 163, 115, 0.5);
background: rgba(212, 163, 115, 0.05);
transform: translateX(4px);
}



## 第八部分：道具库界面

弹窗式，顶部搜索 + 分类 Tab（束缚类 / 刺激类 / 打击类 / 温度类 / 扩张类 / 服装类 / 重型器械）。
道具网格：每个道具一张卡片——图标 + 名称 + 类型标签 + 「使用」按钮。
支持收藏/常用道具置顶。
样式 CSS
// css
.toy-search {
width: 100%;
padding: 10px 14px;
background: rgba(26, 15, 15, 0.7);
border: 1px solid rgba(107, 58, 75, 0.4);
border-radius: 10px;
color: #f0e6d8;
font-size: 13px;
margin-bottom: 12px;
transition: all 0.35s ease;
}
.toy-cats {
display: flex;
gap: 6px;
overflow-x: auto;
margin-bottom: 14px;
padding-bottom: 4px;
scrollbar-width: none;
}
.toy-grid {
display: grid;
grid-template-columns: repeat(3, 1fr);
gap: 10px;
}



## 第九部分：会所地图界面

弹窗式，按楼层分组展示。每一层一个折叠面板，带楼层名 + 简短描述。
点击某层展开区域列表。每个区域一张小卡片：名称 + 一句话氛围描述 + 状态徽章（当前位置 / 可前往 / 未解锁 / 有事件）。
楼层分组：
• 3层·顶级VIP区（VIP套房 / dom休息套房 / 观景台）
• 2层·包厢区（调教包厢 / 主题房 / 镜子房 / 多人房）
• 1层·公共区（大堂 / 酒吧 / 休息区 / 淋浴间）
• B1·功能区（道具库 / 医疗室 / 员工区）
• B2·惩罚重口区（惩罚室 / 深喉训练室 / 后庭开发室 / 炮机房 / 公开行刑台）
// css
.floor-section {
margin-bottom: 10px;
border-radius: 12px;
overflow: hidden;
border: 1px solid rgba(107, 58, 75, 0.3);
background: rgba(26, 15, 15, 0.6);
transition: all 0.35s ease;
}
.floor-header {
padding: 14px 16px;
cursor: pointer;
display: flex;
justify-content: space-between;
align-items: center;
transition: background 0.3s ease;
}



## 第十部分：委托任务面板

弹窗式，三Tab：进行中 / 可接取 / 已完成。
每个委托一张卡片：
• 委托名 + 等级（S/A/B/C）
• 委托人类型（富豪 / 明星 / 神秘人...）
• 报酬（声望+特殊奖励）
• 难度标签
• 简短描述
• 「接取」/「查看详情」按钮
样式 CSS
// css
.mission-card {
background: rgba(26, 15, 15, 0.7);
border: 1px solid rgba(107, 58, 75, 0.35);
border-radius: 12px;
padding: 14px 16px;
margin-bottom: 10px;
transition: all 0.35s ease;
position: relative;
}
.mission-card:hover {
border-color: rgba(212, 163, 115, 0.5);
box-shadow: 0 4px 15px rgba(0,0,0,0.2);
}
.mission-top {
display: flex;
justify-content: space-between;
align-items: flex-start;
margin-bottom: 8px;
}
.mission-name {
font-size: 15px;
color: #f0e6d8;
font-weight: 600;
flex: 1;
}
.mission-grade {
padding: 2px 10px;
border-radius: 6px;
font-size: 11px;
font-weight: bold;
font-family: 'Playfair Display', serif;
letter-spacing: 1px;
margin-left: 10px;
}
.grade-S { background: linear-gradient(135deg, #b84a4a, #8b3a3a); color: #fff; }
.grade-A { background: linear-gradient(135deg, #d4a373, #b8895a); color: #2a1a1a; }
.grade-B { background: rgba(107, 58, 75, 0.4); color: #d4a373; }
.grade-C { background: rgba(61, 36, 36, 0.8); color: #b8a88a; }
.mission-client {
font-size: 12px;
color: #b8a88a;
margin-bottom: 6px;
font-style: italic;
}
.mission-desc {
font-size: 12px;
color: #a08878;
line-height: 1.6;
margin-bottom: 10px;
}
.mission-bottom {
display: flex;
justify-content: space-between;
align-items: center;
}
.mission-reward {
◆ 玫瑰点缀 ◆
font-size: 11px;
color: #d4a373;
}
.mission-reward .num {
font-family: 'Cormorant Garamond', serif;
font-size: 15px;
font-weight: 600;
}
.accept-mission {
padding: 7px 18px;
background: linear-gradient(135deg, #d4a373, #b8895a);
border: none;
border-radius: 8px;
color: #2a1a1a;
font-size: 12px;
font-weight: 600;
cursor: pointer;
transition: all 0.3s ease;
font-family: 'Playfair Display', serif;
letter-spacing: 1px;
}
.accept-mission:hover {
box-shadow: 0 0 15px rgba(212,163,115,0.4);
}



## 第十一部分：调教室特殊UI效果

当进入调教场景（惩罚室/包厢/B2层）时，整体UI有暧昧强化效果：
// css
/* 调教模式：暖红叠层 */
.training-mode .story-area {
background: radial-gradient(ellipse at center, rgba(184,74,74,0.04) 0%, transparent 60%);
}
/* 调教场景分隔符（带装饰） */
.training-break {
text-align: center;
margin: 28px 0;
color: rgba(184, 74, 74, 0.5);
font-size: 11px;
letter-spacing: 5px;
font-family: 'Playfair Display', serif;
font-style: italic;
}
.training-break::before,
.training-break::after {
content: '♱ ─── ♱';
margin: 0 12px;
font-size: 10px;
}
/* 心跳边框（高潮/强烈刺激） */
.heartbeat-frame {
position: relative;
padding: 18px;
border-radius: 12px;
animation: heartbeatBorder 1.2s ease-in-out infinite;
background: rgba(184, 74, 74, 0.04);
◆ 玫瑰点缀 ◆
}
@keyframes heartbeatBorder {
0%, 100% {
box-shadow: inset 0 0 30px rgba(184,74,74,0.08);
border-radius: 12px;
}
50% {
box-shadow: inset 0 0 50px rgba(184,74,74,0.18);
border-radius: 14px;
}
}
/* 呼吸感文字（情欲场景整段） */
.breath-text {
animation: breatheText 5s ease-in-out infinite;
}
@keyframes breatheText {
0%, 100% { opacity: 1; transform: scale(1); }
50% { opacity: 0.94; transform: scale(1.004); }
}
/* 调教数据浮窗（右侧滑入） */
.training-panel {
position: fixed;
top: 65px; right: -300px;
width: 280px;
background: rgba(26, 15, 15, 0.97);
border: 1px solid rgba(184, 74, 74, 0.3);
border-right: none;
border-radius: 14px 0 0 14px;
padding: 18px;
transition: right 0.5s cubic-bezier(0.25, 0.46, 0.45, 0.94);
backdrop-filter: blur(12px);
z-index: 90;
max-height: calc(100vh - 100px);
overflow-y: auto;
box-shadow: -5px 0 25px rgba(0,0,0,0.3);
}
.training-panel.show {
right: 0;
}
.tp-title {
font-family: 'Playfair Display', serif;
color: #b84a4a;
font-size: 15px;
letter-spacing: 3px;
margin-bottom: 14px;
text-align: center;
}
.tp-target {
text-align: center;
margin-bottom: 14px;
}
.tp-target-name {
font-size: 14px;
color: #f0e6d8;
font-weight: 600;
}
.tp-target-state {
font-size: 11px;
color: #d46a6a;
margin-top: 4px;
font-style: italic;
}
/* 调教进度条 */
.tp-progress-group {
margin-bottom: 12px;
}
.tp-progress-label {
display: flex;
justify-content: space-between;
font-size: 11px;
color: #b8a88a;
◆ 玫瑰点缀 ◆
margin-bottom: 4px;
}
.tp-progress-bar {
height: 5px;
background: rgba(61, 36, 36, 0.8);
border-radius: 3px;
overflow: hidden;
}
.tp-progress-fill {
height: 100%;
background: linear-gradient(90deg, #8b3a3a, #d46a6a);
border-radius: 3px;
box-shadow: 0 0 6px rgba(184,74,74,0.5);
transition: width 0.5s ease;
}
.tp-tags {
display: flex;
flex-wrap: wrap;
gap: 5px;
margin-top: 12px;
}
.tp-tag {
padding: 3px 10px;
background: rgba(184, 74, 74, 0.12);
border: 1px solid rgba(184, 74, 74, 0.3);
border-radius: 12px;
font-size: 11px;
color: #d46a6a;
}



## 第十二部分：弹窗与消息提示

/* 确认弹窗按钮组 */
.modal-btn-group {
display: flex;
gap: 10px;
margin-top: 18px;
}
.modal-btn {
flex: 1;
padding: 11px;
background: rgba(107, 58, 75, 0.3);
border: 1px solid rgba(107, 58, 75, 0.5);
color: #b8a88a;
border-radius: 8px;
cursor: pointer;
font-size: 13px;
transition: all 0.35s ease;
font-family: 'Playfair Display', serif;
letter-spacing: 1px;
}
.modal-btn:hover {
border-color: #d4a373;
color: #d4a373;
background: rgba(212, 163, 115, 0.1);
}
.modal-btn.primary {
background: linear-gradient(135deg, #d4a373, #b8895a);
border: none;
color: #2a1a1a;
font-weight: 600;
}
.modal-btn.primary:hover {
box-shadow: 0 0 20px rgba(212,163,115,0.4);
}
.modal-btn.danger {
background: rgba(184, 74, 74, 0.2);
border-color: #b84a4a;
color: #d46a6a;
}
.modal-btn.danger:hover {
background: rgba(184, 74, 74, 0.3);
box-shadow: 0 0 15px rgba(184,74,74,0.3);
}



## 第十三部分：通用文字动效集

/* 玫瑰金呼吸发光 */
.rose-glow {
color: #d4a373;
animation: rosePulse 3s ease-in-out infinite;
}
@keyframes rosePulse {
0%, 100% { text-shadow: 0 0 6px rgba(212,163,115,0.4); }
50% { text-shadow: 0 0 16px rgba(212,163,115,0.7), 0 0 30px rgba(212,163,115,0.3); }
}
/* 丝绒晕开（重要词句出场） */
.velvet-in {
animation: velvetFade 1.2s cubic-bezier(0.25, 0.46, 0.45, 0.94) forwards;
opacity: 0;
filter: blur(4px);
}
@keyframes velvetFade {
to { opacity: 1; filter: blur(0); }
}
/* 烛光摇曳（环境描写文字） */
.candle-flicker {
animation: candleShake 4s ease-in-out infinite;
}
@keyframes candleShake {
0%, 100% { opacity: 1; text-shadow: 0 0 4px rgba(212,163,115,0.2); }
20% { opacity: 0.96; }
40% { opacity: 1; text-shadow: 0 0 8px rgba(212,163,115,0.3); }
60% { opacity: 0.98; }
80% { opacity: 1; text-shadow: 0 0 6px rgba(212,163,115,0.25); }
}



## 第十四部分：快捷菜单（≡）

点击导航栏最右侧「≡」展开右侧抽屉：
// css
.side-drawer {
position: fixed;
top: 0; right: -270px;
width: 250px;
height: 100%;
background: rgba(26, 15, 15, 0.98);
border-left: 1px solid rgba(212, 163, 115, 0.2);
z-index: 200;
transition: right 0.4s cubic-bezier(0.25, 0.46, 0.45, 0.94);
padding: 70px 16px 20px;
backdrop-filter: blur(14px);
overflow-y: auto;
box-shadow: -5px 0 25px rgba(0,0,0,0.4);
}
.side-drawer.show {
right: 0;
}
菜单项目：
• 女王档案
• 客人档案
• 道具库
• 会所地图
• 委托任务
• ── 分割 ──
• 调教记录
• 身体开发
• 收藏夹
• ── 分割 ──
• 游戏设置（文字速度 / 动效强度 / 主题色）
• 存档 / 读档
• 关于



## 第十五部分：响应式适配

@media (max-width: 768px) {
.story-area {
padding: 70px 16px 150px;
font-size: 14px;
line-height: 1.9;
}
.option-grid {
flex-direction: column;
}
.option-btn, .custom-option {
min-width: 100%;
}
}
@media (max-width: 480px) {
.toy-grid {
grid-template-columns: repeat(3, 1fr);
}
}



## 第十六部分：运行说明与HTML结构参考

页面结构总览
整个游戏为单页应用（SPA），所有界面通过 CSS 类切换，无刷新无跳转。
// html
<!DOCTYPE html>
◆ 玫瑰点缀 ◆
<html lang="zh-CN">
<body>
<!-- 开机动画 -->
<div id="splashScreen" class="splash-screen screen active">
<!-- 封面页 -->
<div id="coverPage" class="cover-page screen">
<!-- 角色创建页 -->
<div id="createPage" class="char-create screen">
<!-- 主游戏界面 -->
<div id="gamePage" class="screen">
◆ 玫瑰点缀 ◆
</body>
核心流程
1. 打开页面 → 开机动画（光晕→城市→会所大门→化妆间→标题→进入按钮）
2. 点击「踏入回廊」→ 开屏层右上滑出 + 封面页左下放大浮现（丝滑过渡）
3. 点击封面按钮 → 封面向上淡出 → 角色创建页从下方浮入（单页大表单，一次性填完）
4. 点击「确认登场」→ 创建页右下渐隐 → 游戏页左上放大浮现 → 第一幕剧情开始
5. 游戏全程在主界面进行，功能为弹窗叠加
6. 每段剧情 400 字以上（重要场景 800+），逐段浮现
7. 底部 ABCD 常驻，D 支持回车快捷发送
确认完成



## 第十七部分：色彩与字体速查表

| 用途 | 名称 | 色值 |
|---|---|---|
| 主背景色 | 暖棕酒红 | #2a1a1a |
| 面板底色 | 深玫瑰棕 | #3d2424 |
| 一级底色 | 酒红棕 | #5a2e2e |
| 主色/金 | 玫瑰金 | #d4a373 |
| 亮金 | 暖金 | #e8c99b |
| 激情色 | 酒红 | #8b3a3a |
| 亮红 | 玫瑰红 | #b84a4a |
| 辅助色 | 丝绒紫 | #6b3a4b |
| 正文色 | 暖米白 | #f0e6d8 |
| 次文色 | 米灰金 | #b8a88a |

• 标题字体：'Playfair Display', 'Noto Serif SC', serif —— 优雅奢华，衬线体有会所感
• 正文字体：'Noto Serif SC', 'Songti SC', serif —— 中文阅读舒适
• 点缀字体：'Dancing Script', cursive —— 仅用于品牌名/特殊装饰字，手写体增添暧昧感
• 数字/代码字体：'Cormorant Garamond', serif —— 优雅衬线数字