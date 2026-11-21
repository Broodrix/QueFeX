# Push QuefeX claim docs from Termux (mobile)

You need: Termux, a GitHub account **Broodrix**, a Hugging Face account **Broodrix**,
and this claim zip extracted on the device.

Replace `Broodrix` only if your username differs (you said it is Broodrix on all accounts).

---

## 0. One-time Termux setup

```bash
pkg update -y
pkg install -y git openssh gh python

# Identity for commits
git config --global user.name "Broodrix"
git config --global user.email "YOUR_EMAIL@example.com"
```

Use the email attached to your GitHub account.

### Auth options (pick one)

**A — GitHub CLI (easiest on phone)**

```bash
gh auth login
# GitHub.com → HTTPS → Login with a web browser (or token)
```

**B — Personal Access Token (HTTPS)**

1. Phone browser: github.com → Settings → Developer settings → Personal access tokens  
2. Generate token with `repo` scope  
3. When `git push` asks for password, **paste the token** (not your GitHub password)

**C — SSH key**

```bash
ssh-keygen -t ed25519 -C "broodrix-termux" -f ~/.ssh/id_ed25519 -N ""
cat ~/.ssh/id_ed25519.pub
# Add that line in GitHub → Settings → SSH and GPG keys → New SSH key
```

---

## 1. Extract the claim package

```bash
termux-setup-storage
cd ~/storage/downloads
# If the zip is here:
unzip -o QuefeX_Claim_Docs.zip -d ~/quefex-claim
cd ~/quefex-claim
ls
```

You should see: `README.md`, `LICENSE`, `docs/`, `CITATION.cff`, `TERMUX_PUSH_GUIDE.md`, etc.

---

## 2. GitHub — create repo and push

### 2a. Create empty public repo on GitHub

In the phone browser:

1. github.com/new  
2. Repository name: `QuefeX` (recommended) or `quefex-claim`  
3. Public  
4. **Do not** add README / license on the website (you already have files)  
5. Create repository  

### 2b. Push from Termux

```bash
cd ~/quefex-claim

git init
git branch -M main
git add .
git status
git commit -m "Public claim: QuefeX RHMoE / RHMoE-GDM documentation (Broodrix 2026)"

# HTTPS (token or gh)
git remote add origin https://github.com/Broodrix/QuefeX.git
git push -u origin main

# OR SSH:
# git remote add origin git@github.com:Broodrix/QuefeX.git
# git push -u origin main
```

### 2c. Optional release tag

```bash
git tag -a claim-2026-11-21 -m "Public architecture claim RHMoE / QuefeX"
git push origin claim-2026-11-21
```

On GitHub: Releases → Draft a release from that tag (docs-only is fine).

---

## 3. Hugging Face — create model repo and push

Hugging Face uses Git + a token.

### 3a. Token

1. Browser: huggingface.co/settings/tokens  
2. New token → **Write** access  
3. Copy token (starts with `hf_...`)  
4. Save it offline; do not commit it into the repo  

```bash
# Store token for git (Termux)
pkg install -y git
git config --global credential.helper store
# First push will ask:
# Username: Broodrix
# Password: paste hf_ token
```

### 3b. Create model repo on the website

1. huggingface.co/new  
2. Owner: **Broodrix**  
3. Model name: `QuefeX` or `QuefeX-RHMoE`  
4. License: **Other** / note Proprietary in the card  
5. Create  

### 3c. Push claim files (same tree is fine)

```bash
cd ~/quefex-claim

# Optional: dedicate HF remote without disturbing GitHub remote
git remote add hf https://huggingface.co/Broodrix/QuefeX

# Ensure README.md is the model card (it already has YAML front matter)
git add .
git commit -m "HF model card: QuefeX RHMoE claim (no weights)" || true
git push hf main
```

If the HF default branch is `main` and the empty repo was just created, this works.
If HF created a tiny README and rejects non-fast-forward:

```bash
git pull hf main --rebase
# resolve if needed, then:
git push hf main
```

**Do not** upload `.qhb`, `.qfx`, `.npz`, or source zips to HF if you want to keep the implementation closed.

### 3d. Model card check

Open: `https://huggingface.co/Broodrix/QuefeX`  
Confirm license shows proprietary / other, and the classification text is visible.

---

## 4. After both are live

1. GitHub repo About → URL can point to the HF model page (or vice versa).  
2. Same one-liner on both profiles.  
3. Keep a **private** GitHub repo for real source (separate from `QuefeX` claim).  
4. Never force-push over the first claim commit if you care about the dated trail; add new commits instead.

---

## 5. Troubleshooting (Termux)

| Problem | Fix |
|---------|-----|
| `git push` authentication failed | Use PAT/token as password; or `gh auth login` |
| `gh: command not found` | `pkg install gh` |
| HF asks username | Username = HF account name (`Broodrix`); password = `hf_` token |
| Repo not empty | `git pull --rebase` then push; or delete the web-generated README once |
| Storage permission | `termux-setup-storage` and use `~/storage/downloads` |

---

## 6. Safety

- This package is **documentation only**.  
- Do not add private keys, tokens, or weights to the claim repo.  
- Rotate any token that appears in screenshots or shell history.

Copyright (c) 2026 Broodrix. All Rights Reserved.
