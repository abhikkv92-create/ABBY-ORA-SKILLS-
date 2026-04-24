# GitHub Security Settings Guide

## Security Measures Implemented

This repository has the following security framework in place:

### 1. Files Created
- `SECURITY.md` - Security policy and terms
- Attribution headers in all skill files

### 2. GitHub Protections (Requires Manual Setup)

## Step-by-Step GitHub Configuration

### Step 1: Enable Branch Protection

1. Go to: https://github.com/abhikkv92-create/ABBY-ORA-SKILLS-/settings/branches
2. Under "Branch protection rules", click "Add rule"
3. Set branch name pattern: `main`
4. Enable ALL of these protections:
   - [ ] Require pull request reviews before merging (1 required)
   - [ ] Require status checks to pass before merging
   - [ ] Require conversation resolution before merging
   - [ ] Require commit signatures (if using GPG)
   - [ ] Require branches to be up to date before merging
   - [ ] Include administrators in protections
5. Click "Save changes"

### Step 2: Enable Security Features

1. Go to: https://github.com/abhikkv92-create/ABBY-ORA-SKILLS-/settings/security_analysis
2. Enable:
   - Dependency graph
   - Dependabot alerts
   - Secret scanning

### Step 3: Set Up Code Owners

Create a CODEOWNERS file:

```
# CODEOWNERS - These users are responsible for code quality

# Default owner
* @Abhikkv92
```

### Step 4: Enable Two-Factor Authentication

1. Go to: https://github.com/settings/security
2. Enable 2FA in your account settings

### Step 5: Repository Settings

1. Go to: https://github.com/abhikkv92-create/ABBY-ORA-SKILLS-/settings
2. Under "Features":
   - [x] Issues
   - [x] Projects
   - [x] Wiki (turn OFF to prevent modifications)
   - [x] Allow merge commits (turn OFF)
   - [x] Allow squash merging
   - [x] Allow rebase merging (turn OFF)
   - [x] Auto-merge (turn OFF)
   - [x] Allow outboundMerge pull requests (turn OFF)
3. Under "Pull Requests":
   - [ ] Allow edits by maintainers (turn OFF)

### Step 6: Enable Wikis OFF

Since we want protection:
1. Go to: https://github.com/abhikkv92-create/ABBY-ORA-SKILLS-/settings
2. Uncheck "Wikis" to disable it

---

## For GPG Signing (Advanced)

To set up GPG signing for verified commits:

```bash
# Generate GPG key
gpg --full-generate-key

# List your keys
gpg --list-secret-keys

# Configure git to use GPG
git config --global user.signingkey YOUR_KEY_ID
git config --global gpg.program gpg
git config --global commit.gpgsign true
```

This adds "Verified" badges to your commits.

---

## Quick Checklist

- [ ] Branch protection enabled
- [ ] Security analysis enabled
- [ ] 2FA enabled on your account
- [ ] Wiki disabled
- [ ] Merge options restricted
- [ ] CODEOWNERS created
- [ ] GPG signing configured (optional but recommended)