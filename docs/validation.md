# Validation scope / 实测范围 / 實測範圍

This document describes the actual SkillGuide **source pack detail-page** trial. The skill's acceptance specification is broader than this one integration's completed checks.

| Path | Observed result |
| --- | --- |
| Drag | Title moved 40 CSS px right and 30 down through real Chrome pointer events. |
| Region horizontal center | DOM center error 0 px; y remained unchanged. |
| Key-element left alignment | Left-edge error 0 px; the key element stayed in place. |
| Same-parent layer ordering | Actual overlapping-card hit target changed after front/back actions. |
| Save and refresh | Saved x offset and layer value survived refresh. |
| Re-edit and cancel | A new draft offset was discarded and the saved offset restored. |
| Desktop/mobile isolation | A 390 × 844 viewport stored a separate layout; desktop values returned when switching back. |
| Baseline preservation | At the same viewport, the untouched final title matched its original geometry. |

35 registered objects. Chrome error logs were empty during the recorded trial. Runtime syntax and whitespace checks passed; full-project TypeScript output contained existing errors and matched the original development baseline with no new errors.

**Not verified:** real touch hardware, storage failures/conflict recovery, JSON download, exhaustive alignment/distribution paths, and cross-agent integration. **Not implemented in the trial:** arbitrary cross-parent layer ordering. Installing the skill is not installing a standalone runtime.

**简体中文：** 上表是 SkillGuide 试用的真实验证结果，共35个对象。图层仅验证同一父级；真机触屏、存储异常/冲突、JSON 下载、完整对齐/等距路径和跨 Agent 接入未全部验证。Skill 的完整验收规范不等于本实例已全部通过。

**繁體中文：** 上表為 SkillGuide 試用的真實驗證結果，共35個物件。圖層僅驗證同一父層；真機觸控、儲存異常/衝突、JSON 下載、完整對齊/等距路徑及跨 Agent 整合未全部驗證。完整驗收規格不代表本實例已全部通過。

The screenshot is a real development-page capture. Neither the screenshot nor these checks imply the editor has been deployed to the public SkillGuide website.

## Homepage showcase

The README homepage images are original development screenshots supplied by the project owner: desktop captured on 2026-09-01, and a fixed 390 × 844 mobile canvas captured on 2026-09-02. They were copied unchanged. The mobile image itself is 750 × 983 and includes the development canvas wrapper; it is not a physical-device capture. These images illustrate the skill’s origin and visible editor controls, not a new execution of the tests above.

The original detail-page captures remain available as supporting evidence: [desktop drag](../media/desktop-drag.jpg), [desktop center](../media/desktop-align.jpg), [mobile drag](../media/mobile-drag.jpg), [mobile saved](../media/mobile-saved.jpg).
