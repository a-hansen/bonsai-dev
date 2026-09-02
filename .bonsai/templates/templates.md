# Bonsai Templates

This guide routes to the templates available in the same resolved Bonsai Home. Templates are instantiated only by
their owning workflows; they do not define behavior independently of `specification.md` and those workflows.

| Template | Intended consumer / responsibility |
| --- | --- |
| `<bonsai-home>/templates/api_ext_template.md` | Code-map workflow when a subsystem needs selective, non-obvious extension mechanics. |
| `<bonsai-home>/templates/api_pub_template.md` | Code-map workflow when a subsystem needs selective, non-obvious caller mechanics. |
| `<bonsai-home>/templates/code_map_template.md` | Code-map workflow for the compact entry point and identity of a named source map. |
| `<bonsai-home>/templates/icebox_template.md` | Handoff workflow when the human first authorizes preserving an out-of-scope observation. |
| `<bonsai-home>/templates/manifest_template.tsv` | Code-map workflow when a fuller subsystem-to-owning-path manifest has justified lookup value. |
| `<bonsai-home>/templates/map_state_template.md` | Code-map workflow when active mapping work benefits from a minimal resumable state file. |
| `<bonsai-home>/templates/namespace_router_template.tsv` | Code-map workflow when a fuller namespace-to-subsystem router has justified lookup value. |
| `<bonsai-home>/templates/plan_phase_template.md` | Phase-execution workflow when a required detailed phase plan must be instantiated. |
| `<bonsai-home>/templates/subsystem_map_template.md` | Code-map workflow for a justified architectural subsystem map. |
| `<bonsai-home>/templates/symbol_index_template.tsv` | Code-map workflow when a selective symbol lookup index has justified value. |
