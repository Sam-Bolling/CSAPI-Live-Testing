# Quick Setup Guide

## Step 1: Create Private GitHub Repository

```bash
# Via GitHub CLI (if available)
gh repo create ogc-client-csapi-live-tests --private

# Or manually via GitHub web interface:
# 1. Go to https://github.com/new
# 2. Name: ogc-client-csapi-live-tests
# 3. Check "Private"
# 4. Click "Create repository"
```

## Step 2: Push Local Repository

```bash
cd C:\Users\sbolling\Documents\ogc-client-csapi-live-tests

# Add remote (replace YOUR_USERNAME with your GitHub username)
git remote add origin https://github.com/YOUR_USERNAME/ogc-client-csapi-live-tests.git

# Push to GitHub
git branch -M main
git push -u origin main
```

## Step 3: Configure GitHub Secrets

1. Go to repository Settings → Secrets and variables → Actions
2. Click "New repository secret"
3. Add three secrets:

   - **Name**: `CSAPI_LIVE_SERVER`
     **Value**: `http://45.55.99.236:8080/sensorhub/api`

   - **Name**: `CSAPI_LIVE_USER`
     **Value**: `ogc`

   - **Name**: `CSAPI_LIVE_PASS`
     **Value**: `ogc`

## Step 4: Verify Setup

```bash
# Run demo locally
npm run demo:connection

# Run tests locally (once auth issue is fixed)
npm test

# Check GitHub Actions
# Go to repository → Actions tab
# Workflow should be available but not run yet (waits for schedule or manual trigger)
```

## Step 5: Link to Main Repository

The `package.json` already references the main library:
```json
"dependencies": {
  "@camptocamp/ogc-client": "file:../ogc-client-CSAPI"
}
```

Whenever you make changes to `ogc-client-CSAPI`:
```bash
cd ogc-client-csapi-live-tests
npm install  # Refreshes the link
npm test     # Validate changes
```

## Maintenance

### Update Credentials
Edit `.env` file locally (it's gitignored, won't be committed).
Update GitHub Secrets if they change.

### Add New Tests
1. Edit `tests/live-server.integration.spec.ts`
2. Test locally: `npm test`
3. Commit and push
4. CI will run on next schedule or manual trigger

### View Test Results
- GitHub Actions artifacts (30 day retention)
- Local: check `test-results/` and `coverage/` directories

## Security Checklist

- ✅ Repository is PRIVATE
- ✅ `.env` file is gitignored
- ✅ Credentials in GitHub Secrets (encrypted)
- ✅ No credentials in code (uses environment variables)
- ✅ README warns about privacy

## Done! 🎉

Your private testing repository is ready to:
- Validate CSAPI implementation continuously
- Run demos with real data
- Prove production-readiness
- Support Phase 6 upstream contribution
