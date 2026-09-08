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

## Current homepage integration — September 8, 2026

The showcase now uses the running development homepage and its existing responsive design, with the same editor runtime integrated into the homepage source. The September 1/2 reference screenshots were rejected as outdated and removed from the active showcase.

| Homepage check | Observed result |
| --- | --- |
| Published desktop drag capture | 1280 × 720 viewport; title moved from (161, 204.5) to (171, 214.5), a real +10/+10 px pointer drag. |
| Horizontal center | Title x became 160; center error 0 px; y remained 214.5. |
| Save / refresh / re-edit | A +30/+20 test was centered and saved; title geometry survived refresh and the re-edit control reopened the editor. |
| Mobile drag | 390 × 844 viewport; title moved from (20, 184) to (30, 194). |
| Mobile center / save / refresh | x became 20, y stayed 194; saved position survived refresh, with editing outlines hidden. |
| Breakpoint isolation | Returning from mobile restored the separately saved desktop offsets. |
| Normal page | With no editor query, no editor was mounted; the title matched its baseline geometry. |
| Existing layout transforms | Computed CSS translation is preserved when adding an editor offset; original inline styles are restored on disposal. |

The homepage's glass objects retain their native 3D interaction; independent WebGL object ordering is not controlled by this DOM layout panel. Homepage layer-order, every alignment command, physical-device touch, and storage-failure paths were not retested here. The earlier detail-page tests above remain separate evidence.

Runtime syntax and whitespace checks passed. Full TypeScript output matched the previous development baseline after path normalization; existing unrelated errors remain. No website deployment was performed.

The new images are uncomposited browser viewport captures. The full-page export from this browser produced duplicate regions and was excluded. Original detail-page captures remain available as supporting evidence: [desktop drag](../media/desktop-drag.jpg), [desktop center](../media/desktop-align.jpg), [mobile drag](../media/mobile-drag.jpg), [mobile saved](../media/mobile-saved.jpg).
