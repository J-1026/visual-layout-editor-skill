---
name: visual-layout-editor
description: Add drag, alignment, layer ordering, save and re-edit controls to a selected region in the frontend project currently under development, with writable source access. Use for hands-on layout adjustment during development, not arbitrary URL editing.
---

# Visual Layout Editor

Integrate a real layout editor into the user's current development page. The user arranges elements; the agent supplies controls, validates behavior and saves reliably. Do not infer final coordinates from a screenshot.

## Establish the actual target

Identify the current worktree, page source, region and matching preview process. A URL locates a preview; it does not establish source access. If only an external URL or reference screenshot is available, ask for the development project. Do not proxy, inject into, clone or replace an external site with a demo. “Let me try” means opening the integrated current development page, not a historical page or unrelated example.

Read project rules and reuse existing components, CSS and editor controls. Inspect the actual page at the same desktop and mobile widths. State target elements, reuse sources and allowed changes. Preserve content, typography, colors, sizes, animations, business behavior and surrounding layout unless explicitly requested.

Use the user's language for the panel, feedback and handoff, including English, Simplified Chinese or Traditional Chinese. Translate visible labels consistently without changing stable IDs or data keys. Changing the editor language does not authorize translating the underlying page content.

## Register the selected region

Inventory text, buttons, images, icons, decorations, fields and containers with stable IDs, hierarchy, breakpoint visibility and stacking context. Support groups and children; prefer the deepest editable object and provide parent/child selection. Prevent selecting both an ancestor and descendant for double movement.

Existing reference backgrounds/guides start locked with an unlock control; include backgrounds when requested. Pseudo-elements need proxy objects. SVG, Canvas and WebGL internals need explicit adapters; moving the whole surface is not per-object editing. Report unsupported granularity as unfinished.

Read [interaction and persistence](references/implementation.md) before implementation and [acceptance paths](references/acceptance.md) during verification.

## Required behavior

- Drag by mouse and touch, with selection boxes, coordinates and guides. Provide numeric x/y and arrow-key adjustment; Shift increases the step. Do not steal keys from text inputs.
- Align left/center/right and top/middle/bottom to the region. Horizontal centering changes x only; vertical centering changes y only. Align a multiselection as a group to preserve internal spacing.
- Align elements to a clearly marked key element or frozen selection bounds. The key remains stationary. Distribute three or more elements evenly with fixed endpoints; explain insufficient space.
- Move layers forward/backward/front/back with genuine visual ordering. Select covered objects through the object list. Expose stacking boundaries and disable impossible operations instead of showing ineffective z-index changes.
- Maintain baseline, saved and draft states. Save/fix validates and persists the draft, exits editing and restores normal links/forms. Refresh restores the saved version. A discoverable re-edit entry loads that version.
- Undo/redo complete operations. Cancel restores the version from entry. Reset to default is a separate undoable action and does not overwrite saved state until fixed.
- Export validated layout JSON, clearly identifying saved versus draft. Source integration and deployment are separate, user-requested actions.

## Integration constraints

Edit actual DOM elements and preserve framework state/events. Do not substitute screenshots or transparent hotspots. Do not convert all flex/grid layouts to absolute positioning. Compose offsets independently of existing transforms and animations; check wrappers for selector, flow and stacking changes.

Keep the collapsible tool panel outside the content region or in a separate tool layer. A mobile iframe workbench must have a real mobile viewport, not just a narrow desktop border. In edit mode prevent accidental navigation/submission; restore normal behavior on exit. Exclude tools/overlays from editable objects.

Isolate saved and draft layouts by project/page/region/breakpoint/baseline. Follow project breakpoints, retain each profile's draft and end dragging before switching. Default to a development-only integration with the same environment gate for both editor and saved offsets. If the user requests a public/admin editor, follow existing authentication and persistence architecture rather than imposing localhost.

“Fixed” means persisted and no longer editing, not committed or deployed. When the user requests source integration, map the confirmed layout to configuration/responsive CSS and advance the baseline to prevent double offsets. Follow the project's release authorization.

## Delivery

Verify actual drag, inter-element alignment, occlusion, refresh and re-edit paths. Buttons, screenshots and successful builds alone are not proof. Report working edit/preview URLs, registered elements and exceptions, persistence scope, checks and unfinished items. Use page-content screenshots, including the full page when useful; exclude browser tabs, address/bookmark bars and desktop chrome.

When delivering only this skill, validate structure, references and requirement coverage; do not invent runtime evidence or modify an unrelated site merely to test it.
