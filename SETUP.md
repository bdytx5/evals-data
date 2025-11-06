# GitHub Pages Setup Guide

## What I've Done

✅ Created `/evals-data/` directory with GitHub Actions workflow
✅ Updated Flutter `eval_data_service.dart` to support GitHub Pages
✅ Created `publish_to_github.sh` script for easy publishing

## Step 1: Create GitHub Repository

```bash
cd /Users/brettyoung/Desktop/dev25/wandb_work/simplify/zzz_openevals/evals-data

# Create GitHub repo (replace YOUR_USERNAME with your GitHub username)
gh repo create evals-data --public --source=. --remote=origin --push
```

## Step 2: Enable GitHub Pages

```bash
# Enable GitHub Pages with source from main branch
gh api repos/YOUR_USERNAME/evals-data/pages -X POST -f source[branch]=main -f source[path]=/results

# Or do it manually:
# 1. Go to https://github.com/YOUR_USERNAME/evals-data/settings/pages
# 2. Under "Build and deployment" → Source: "GitHub Actions"
```

## Step 3: Copy Existing Results

```bash
cd /Users/brettyoung/Desktop/dev25/wandb_work/simplify/zzz_openevals/weave_evals

# Run the publish script to copy results and push to GitHub
./publish_to_github.sh
```

This will:
- Copy all results from `zzz_front_end/evals_app/assets/results/` to `evals-data/results/`
- Commit and push to GitHub
- GitHub Actions will auto-deploy to Pages (~1 minute)

## Step 4: Update Flutter App Configuration

Once GitHub Pages is live, update the Flutter service:

**File:** `zzz_front_end/evals_app/lib/services/eval_data_service.dart`

```dart
// Line 9: Set to true
static const bool useGitHubPages = true;

// Line 12: Replace YOUR_USERNAME with your GitHub username
static const String githubPagesUrl = 'https://YOUR_USERNAME.github.io/evals-data';
```

## Step 5: Remove Assets from pubspec.yaml (Optional)

After switching to GitHub Pages, you can remove the result assets to reduce app size:

**File:** `zzz_front_end/evals_app/pubspec.yaml`

```yaml
assets:
  # Remove these lines:
  # - assets/results/models.json
  # - assets/results/openai_gpt-5_20251106_000343/
  # - assets/results/openai_gpt-4.1_20251103_015714/
  # etc...

  # Keep only:
  - assets/images/logo.jpg
```

## Daily Workflow

### After Running New Evaluations:

```bash
cd /Users/brettyoung/Desktop/dev25/wandb_work/simplify/zzz_openevals/weave_evals

# Run publish script
./publish_to_github.sh
```

That's it! GitHub will auto-deploy in ~1 minute, and your Flutter app will fetch the latest results on refresh.

## Benefits

✅ **Smaller app**: No JSON files bundled (~1-5 MB smaller)
✅ **No rebuilds**: Just push JSON, app fetches latest data
✅ **Instant updates**: Results live in ~1 minute after push
✅ **Version history**: Git tracks all changes to results

## Testing

You can toggle between local assets and GitHub Pages anytime:

```dart
// Use local assets (for development)
static const bool useGitHubPages = false;

// Use GitHub Pages (for production)
static const bool useGitHubPages = true;
```

## Verify Deployment

After pushing, check:
- GitHub Actions: `https://github.com/YOUR_USERNAME/evals-data/actions`
- Live URL: `https://YOUR_USERNAME.github.io/evals-data/models.json`
