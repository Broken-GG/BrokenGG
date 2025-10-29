# 🚀 CI/CD Setup Guide for Separate Repositories

## Overview

Since you have **two separate GitHub repositories**, you need to set up CI/CD pipelines for each one independently:

- **BrokenGG/Backend** - Backend API (.NET)
- **BrokenGG/Frontend** - Frontend Web App (HTML/JS/Nginx)

---

## 📋 What Happens Automatically

When you push code to GitHub, the CI/CD pipeline will:

### ✅ Backend Repository
1. Build the .NET project
2. Run unit tests
3. Build Docker image
4. Test the Docker container
5. Scan for security vulnerabilities
6. Report results on GitHub

### ✅ Frontend Repository
1. Validate HTML & JavaScript files
2. Check file structure
3. Build Docker image
4. Test the Docker container
5. Scan for security vulnerabilities
6. Report results on GitHub

---

## 🔧 Setup Instructions

### Step 1: Backend Repository Setup

You've already done this! The file is at:
```
Backend/.github/workflows/ci-cd.yml
```

**To activate it:**
```bash
cd c:\Users\Simon\BrokenGG\Backend
git add .github/workflows/ci-cd.yml
git commit -m "Add CI/CD pipeline"
git push origin Clean-up-and-project-changes
```

The pipeline will run automatically on every push!

---

### Step 2: Frontend Repository Setup

I created a file at:
```
Frontend/.github/workflows/ci-cd.yml
```

**You need to copy this to your Frontend repository:**

1. Navigate to your Frontend repo
2. Create the folder structure:
   ```bash
   cd path\to\your\Frontend
   mkdir -p .github\workflows
   ```

3. Copy the file:
   ```bash
   # Copy from c:\Users\Simon\BrokenGG\Frontend\.github\workflows\ci-cd.yml
   # to your Frontend repository's .github/workflows/ci-cd.yml
   ```

4. Commit and push:
   ```bash
   git add .github/workflows/ci-cd.yml
   git commit -m "Add CI/CD pipeline"
   git push
   ```

---

## 🔍 What to Keep in Mind

### 1. **Pipeline Triggers**

The pipeline runs when:
- ✅ You push to `main` or `develop` branches
- ✅ You open a Pull Request to `main`
- ✅ You push to your current branch (`Clean-up-and-project-changes`)

**To trigger it manually:**
1. Go to your GitHub repo
2. Click "Actions" tab
3. Select the workflow
4. Click "Run workflow"

---

### 2. **Secrets (API Keys)**

⚠️ **IMPORTANT**: Your `.env` file with the Riot API key is **gitignored** (and should stay that way!).

The CI/CD pipeline:
- ✅ Will build and test your code
- ✅ Will test the Docker image
- ❌ Won't have access to your Riot API key

This is **GOOD** for security, but means:
- Integration tests that need the API key will fail
- You can add the API key as a GitHub Secret if needed

**To add secrets (optional):**
1. Go to your GitHub repo
2. Settings → Secrets and variables → Actions
3. Click "New repository secret"
4. Name: `RIOT_API_KEY`
5. Value: Your actual API key

Then modify the workflow to use it:
```yaml
env:
  RIOT_API_KEY: ${{ secrets.RIOT_API_KEY }}
```

---

### 3. **Build Status**

After pushing, you'll see:
- ✅ Green checkmark = All tests passed
- ❌ Red X = Build or tests failed
- 🟡 Yellow circle = Running

You can click on it to see detailed logs!

---

### 4. **Docker Hub (Optional)**

If you want to automatically push Docker images to Docker Hub:

1. **Create Docker Hub account** at https://hub.docker.com/

2. **Add Docker Hub secrets** to GitHub:
   - `DOCKER_USERNAME` - your Docker Hub username
   - `DOCKER_PASSWORD` - your Docker Hub password/token

3. **Uncomment the Docker push section** in the workflow files

---

## 📊 Viewing Pipeline Results

### On GitHub:

1. Go to your repository
2. Click the **"Actions"** tab
3. See all workflow runs
4. Click on a run to see details

### On Pull Requests:

When you create a PR, you'll see:
- Build status checks
- Test results
- Security scan results

GitHub can **block merging** if tests fail!

---

## 🎯 Common Questions

### Q: Do I need to do anything after pushing?
**A:** No! The pipeline runs automatically. Just push your code.

### Q: What if the build fails?
**A:** 
1. Click on the failed workflow in GitHub Actions
2. Look at the error logs
3. Fix the issue locally
4. Push the fix - pipeline runs again automatically

### Q: Can I test the pipeline locally?
**A:** Not exactly, but you can:
```bash
# Test what the pipeline does:
dotnet build
dotnet test
docker build -t test .
```

### Q: Does this cost money?
**A:** No! GitHub Actions is free for public repos and has generous free tier for private repos.

---

## 🚨 Important Notes

### For Backend:

- ✅ CI/CD file is ready to use
- ✅ Will run on every push
- ⚠️ Tests need API key to fully work (add as GitHub Secret if needed)

### For Frontend:

- ⚠️ **You need to copy the CI/CD file** to your Frontend repository
- ✅ Then it will run automatically
- ✅ No secrets needed for frontend

---

## 📝 Next Steps

1. **Push your Backend changes**:
   ```bash
   cd Backend
   git add .
   git commit -m "Add CI/CD pipeline and improvements"
   git push
   ```

2. **Check GitHub Actions tab** - you'll see the pipeline running!

3. **Copy the Frontend CI/CD file** to your Frontend repository

4. **Watch it work!** Every push will automatically:
   - Build your code
   - Run tests
   - Build Docker images
   - Scan for vulnerabilities

---

## 🎓 What You're Getting

With this CI/CD setup:

✅ **Automated Testing** - Catch bugs before they reach production
✅ **Consistent Builds** - Same build process every time
✅ **Security Scanning** - Automatic vulnerability detection
✅ **Docker Images** - Always have a deployable container
✅ **Code Quality** - Enforce standards on every PR
✅ **Team Collaboration** - Everyone sees test results
✅ **Professional Workflow** - Industry-standard practices

---

## 🆘 Troubleshooting

### Pipeline not running?
- Check you pushed to the right branch
- Verify `.github/workflows/ci-cd.yml` exists in your repo
- Check the "Actions" tab is enabled in repo settings

### Build failing?
- Check the logs in GitHub Actions
- Test locally: `dotnet build` or `docker build`
- Ensure all files are committed

### Want to skip CI for a commit?
Add `[skip ci]` to your commit message:
```bash
git commit -m "Update README [skip ci]"
```

---

**You're all set!** Push your code and watch the magic happen! 🎉
