# Interaction and persistence

## Coordinates and selection

Use independent stable IDs, unique within a profile, never text, array indices or per-render randomness. Resolve duplicate matches explicitly. Retain hidden objects' data but exclude them from geometry. Define the region content box and padding convention. Convert all measured rectangles to the same coordinate space; do not mix client, page and offset-parent coordinates.

For an unrotated scaled canvas, local delta is screen delta divided by scale per axis. Nested rotation/scaling needs inverse transforms. Remeasure after scroll, fonts/images load and resize. Disable unsupported transforms rather than persisting approximate coordinates. Allow original overflow decorations unless bounds were requested. Apply a single boundary correction to a multiselection, retaining internal distances; explain oversized/conflicting constraints.

Click selects; Shift or explicit touch multiselect toggles. A hierarchy list must reach covered objects, groups and children. Cross-group alignment is allowed after coordinate conversion. Remove ancestor/descendant double selection. Locked objects cannot move but may be the alignment key.

## Pointer and keyboard transactions

Track pointer ID, start, initial offsets and selection; use pointer capture or equivalent reliable handling. One drag produces one undo entry. Pointerup commits the draft operation; pointercancel, blur or Escape restores its starting state and cleans up. Limit touch-action suppression to edit handles so the page can scroll. Releasing a drag must not activate links/forms. Child-relative offsets remain unchanged when their parent moves. Apply one common delta to a selection, mapped through each object's coordinate space.

Default keyboard step is 1 CSS px, Shift 10, unless the project has a convention. Avoid IME, contenteditable, inputs and shortcut conflicts.

## Deterministic alignment

For object (x,y,w,h) and reference (rx,ry,rw,rh), change only the stated axis:

| Operation | Target |
| --- | --- |
| Left | x = rx |
| Horizontal center | x = rx + (rw-w)/2 |
| Right | x = rx+rw-w |
| Top | y = ry |
| Vertical center | y = ry+(rh-h)/2 |
| Bottom | y = ry+rh-h |

With baseline deltas, add target-minus-current to the existing delta; never write absolute coordinates into dx/dy. Region alignment treats a multiselection as one bounding box. Key-element alignment keeps the marked key stationary. Selection-bound alignment freezes the starting bounds before moving each object. Remeasure actual DOM geometry with <=1 CSS px tolerance; UI labels claiming zero are not evidence. Guides show reference edges/centers. Optional snapping around 6 screen px is independent of explicit alignment and must not alter the other axis.

For horizontal distribution, sort by left position with stable ID ties, fixing the first left and last right edges. gap = (lastRight-firstLeft-sumWidths)/(n-1). Accumulate widths and gap; leave y unchanged. Vertical is analogous. Disable for fewer than three objects, negative gaps or moving locked targets; explain instead of silently overlapping/unlocking.

## Actual layer order

Maintain bottom-to-top stable ID order in each sortable scope. Forward/back swap neighbors; front/back move to endpoints. Boundary operations do nothing. Move multiselections as a block preserving relative order. Persist order and locks.

Inspect ancestor transform, opacity, filter, isolation, positioning and z-index. Child z-index cannot escape its stacking context, and ordinary z-index cannot override browser top-layer elements. Verify visual occlusion and hit targets. Prefer a shared stacking context or sortable parent layer without changing baseline appearance/flow. DOM reordering can change flex/grid and accessibility order; only restructure after verifying an isolated candidate's geometry, state and reading order. Explain impossible cross-context moves in the panel. If arbitrary ordering is required, missing adaptation remains unfinished. Tool/modal layers are excluded.

## State transitions

| Action | Result |
| --- | --- |
| Preview/refresh | Apply valid saved data, never an unfixed draft |
| Enter/re-edit | Clone saved, or baseline, into draft |
| Move/align/order | Mutate draft and add one undo transaction |
| Fix | Validate/persist; only after success replace saved and exit |
| Failure | Remain editing, retain draft, offer export and show failure |
| Cancel | Restore saved from entry |
| Reset | Restore current baseline into draft; undoable, not yet saved |
| Change breakpoint | Store profile draft, end drag, load target profile |

A minimal payload includes schemaVersion, projectId, pageId, regionId, profile, baselineVersion, coordinateMode (baseline-delta-css-px), canvas dimensions, elements keyed by ID with dx/dy/locked, layerOrder by scope, updatedAt. Use actual metadata and finite numbers. Storage keys include project/page/region/profile/baseline; keep saved and draft separate.

Validate schema, scope, baseline, finite values, unique registered IDs, complete layer membership and boolean locks. Never accept executable expressions, arbitrary CSS/HTML or foreign selectors. Preserve corrupt/incompatible data for recovery and explain it. New objects use baseline; deleted objects are reported as orphaned records rather than assigned elsewhere.

LocalStorage is specific to browser profile and origin (including port), not multi-device sync. Use the existing backend for collaboration, identity and concurrent writes. Catch access/quota errors and verify readback. Detect multi-tab revisions before overwrite; preserve local drafts when conflict occurs. Export distinguishes saved/draft and names profiles. Never clear all localStorage; reset only the selected region/profile unless a broader reset was requested.

## Integrating a confirmed layout into source

Only when requested, verify confirmed rendered positions and valid payload, then map them to component configuration or responsive CSS. Preserve flow where possible. Do not use scaled screen coordinates as CSS units or infer confirmation from a stale storage key. Advance baseline versions and migrate/zero old deltas for the affected profiles. Test empty storage, old saved data, refresh and editor disabled for double application. Deployment remains a separate authorized action.
