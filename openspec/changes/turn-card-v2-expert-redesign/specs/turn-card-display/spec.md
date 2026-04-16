## REMOVED Requirements

### Requirement: Turn card has five-layer visual hierarchy
**Reason**: v2 compresses to three lines; the "five layer" abstraction is replaced by a cleaner three-line pattern where risk is inlined into the secondary line rather than being its own layer.
**Migration**: See `turn-card-v2` spec. Existing `.turn-risk` DOM elements are removed entirely.

### Requirement: Identity line shows turn number, model, status dot, wait indicator
**Reason**: Status dot is replaced by the left-edge color bar (Ware's position channel is more effective than small dots). Model name is now session-aware (omitted when unchanged).
**Migration**: Remove `.status-dot` CSS and span. Add `.turn-left-bar` class on the `.turn-item`.

### Requirement: Risk badges surface actionable signals
**Reason**: `⚠` emoji badges caused symbol competition with other glyphs and failed Tufte's data-ink principle. Replaced by inline markers within the secondary line.
**Migration**: Remove `.turn-risk` layer and all `*-badge` classes except `.cred-highlight` (used in detail view). Emit compact inline markers (`✗tool`, `⟳Name×N`, `🔑cred`, `✂max`) on secondary line.

### Requirement: compact and inferred metadata available via tooltip
**Reason**: Retained in spirit but made stricter — the v2 spec forbids the `turn-meta` text suffix entirely; only tooltip remains.
**Migration**: Remove `.turn-meta` span output. Keep tooltip attribute.
