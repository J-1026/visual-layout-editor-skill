<p align="center">
  <a href="README.md">English</a> · <a href="README.zh-CN.md">简体中文</a> · <a href="README.zh-TW.md">繁體中文</a>
</p>


# Visual Layout Editor

**Your agent builds the page. You put things where they belong.**

Drag a heading, line up a group of cards, adjust overlapping layers, then save and keep editing. This skill guides your coding agent to add those controls to the **real frontend project you are developing**.

Built while developing **[SkillGuide](https://skillguide.ai/?utm_source=github&utm_medium=readme&utm_campaign=visual_layout_editor)**, our directory for discovering AI Skills, MCP servers and plugins.

**[Download the Skill](https://github.com/j19881026/visual-layout-editor-skill/releases/latest)** · **[See the example](#see-it-on-the-skillguide-homepage)** · **[Explore SkillGuide ↗](https://skillguide.ai/?utm_source=github&utm_medium=readme&utm_campaign=visual_layout_editor)**

## Why we made it

While building SkillGuide, small layout adjustments kept turning into another round of prompts: move this heading, center those buttons, bring that card forward. We wanted to make those decisions directly on the page, then hand the confirmed layout back to the agent.

Visual Layout Editor turns that development workflow into a reusable skill. You control the arrangement; the agent handles source integration, persistence and validation.

## See it on the SkillGuide homepage

[![Actual SkillGuide homepage in edit mode: full hero, selected title, alignment guides and complete controls alongside the page](media/homepage-editing-overview.jpg)](media/homepage-editing-overview.jpg)

**The homepage stays visible while you edit.** The selected heading has a blue outline; dotted boxes mark the editable elements and a vertical guide marks the canvas center. The complete panel sits beside the hero, with a **211.5 px gap** from the canvas. Its alignment, layer, undo and save controls are visible without covering the page.

Captured directly in Chrome at **2495 × 1138** on September 8, 2026. This is the running development homepage in **edit mode**, using its existing design. [Open the full-page screenshot, including the footer](media/homepage-editing-full-page.jpg).

<details>
<summary>Real interaction: drag the title, then center it</summary>

![Homepage in edit mode after a real 10px right and down drag](media/homepage-editing-drag.jpg)

**Drag:** the title moved 10 px right and down; the panel shows x 10, y 10.

![Homepage still in edit mode after horizontal alignment](media/homepage-editing-aligned.jpg)

**Center:** the measured center error becomes 0 px; y stays at 10. Both images retain the selection, guides and full editing panel.

</details>

The skill came from this development workflow at SkillGuide. Desktop and mobile layouts can save separately. The homepage's glass objects retain their native 3D interaction; the panel edits registered page elements. [Read the validation scope](docs/validation.md) for tested behavior and limits.

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
Use $visual-layout-editor on the homepage we are developing.
Make the hero title, subtitle, buttons and decorative elements draggable
within the hero region.
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
