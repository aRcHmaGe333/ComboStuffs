# ComboStuffs

Consumer-composed product bundles — a small project to record, timestamp, and publish consumer-submitted product-combination ideas and their provenance.

Purpose
- Present the idea described in `docs/original-idea.md` (consumer-composed product bundles).
- Provide IPClaim-compatible tooling (`VERIFY.md`, `.github/workflows/timestamp.yml`, `stamp.sh`) so authors can create a cryptographic timestamped claim.

Quickstart
1. Inspect the original submission: `docs/original-idea.md`
2. (Optional) Edit `LICENSE-APC-VF.md` or leave it for `stamp.sh` to apply.
3. Initialize git, commit, and run the stamping helper (examples below).

Example commands (run from this folder):

```powershell
git init
git checkout -b main
git add .
git commit -m "Initial ComboStuffs: project files and IPClaim templates"

# Create a cryptographic claim and fill the LICENSE automatically (author = your Windows username):
pwsh -Command "& { $tree = (& git rev-parse 'HEAD^{tree}'); $date=(Get-Date).ToUniversalTime().ToString('yyyy-MM-dd'); $year=(Get-Date).Year; $author=$env:USERNAME; (Get-Content -Raw LICENSE-APC-VF.md) -replace '\\[AUTHOR NAME OR ENTITY\\]',$author -replace '\\[AUTHOR NAME\\]',$author -replace '\\[INSERT ROOT HASH\\]',$tree -replace '\\[INSERT TREE HASH\\]',$tree -replace '\\[INSERT HASH\\]',$tree -replace '\\[HASH\\]',$tree -replace '\\[INSERT DATE AND TIME UTC\\]',$date 'UTC' -replace '\\[INSERT DATE UTC\\]',$date 'UTC' -replace '\\[YEAR\\]',$year | Set-Content -Encoding UTF8 LICENSE }
git add LICENSE
git commit -m "[APC] IPClaim stamp applied — LICENSE"
```

Verification
- See `VERIFY.md` for how anyone can verify a claim using OpenSSL.

Files of interest
- `docs/original-idea.md` — original idea text
- `LICENSE-APC-VF.md` — license template (ValueFlow variant)
- `VERIFY.md` — verification instructions
- `.github/workflows/timestamp.yml` — optional GitHub Action to record RFC3161 timestamps
- `stamp.sh` — stamp helper script (bash)

Contact
- This is a working draft for publishing consumer-composed bundles. Please open issues or PRs in this repository to suggest changes.
