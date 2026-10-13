# GitHub release setup — NodeExpressIIS

> Instructions only — **do not run** until you explicitly approve publishing.
> This folder contains only approved release files. Nothing has been pushed anywhere.

## Repository structure

```
NodeExpressIIS/
├── NodeExpressIIS.exe          # application (unsigned)
├── NodeExpressIIS.msi          # installer (unsigned)
├── readme.html               # customer-facing documentation (installed with the MSI)
├── README.md                # GitHub documentation
└── assets/
    ├── logo.png
    ├── about_us.png
    └── icon.ico
```

Do NOT publish: the `.ps1` deployment/recovery scripts (embedded inside the EXE — see disclosure below), `DeployTool.exe`, `DeployTool.ps1`, source code, or build outputs.

## Create the repository (manual steps)

1. Go to https://github.com/new
2. Repository name: `NodeExpressIIS`
3. Visibility: **Private** (switch to Public later if you want)
4. **Do not** initialize with README/.gitignore (files already exist locally)
5. Click "Create repository"

## Push from this folder

```powershell
cd "C:\Users\akkia\OneDrive\Documents\Default Project\NodeExpress IIS Release"
git init
git add .
git commit -m "NodeExpress IIS v1.0.0 - initial release"
git branch -M main
git remote add origin https://github.com/akash-awaskar/NodeExpressIIS.git
git push -u origin main
```


## Create a GitHub Release

1. Repository → Releases → "Draft a new release"
2. Tag: `v1.0.0`
3. Title: `NodeExpress IIS v1.0.0`
4. Upload `NodeExpressIIS.msi` (and optionally `NodeExpressIIS.exe`)
5. Description: paste the Installation / Prerequisites sections from README.md

## Before publishing — checklist

- [x] GitHub URL set to https://github.com/akash-awaskar/NodeExpressIIS
- [ ] Confirm the contact details (binatechsolution@gmail.com, binatechs.in/contact) are correct
- [ ] Confirm the licensing API at `http://localhost:3000` requirement is acceptable to document
- [ ] Decide whether the MSI/EXE should be code-signed first (see "Code signing" in README.md)

## Disclosure — embedded content in the EXE

`NodeExpressIIS.exe` contains the three deployment PowerShell scripts (publish.ps1, deploy.ps1, recover.ps1) as **embedded resources** — they are part of the application's behavior (the tool extracts and runs them). They contain no credentials, tokens, or private URLs (only localhost/127.0.0.1 references and pm2/appcmd commands), but they are effectively published when the EXE is published. Confirm you approve this before making the repository public.
