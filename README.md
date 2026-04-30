# meltano-hub-poc

Replica of meltano/hub's test_dispatcher CI workflow.

Demonstrates expression injection via filenames in pull_request_target:
- `get_changed_files` job interpolates `${{ steps.changed_files.outputs.all_changed_files }}`
  directly into a shell command without sanitization
- Filenames containing `$(...)` execute as bash command substitution
- `dispatch_tests` job interpolates `${{ matrix.changed_file }}` in run: blocks
- MELTYBOT_GITHUB_AUTH_TOKEN is available in the dispatch job
- No permissions: block → GITHUB_TOKEN has write access

Used for authorized security research only.
