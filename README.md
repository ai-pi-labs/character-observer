<p align="center">
  <img src="docs/assets/aipi-banner.svg" alt="AIπ · AI圆周派 · AI-PI-LABS" width="100%">
</p>

<h1 align="center">Character Observer</h1>

<p align="center"><strong>一个角色，十九种观察视角。</strong><br>One character. Nineteen ways to see.</p>

<p align="center">
  <img src="docs/assets/modes-badge.svg" alt="19 种观察模式">
  <img src="docs/assets/prompts-badge.svg" alt="每次 1–20 条提示词">
</p>

<p align="center"><strong>简体中文</strong> · <a href="README.en.md">English</a></p>

<p align="center">
  <a href="#start">快速开始与安装</a> ·
  <a href="references/mode-examples.md">19 种模式案例</a> ·
  <a href="#usage">调用方式</a> ·
  <a href="SKILL.md">技能母版</a>
</p>

输入一个成年虚构角色，生成监控、手机随拍、长焦、反射、建筑框景等 **19 种观察视角**的摄影提示词。一次支持 **1–20 条**，自动变化场景、动作和构图，并保持角色识别特征。

**默认交付的是中文提示词。** 把生成的提示词复制到图像生成工具即可使用；本仓库不包含独立生图服务，也不需要运行程序。

- [完整母版：SKILL.md](SKILL.md)
- [19 种模式：逐个调用示例 + 可直接生图的完整提示词](references/mode-examples.md)

<a id="start"></a>

## 快速开始与安装

### 方法 A：直接复制母版，不安装

1. 打开 [SKILL.md](SKILL.md)，复制完整内容，作为当前任务的母版指令发给支持长文本的 AI 助手。
2. 接着发送角色和要求，例如：

```text
按照刚才的母版，为28岁原创成年城市旅人生成提示词。
mode=reflection n=3 scene=雨后商业街
黑色短发，海军蓝外套、卡其长裤、白色运动鞋，完整着装。
只要提示词。
```

3. 从回答中复制一条完整提示词到图像生成工具。需要案例参考时，把 [模式案例文件](references/mode-examples.md) 也提供给助手。

这种方式使用的是文本指令，不依赖助手能识别 `$character-observer` 命令。

### 方法 B：安装到本地 Codex

可以直接对 Codex 说：

```text
使用 $skill-installer，把 https://github.com/ai-pi-labs/character-observer
仓库根目录的 Skill 安装到我的本地环境，保留 references 文件夹。
```

仓库目前为私有，需要使用有访问权限的 GitHub 账号。也可以下载仓库，将文件夹命名为 `character-observer`，放到个人 Skills 目录，保持如下结构：

```text
~/.agents/skills/character-observer/
├── SKILL.md
├── README.md
└── references/
    └── mode-examples.md
```

