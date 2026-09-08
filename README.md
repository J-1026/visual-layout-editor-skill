<p align="center">
  <a href="README.md">English</a> · <a href="README.zh-CN.md">简体中文</a> · <a href="README.zh-TW.md">繁體中文</a>
</p>


# Visual Layout Editor

**Your agent builds the page. You put things where they belong.**

Drag a heading, line up a group of cards, adjust overlapping layers, then save and keep editing. This skill guides your coding agent to add those controls to the **real frontend project you are developing**.

Built while developing **[SkillGuide](https://skillguide.ai/?utm_source=github&utm_medium=readme&utm_campaign=visual_layout_editor)**, our directory for discovering AI Skills, MCP servers and plugins.

**[Download the Skill](https://github.com/j19881026/visual-layout-editor-skill/releases/latest)** · **[See the example](#see-it-in-a-real-project)** · **[Explore SkillGuide ↗](https://skillguide.ai/?utm_source=github&utm_medium=readme&utm_campaign=visual_layout_editor)**

## Why we made it

While building SkillGuide, small layout adjustments kept turning into another round of prompts: move this heading, center those buttons, bring that card forward. We wanted to make those decisions directly on the page, then hand the confirmed layout back to the agent.

Visual Layout Editor turns that development workflow into a reusable skill. You control the arrangement; the agent handles source integration, persistence and validation.

## See it in a real project

[![SkillGuide detail-page integration: editable page region and control panel](media/desktop-drag.jpg)](media/desktop-drag.jpg)

**Desktop — drag directly on the page.** The selected title was moved 40 px right and 20 px down using real pointer events. Its blue outline and the panel's x/y values show the same change. [Open the full-page capture](media/skillguide-full-page.png).

<details>
<summary>Desktop — align the selected title to the region center</summary>

![Desktop horizontal alignment after dragging](media/desktop-align.jpg)

Clicking horizontal center changed x from 40 to 85 while keeping y at 20; the measured region-center offset became 0 px. This is an actual browser capture.

</details>

### Mobile — adjust, then save

<p>
  <img src="media/mobile-drag.jpg" alt="Mobile editor after a real drag: x 10, y 10, with alignment controls" width="280">
  <img src="media/mobile-saved.jpg" alt="Mobile saved preview with the re-edit button and selection outlines removed" width="280">
</p>

**Left:** the same project at a real 390 × 844 browser viewport, after dragging the title 10 px right and down. **Right:** after saving, selection outlines are hidden and the re-edit button remains available. This captures the responsive UI, not a physical-device touch test.


| What you see | What you can do |
| --- | --- |
| **Outlined content region** | Select headings, source information and member cards; drag or enter x/y offsets. |
| **Alignment controls** | Center within the region, or align multiple objects to a marked key element. |
| **Element list and layers** | Select covered objects and adjust their order within a supported stacking scope. |
| **Save and re-edit** | Fix the current layout, refresh, then reopen it for another round of edits. |

This integration registers **35 objects**. Its tested layer controls work within the same parent. Desktop and mobile layouts are saved separately. The screenshot shows a Chinese page; the skill can be used with projects in other languages.

## Get started

### 1. Install the skill

With the [Skills CLI](https://github.com/vercel-labs/skills), run this from your project and choose your coding agent:

```bash
npx skills add j19881026/visual-layout-editor-skill --skill visual-layout-editor
```

Prefer a download? Get the **[installable ZIP](https://github.com/j19881026/visual-layout-editor-skill/releases/latest/download/visual-layout-editor-multilingual.zip)** and copy its `visual-layout-editor` folder into your agent's skills directory. For Codex, this is normally `~/.codex/skills`, or the `skills` directory under your configured `CODEX_HOME`. Back up an existing copy before replacement. Start a new agent session if it has not discovered the skill.

### 2. Point it at the page you are building

Open that project's source, then ask:

```text
Use $visual-layout-editor on the detail page we are developing.
Make the title, source information and member cards draggable.
Add element alignment, layer ordering, save and re-edit controls.
Keep the existing page design. Open the preview so I can arrange it.
Use English for the editor controls.
```

### 3. Arrange → save → refine

The agent locates your current source page, reuses its components and adds the editor. You arrange the real preview and save the layout. Reopen the editor whenever you want to refine it. Once you are happy, ask the agent to integrate the confirmed layout into source.

## The workflow at a glance

| Need | Skill guides the agent to provide |
| --- | --- |
| Position precisely | Drag, numeric offsets, arrow keys, selection guides and locking. |
| Align objects | Six edge/center alignments, a key element or selection bounds, and equal spacing. |
| Control overlap | Forward, backward, front and back, with explicit stacking limits. |
| Iterate safely | Draft/saved states, undo/redo, cancel, reset and JSON export. |
| Work responsively | Separate breakpoint layouts, without overwriting desktop with mobile. |

## Before you use it

**You need the current project and writable page source.** This is an agent skill, not a browser extension or a hosted editor. Your agent integrates the controls; installing the skill does not make arbitrary URLs editable.

| Action | Meaning |
| --- | --- |
| **Save / fix** | Persist the layout in the editor's configured storage. Local browser storage stays in that browser and origin. |
| **Integrate into source** | Ask the agent to turn your confirmed layout into project CSS or configuration. |
| **Deploy** | Release the project through its existing deployment process. |

The repository contains instructions and reference specifications, not a standalone editor runtime. The SkillGuide trial verified core drag/alignment, same-parent layers and persistence paths; it has not verified every requirement or every agent. **[Read the validation scope](docs/validation.md)** for exact evidence and limits.

## Built at SkillGuide

We are building **[SkillGuide](https://skillguide.ai/?utm_source=github&utm_medium=readme&utm_campaign=visual_layout_editor)** to help people discover AI Skills, MCP servers and plugins, with links back to their sources. This skill grew out of the work on the site itself.

**[Explore SkillGuide →](https://skillguide.ai/?utm_source=github&utm_medium=readme&utm_campaign=visual_layout_editor)** · [Browse Skills](https://skillguide.ai/en/skills) · [Browse skill packs](https://skillguide.ai/en/packs)

If this workflow helps, star the repository or [share an integration issue](https://github.com/j19881026/visual-layout-editor-skill/issues). Include your framework, the target region and the behavior you expected.

<details>
<summary><strong>For contributors: implementation and acceptance</strong></summary>

- [Skill entry point](skills/visual-layout-editor/SKILL.md)
- [Interaction and persistence](skills/visual-layout-editor/references/implementation.md)
- [Browser acceptance paths](skills/visual-layout-editor/references/acceptance.md)
- [Original Chinese instructions](docs/zh-CN/SKILL.md)

Preserve the host page's existing design and behavior. Check real alignment geometry, occlusion, save/refresh and re-edit flows; UI labels alone are not evidence.

</details>

## License

Skill instructions and reference specifications: [MIT](LICENSE). Screenshots and third-party content retain their respective rights and are excluded from that grant.
