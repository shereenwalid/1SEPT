Three files:

1. **`utils/validation_step.py`** — resolution tracking (`_build_resolution`, `_extract_checks`, the new payload fields)
2. **`utils/config_loader.py`** — added the `sync_enabled` field
3. **`config.yaml`** — `sync_enabled: false`
4. **`pipeline.py`** — sync now gated on `sync_enabled` rather than just `source_bucket`

So four, not three — sorry. If you'd rather touch fewer files, you can skip the `pipeline.py` and config changes entirely and just set `source_bucket: ""` in your config; the sync already no-ops when it's empty. The `sync_enabled` flag is only clearer about intent.

That means the minimum for the resolution feature alone is **`utils/validation_step.py`**.

One caveat: this assumes your deployed copy is current. `validation_agent.py` changed last turn too (VAL-008 rewrite), and `utils/validation_step.py` changed then as well for the processing-date injection and note surfacing. If you skipped that update, take both files.