Codex 支持个人目录 `~/.agents/skills` 和项目目录 `.agents/skills`；新技能未出现时可重启 Codex。在 Codex CLI 或 IDE 扩展中，可用 `$` 提及技能。安装目录与调用方式参考 [OpenAI 官方 Skills 文档](https://learn.chatgpt.com/docs/build-skills)。

<a id="usage"></a>

## 第一次调用

在已加载本 Skill 的对话中发送：

```text
$character-observer
角色="28岁原创成年城市旅人，黑色微卷短发，海军蓝外套、卡其长裤、白色运动鞋"
mode=smartphone n=1 scene=咖啡店门外
```

你会得到：参数摘要、一个画面标题、一段完整摄影提示词，以及与当前画面相关的避免项。想省去说明，就加一句“只要提示词”。

也可以只用自然语言：

```text
用 character-observer，给28岁原创成年城市旅人设计3条手机随手拍提示词。
地点在咖啡店门外，衣服保持一致，动作和构图各不相同，只要提示词。
```

## 常见用法

<details>
<summary>展开 7 种调用方式：批量、多视角、发现镜头与连续动作</summary>

### 同一种视角，生成五条不同画面

```text
$character-observer 28岁原创成年书店店员
mode=occluded n=5 scene=书店 continuity=same-character
```

全部采用前景遮挡模式，变化动作、人物落点、遮挡物或观察位置。

### 同一角色混用三种视角

```text
$character-observer 28岁原创成年城市旅人
mode=smartphone,reflection,paparazzi n=6
continuity=same-character discovered=off
```

总共六条，按所列顺序循环，每种模式两条。人物和服装保持一致。

### 全部十九种，各来一条

```text
$character-observer 28岁原创成年女快递员 mode=all
```

`mode=all` 未指定数量时默认十九条。若写 `mode=all n=5`，总数仍为五条，按母版顺序取前五种。

### 让部分画面出现“发现镜头”剧情

```text
$character-observer 28岁原创成年城市旅人
mode=smartphone n=8 discovered=25%
```

八条中两条表现角色发现镜头，其他六条专注自己的动作。剧情均为知情摆拍；无法合理看到摄影机的模式不会强行安排对视。

### 六格连续动作联络表

```text
$character-observer 28岁原创成年城市旅人
mode=contact-sheet n=1 panels=6 scene=咖啡馆公共露台
```

得到一条完整六格图的提示词，描写同一角色拿杯、喝水、放杯等连续动作。

### 同一事件的四个机位

```text
$character-observer 28岁原创成年展会向导
mode=multi-cam n=1 panels=4 scene=展馆入口 discovered=off
```

得到一条四宫格提示词。四格记录同一时刻的动作，改变摄影机位置，保持人物姿态、朝向和道具状态一致。

### 指定服装、天气与画幅

```text
$character-observer
角色="28岁原创成年女快递员，黑色齐耳短发"
mode=dashcam n=3 style=写实
scene=商业街 outfit="橙色夹克、黑色长裤、运动鞋"
time=傍晚 weather=雨后 ar=16:9 texture=balanced
discovered=off 只要提示词
```

</details>

## 十九种 mode 怎么选

将表格最后一列放在角色描述之后即可，例如：`$character-observer 28岁原创成年城市旅人 mode=cctv n=1`。每种模式的完整生图案例都在 [案例文档](references/mode-examples.md)，按相同顺序排列。

<details>
<summary>展开全部 19 种模式与最简参数</summary>

| mode | 视觉效果 / 适用画面 | 最简参数 |
|---|---|---|
| `cctv` | 固定高位监控；便利店、大厅 | `mode=cctv n=1` |
| `dashcam` | 隔挡风玻璃；商业街、停车区 | `mode=dashcam n=1` |
| `doorbell` | 门铃超广角；公共走廊、门口布景 | `mode=doorbell n=1` |
| `paparazzi` | 远距离长焦；虚构明星活动出口 | `mode=paparazzi n=1` |
| `smartphone` | 手机随手拍；生活动作、轻微歪构图 | `mode=smartphone n=1` |
| `reflection` | 角色出现在反射中；橱窗、镜面柱 | `mode=reflection n=1` |
| `bodycam` | 工作人员胸前记录仪；展馆引导 | `mode=bodycam n=1` |
| `tourist` | 游客照片中的偶遇；地标、广场 | `mode=tourist n=1` |
| `news-camera` | 虚构采访背景；步行街、展会 | `mode=news-camera n=1` |
| `contact-sheet` | 同一次拍摄的连续动作联络表 | `mode=contact-sheet n=1 panels=6` |
| `multi-cam` | 同一事件的不同设备视点 | `mode=multi-cam n=1 panels=4` |
| `occluded` | 近景遮挡；书架、植物、柱边 | `mode=occluded n=1` |
| `architecture-frame` | 建筑框中框；门洞、拱廊、柱廊 | `mode=architecture-frame n=1` |
| `urban-observer` | 城市远景里的小人物；广场、人群 | `mode=urban-observer n=1` |
| `behind-the-scenes` | 活动工作照；获准拍摄的候场区 | `mode=behind-the-scenes n=1` |
| `camera-test` | 还没准备好的摄影测试片 | `mode=camera-test n=1` |
| `discovered-camera` | 动作停顿、侧眼发现镜头 | `mode=discovered-camera n=1` |
| `public-transit` | 扶手、门框与车厢层次 | `mode=public-transit n=1` |
| `low-angle-public` | 公共空间低机位环境肖像 | `mode=low-angle-public n=1` |

</details>

## 参数速查

<details>
<summary>展开角色、镜头、连续性与网格参数</summary>

| 参数 | 默认值 | 如何使用 |
|---|---|---|
| `角色` / `character` | 原创28岁成年城市旅人 | 写清年龄、外貌、配色、完整服装；支持已明确成年的虚构角色 |
| `mode` | `auto` | 单模式、逗号分隔多个模式，或 `all` |
| `n` | `1` | 提示词总数，整数1–20；`all` 未指定 n 时为19 |
| `style` | `真人COS` | 写实、二次元、日系街拍、韩系生活记录、胶片 |
| `scene` | `auto` | 公开或允许拍摄的半公开场景 |
| `outfit` / `action` | `auto` | 指定完整服装 / 正在发生的生活动作 |
| `time` / `weather` | `auto` | 如傍晚、雨后、阴天 |
| `lens` | `auto` | 如 `85mm`；须符合模式的设备逻辑 |
| `ar` | `auto` | 如 `3:4`、`16:9`、`4:3` |
| `discovered` | `auto` | `off`、`on`、`0–100%`；控制发现镜头的条目数 |
| `obstruction` | `auto` | 前景遮挡占画面面积，`0–40%` |
| `texture` | `balanced` | `clean` 少瑕疵、`balanced` 适量、`rough` 较明显 |
| `continuity` | `auto` | `same-character` 同角色、`same-scene` 同场景、`free` 放开未指定项 |
| `layout` | `auto` | 普通模式为 `single`，联络表和多机位为 `grid` |
| `panels` | `auto` | 网格内小图数：4、6、9；联络表默认6、多机位默认4 |
| `text` | `none` | `fictional-overlay` 可添加简短虚构设备编号或时间码 |

完整默认值、冲突处理与模式视觉规格见 [SKILL.md](SKILL.md)。这些参数是提供给助手的文本约定，不是可在终端执行的命令行参数。

</details>

## 常见问题

<details>
<summary>展开数量、角色一致性、生图与安装问题</summary>

**`n=6` 是生成六张图片吗？**

默认是六条提示词。需要实际生成图片时另行明确要求，并使用当前环境可用的图像工具。

**`n=2 panels=6` 是多少条？**

在网格模式中，是两条提示词，每条描述一张含六个小图的网格图，共十二个小画面。

**怎么让人物保持一致？**

写清发型、配色、服装、饰品和道具，并用 `continuity=same-character`。同场景连续动作改用 `same-scene`。这是提示词层面的约束，实际生图后仍需检查人物一致性。

**不懂镜头参数可以用吗？**

可以。只提供成年虚构角色和想要的感觉，其余采用自动设置，例如：“做三条像游客偶遇的照片提示词。”

**怎么生成更有观察感的画面？**

指定一个具体动作、一种合理遮挡和一个观察位置，例如“在书架端部看见角色翻书”。`texture=rough` 只是增加成像瑕疵，不保证更自然，也不保证传播效果。

**安装后没有出现怎么办？**

检查 `character-observer/SKILL.md` 是否直接位于 Skills 目录下，避免多套一层下载文件夹；再重启 Codex。也可以先用上面的“方法 A”直接提供母版文本。

</details>

## 使用范围

仅用于明确成年、成年外观的虚构角色或成年演员知情摆拍，完整着装，在公开或获准拍摄的半公开空间中创作。不用于真实人物隐私侵犯、真实非自愿偷拍、未成年人、浴室/厕所/更衣室/卧室偷窥，或性化隐藏摄像头角度。监控、新闻、发现镜头等效果均为虚构视觉语言。
