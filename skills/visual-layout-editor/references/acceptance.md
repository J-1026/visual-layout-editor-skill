# Acceptance paths

Use real browser events, with isolated test storage/profile so the user's layout is not polluted. Geometry unit tests supplement UI verification. Remove only the test data afterward.

1. Verify worktree, page source and preview process match the current development target. An external URL, historic page, proxy, clone or substitute demo does not pass.
2. Compare the registered inventory and actual selection. Identify granularity for pseudo-elements, SVG and Canvas. At matching desktop/mobile viewports, preserve untouched content, typography, color, positions, component reuse and surrounding UI. Test a nested group and its button, separately and without double offsets.
3. Drag a measured distance, repeat with scale and scroll, touch, release outside, Escape and pointercancel. Verify numeric and keyboard adjustment without intercepting form input.
4. Test all six region alignments, <=1 CSS px DOM error with the other axis unchanged. Group centering preserves internal distances.
5. Test six inter-element alignments with three differently sized objects. The key stays fixed; selection bounds are frozen; repeated alignment with existing offsets does not drift.
6. Distribute three differently sized objects horizontally/vertically: equal gaps, fixed endpoints, other axis unchanged. Check locked targets and insufficient space feedback.
7. Overlap two objects; test forward/backward/front/back via actual occlusion/hit targets. Select covered objects in the panel. Repeat with transformed ancestors. Multi-object reordering retains relative order.
8. Move, align, reorder and lock; fix; verify edit overlays hide and normal links/forms work; refresh; re-edit; cancel restores saved; save a second version and refresh.
9. Save desktop A and mobile B, switch back to A; change widths within and across breakpoints. Verify iframe viewport and no profile leakage or unintended overflow.
10. Test storage failure, corrupt JSON, wrong baseline/scope and multi-tab conflict without losing valid data/drafts. Check export. One undo per operation, redo restores it. Reset is scoped and cancel never changes saved.
11. Verify both saved offsets and editor are gated outside the enabled environment. For product editors, verify roles. After source integration, test old and empty storage for double offsets.

Report URLs, viewport dimensions, element counts/exceptions, measured before/after geometry, occlusion, save/refresh/re-edit results, changed files and untested items. Capture only page content without browser chrome. Button labels, state numbers, z-index changes, a successful storage call, HTTP 200 and build success alone do not pass.

For skill-only delivery, validate files, links, self-containment and coverage. Do not claim these runtime paths passed without execution, or change an unrelated website just to test the skill.
