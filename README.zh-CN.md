<p align="center">
  <a href="README.md">English</a> · <a href="README.zh-CN.md">简体中文</a> · <a href="README.zh-TW.md">繁體中文</a>
</p>


# 开发中页面布局编辑器

**Agent 把页面做出来，你把元素摆到合适的位置。**

拖动标题、对齐卡片、调整遮挡顺序，保存后还能继续编辑。这个 Skill 让编程 Agent 将这些能力接入**你正在开发的真实前端项目**。

它来自我们开发 **[SkillGuide](https://skillguide.ai/?utm_source=github&utm_medium=readme&utm_campaign=visual_layout_editor)** 时的实际需求。SkillGuide 是我们正在做的 AI Skills、MCP 与 Plugins 发现网站。

**[下载安装包](https://github.com/j19881026/visual-layout-editor-skill/releases/latest)** · **[查看真实演示](#在真实项目中使用)** · **[逛逛 SkillGuide ↗](https://skillguide.ai/?utm_source=github&utm_medium=readme&utm_campaign=visual_layout_editor)**

## 为什么做这个 Skill

开发 SkillGuide 时，最后一点布局调整经常变成新一轮提示词：标题挪一下、按钮居中、卡片放到上面。我们希望直接在页面上把位置摆好，再将确认的结果交给 Agent。

于是把这套开发方式整理成了 Visual Layout Editor：你决定怎么摆，Agent 负责源码接入、保存和验证。

## 在真实项目中使用

[![SkillGuide 技能包详情页：可编辑区域与布局控制面板](media/desktop-drag.jpg)](media/desktop-drag.jpg)

**桌面端：直接拖动真实元素。** 标题通过真实鼠标操作向右移动40 px、向下20 px；蓝色选框与右侧 x/y 数值对应这次变化。[查看完整长截图](media/skillguide-full-page.png)。

<details>
<summary>桌面端：拖动后，一键水平居中</summary>

![桌面端水平居中后的真实截图](media/desktop-align.jpg)

点击水平居中后，x 从40变为85，y 保持20，区域中轴偏差变为0 px。这是实际浏览器截图。

</details>

### 移动端：调整后固定保存

<p>
  <img src="media/mobile-drag.jpg" alt="移动端实际拖动后x和y均为10，下方为对齐面板" width="280">
  <img src="media/mobile-saved.jpg" alt="移动端固定后的预览，选框消失并提供再次编辑按钮" width="280">
</p>

**左图：** 同一项目在390 × 844真实浏览器视口中，标题向右、向下各拖动10 px。**右图：** 固定保存后选框消失，保留“再次编辑”入口。这里展示响应式界面，不冒充手机真机触摸测试。


| 图中位置 | 对应操作 |
| --- | --- |
| **页面内容虚线框** | 选择标题、来源信息和成员卡片，拖动或输入 x/y 精调。 |
| **对齐控制区** | 相对区域居中，或让多个对象对齐到标记的关键元素。 |
| **元素清单与图层** | 选择被遮挡的对象，在支持的图层范围内调整前后顺序。 |
| **固定与再次编辑** | 保存布局，刷新恢复，需要时再次打开继续调整。 |

这个实例登记了 **35 个对象**，图层排序已验证的范围是同一父级。桌面和手机布局分别保存。截图使用中文页面，Skill 可接入其他语言的开发项目。

## 开始使用

### 1. 安装 Skill

在项目中运行 [Skills CLI](https://github.com/vercel-labs/skills) 命令，并选择你的编程 Agent：

```bash
npx skills add j19881026/visual-layout-editor-skill --skill visual-layout-editor
```

也可以直接下载 **[Skill ZIP](https://github.com/j19881026/visual-layout-editor-skill/releases/latest/download/visual-layout-editor-multilingual.zip)**，把其中的 `visual-layout-editor` 文件夹复制到 Agent 的技能目录。Codex 通常使用 `~/.codex/skills`；配置了 `CODEX_HOME` 时使用其 `skills` 子目录。替换旧版前先备份；当前会话未识别时，新开会话调用。

### 2. 指定你正在开发的页面

打开项目源码后，对 Agent 说：

```text
使用 $visual-layout-editor，在当前开发的详情页接入布局编辑。
标题、来源信息和成员卡片可以拖动，支持相互对齐、图层排序、
固定保存和再次编辑。保留页面现有设计，控件用中文。
打开真实预览，让我自己调整。
```

### 3. 摆放 → 保存 → 继续调整

Agent 找到当前源码页面并复用已有组件接入编辑器。你在真实预览里摆放、固定保存，需要时再次编辑。确定结果后，再要求 Agent 将这版布局固化到源码。

## 能力一览

| 你的需求 | Skill 指导 Agent 实现 |
| --- | --- |
| 精确调位置 | 拖拽、数值偏移、方向键、参考线和锁定。 |
| 让元素对齐 | 六种边缘/居中命令、关键元素或选区参照、等距排列。 |
| 改变遮挡关系 | 上移、下移、置顶、置底，明确显示图层限制。 |
| 反复试方案 | 草稿与固定版本、撤销重做、取消、重置、JSON 导出。 |
| 调手机和桌面 | 不同断点分别保存，避免互相覆盖。 |

## 使用前知道这几件事

**必须有当前项目和可修改的页面源码。** 这是 Agent Skill，由 Agent 在源码中接入控件，不是给任意网址开启编辑的浏览器扩展或在线平台。

| 操作 | 实际含义 |
| --- | --- |
| **固定保存** | 保存到编辑器配置的存储；本机浏览器存储只属于该浏览器及同一来源。 |
| **固化源码** | 另行要求 Agent 将确认布局写入项目 CSS 或配置。 |
| **发布上线** | 走项目已有发布流程。 |

仓库提供指令与参考规范，不包含独立编辑器运行库。当前试用通过了拖拽、对齐、同父级图层和持久化等核心路径，尚未验证全部要求或所有 Agent。**[查看实测范围与限制](docs/validation.md)**。

## 来自 SkillGuide

我们正在做 **[SkillGuide](https://skillguide.ai/?utm_source=github&utm_medium=readme&utm_campaign=visual_layout_editor)**：帮助你发现 AI Skills、MCP 和 Plugins，并找到它们的原始出处。这个 Skill 就是从网站开发中提炼出来的。

**[打开 SkillGuide →](https://skillguide.ai/?utm_source=github&utm_medium=readme&utm_campaign=visual_layout_editor)** · [发现 Skills](https://skillguide.ai/zh/skills) · [查看技能包](https://skillguide.ai/zh/packs)

如果对你有帮助，欢迎 Star；接入时遇到问题，可以[提交 Issue](https://github.com/j19881026/visual-layout-editor-skill/issues)，说明框架、目标区域和期望行为。

<details>
<summary><strong>开发者资料：实现规范与验收路径</strong></summary>

- [Skill 入口](skills/visual-layout-editor/SKILL.md)
- [中文指令](docs/zh-CN/SKILL.md)
- [交互与数据规范](docs/zh-CN/references/implementation.md)
- [真实浏览器验收](docs/zh-CN/references/acceptance.md)

保留原页面的设计与业务行为；检查实际坐标、遮挡、保存刷新和再次编辑，不能只凭菜单文案验收。

</details>

## 许可

Skill 指令与参考规范使用 [MIT](LICENSE)。截图与第三方内容保留各自权利，不在此许可授权范围内。
