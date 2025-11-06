# Quick Start - Manual GitHub Setup

Since you don't have `gh` CLI, here's how to set up manually:

## Step 1: Create GitHub Repository

1. Go to: https://github.com/new
2. Repository name: `evals-data`
3. Make it **Public**
4. **Do NOT** initialize with README (we already have files)
5. Click "Create repository"

## Step 2: Push Your Code

After creating the repo, GitHub will show you instructions. Run these commands:

```bash
cd /Users/brettyoung/Desktop/dev25/wandb_work/simplify/zzz_openevals/evals-data

# Add the remote (replace YOUR_USERNAME with your GitHub username)
git remote add origin https://github.com/YOUR_USERNAME/evals-data.git

# Push to GitHub
git push -u origin main
```

If the default branch is `master` instead of `main`, use:
```bash
git branch -M main
git push -u origin main
```

## Step 3: Enable GitHub Pages

1. Go to: https://github.com/YOUR_USERNAME/evals-data/settings/pages
2. Under "Build and deployment":
   - Source: Select **"GitHub Actions"**
3. Save

That's it! GitHub Actions will auto-deploy when you push.

## Step 4: Publish Your First Results

```bash
cd /Users/brettyoung/Desktop/dev25/wandb_work/simplify/zzz_openevals/weave_evals

# Run the publish script
./publish_to_github.sh
```

This will:
- Copy results from Flutter app assets
- Push to GitHub
- Trigger auto-deployment (~1 min)

## Step 5: Enable in Flutter

Edit: `zzz_front_end/evals_app/lib/services/eval_data_service.dart`

```dart
// Line 9: Change to true
static const bool useGitHubPages = true;

// Line 12: Already updated with your username
static const String githubPagesUrl = 'https://bdytx5.github.io/evals-data';
```

## Verify It's Working

After GitHub Actions completes (~1 min), visit:
- https://bdytx5.github.io/evals-data/models.json

You should see your models.json file!

---

## Alternative: Install GitHub CLI (Optional)

If you want the `gh` command for future use:

```bash
# macOS with Homebrew
brew install gh

# Then authenticate
gh auth login
```

But it's not required - the manual method above works perfectly!
