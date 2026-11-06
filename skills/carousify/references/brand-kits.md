# Brand kits

A brand kit is the identity on every slide: display **name**, **handle** (e.g. @carousify), **logo**, plus colors and
fonts the user saved.

- `list_brand_kits` shows each kit with its id, name, handle, logo, colors and fonts, and which is the default.
- `create_carousel`, `create_template` and `edit_carousel` take `brand_kit_id`. Without one, the workspace default is
  used (or the first kit). The kit fills the `brand-name`, `brand-user` and `brand-logo` slots on every slide — you
  never write those slots yourself.
- When the user names a brand ("use the Carousify brand", "post as Gronite"), match it by name or handle. If several
  kits look alike, ask which one (show their names and handles), rather than guessing.
- To fix a wrong or missing logo, name or handle on an existing draft: `edit_carousel` with the right `brand_kit_id`.
  If the kit's own logo is broken, the user needs to re-upload it in Carousify (Workspace settings › Brand Kit).
- When designing a new template, use the kit's colors and fonts as the starting palette unless the user asked for a
  different look; it makes the design feel like theirs.
- Brand kits are created and edited in the Carousify app, not through the connector.
