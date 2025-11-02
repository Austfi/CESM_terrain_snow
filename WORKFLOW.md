# Git Workflow Guide for CESM_terrain_snow

## Initial Setup

### Clone the repository (first time)
```bash
git clone https://github.com/Austfi/CESM_terrain_snow.git
cd CESM_terrain_snow
```

## Daily Workflow

### 1. Pull latest changes before starting work
```bash
git pull origin main
```

### 2. Create a new branch for your work
```bash
# Create and switch to a new branch
git checkout -b feature/your-feature-name

# Or if you prefer the newer syntax
git switch -c feature/your-feature-name
```

### 3. Make your changes
- Edit files
- Run notebooks
- Test your code

### 4. Stage and commit your changes
```bash
# Check what changed
git status

# Stage specific files
git add terrain_plot.ipynb

# Or stage all changes
git add .

# Commit with a descriptive message
git commit -m "Description of your changes"
```

### 5. Push your branch to GitHub
```bash
# Push the branch (first time)
git push -u origin feature/your-feature-name

# Subsequent pushes
git push
```

### 6. Create a Pull Request on GitHub
- Go to https://github.com/Austfi/CESM_terrain_snow
- Click "New Pull Request"
- Select your branch
- Add description and create PR

### 7. Merge and update main
After PR is merged:
```bash
# Switch back to main
git checkout main

# Pull the latest changes (including your merged PR)
git pull origin main

# Delete the local branch (optional cleanup)
git branch -d feature/your-feature-name
```

## Quick Commands Reference

```bash
# Check current status
git status

# See what branch you're on
git branch

# View commit history
git log --oneline

# See differences
git diff

# Discard local changes (be careful!)
git checkout -- filename

# Update from remote
git pull origin main

# Push to remote
git push origin main
```

