# Profile Shooter 🚀

A private repository that automatically generates and updates an animated space shooter WebP on your GitHub profile. Your GitHub contributions become enemies in an epic space battle!

<img src="./example.webp" alt="Space Shooter" width="100%">

## How It Works

1. **Corn Job**, run at set time automatically
2. It fetches your GitHub contribution data
3. Generates an animated WebP where your contributions become enemies
4. Pushes the animation to your profile repository (AnujYadav-Dev/AnujYadav-Dev)

Your profile README displays the ever-updating game!

---

## 🔧 Setup Instructions

### Step 1: Create a Personal Access Token (PAT)

You need a PAT to allow this repo to push to your profile repository.

1. Go to **[GitHub Settings → Developer settings → Personal access tokens → Tokens (classic)](https://github.com/settings/tokens)**

2. Click **"Generate new token"** → **"Generate new token (classic)"**

3. Configure the token:
   | Setting | Value |
   |---------|-------|
   | **Note** | `profile-animation-updater` (or any name you like) |
   | **Expiration** | 90 days, or "No expiration" |
   | **Scopes** | ☑️ `repo` (Full control of private repositories) |
   | | ☑️ `read:user` (Read user profile data) |

4. Click **"Generate token"**

5. **⚠️ IMPORTANT: Copy the token immediately!** You won't be able to see it again.

---

### Step 2: Add Token as Repository Secret

1. Go to **this repository** → **Settings** → **Secrets and variables** → **Actions**

2. Click **"New repository secret"**

3. Fill in:
   | Field | Value |
   |-------|-------|
   | **Name** | `GH_PAT` |
   | **Secret** | Paste your Personal Access Token |

4. Click **"Add secret"**

---

### Step 3: Run the Workflow

**Automatic:** The workflow runs daily at midnight UTC.

**Manual trigger:**
1. Go to **Actions** tab
2. Click **"Update Profile Space Shooter"** on the left
3. Click **"Run workflow"** → **"Run workflow"**

---

### Step 4: Add Animation to Your Profile

In your profile repository ([AnujYadav-Dev/AnujYadav-Dev](https://github.com/AnujYadav-Dev/AnujYadav-Dev)), edit `README.md` and add:

```markdown
<a href="https://github.com/AnujYadav-Dev/">
  <img src="game.webp" alt="Space Shooter" width="100%">
</a>
```

That's it! Your profile now shows an animated space shooter game based on your contributions! 🎮

---

## ⚙️ Customization

Edit `generate_webp.py` to customize:

```python
# ============================================================
# CONFIGURATION - Edit these values to customize your animation!
# ============================================================

USERNAME = "AnujYadav-Dev"       # Your GitHub username
OUTPUT_FILE = "game.webp"        # Output filename
STRATEGY = "random"              # Options: "random", "column", "row"
FPS = 40                         # Animation speed (20-50 recommended)
MAX_FRAMES = None                # Set to a number to limit frames (e.g., 500)
```

### Strategy Options

| Strategy | Description |
|----------|-------------|
| `random` | Ship attacks enemies in random order (chaotic!) |
| `column` | Ship clears enemies column by column (left to right) |
| `row` | Ship clears enemies row by row (top to bottom) |

### FPS Guidelines

| FPS | Result |
|-----|--------|
| 20-25 | Slower animation, smaller file size (~5-8 MB) |
| 30-40 | Balanced (recommended) (~8-12 MB) |
| 45-50 | Faster animation, larger file size (~12-15 MB) |

> ⚠️ **Note:** FPS above 50 may not display smoothly in all browsers.

---

## 🖥️ Running Locally

You can test the WebP generation on your local machine:

### Windows
```powershell
# Set your token
$env:GH_TOKEN = "your_token_here"

# Install dependencies
pip install -r requirements.txt

# Generate the WebP
python generate_webp.py
```

### Linux/Mac
```bash
# Set your token
export GH_TOKEN=your_token_here

# Install dependencies
pip install -r requirements.txt

# Generate the WebP
python generate_webp.py
```

---

## 🔍 Troubleshooting

### Workflow fails with "Bad credentials"

- Your PAT may have expired. Generate a new one and update the `GH_PAT` secret.

### Workflow fails with "Repository not found"

- Make sure your profile repository exists: `github.com/AnujYadav-Dev/AnujYadav-Dev`
- Verify the PAT has `repo` scope

### Animation not updating on profile

- Check if `game.webp` exists in your profile repo
- Clear your browser cache (GitHub caches profile READMEs)
- Try adding a query string: `![Space Shooter](game.webp?v=1)`

### Animation is too large

- Reduce FPS (e.g., from 40 to 25)
- Set `MAX_FRAMES = 400` to shorten the animation

### "User not found" error

- Verify the `USERNAME` in `generate_webp.py` is spelled correctly
- The username is case-sensitive

---

## 📁 Project Structure

```
Profile-Shooter/
├── .github/
│   └── workflows/
│       └── update-profile.yml    # GitHub Action workflow
├── src/
│   ├── cli.py                # CLI (not used, but kept for reference)
│   ├── github_client.py      # GitHub API client
│   ├── constants.py          # Game constants
│   └── game/
│       ├── animator.py       # WebP generation
│       ├── renderer.py       # Frame rendering
│       ├── game_state.py     # Game state management
│       ├── drawables/        # Ship, enemies, bullets, etc.
│       └── strategies/       # Attack patterns
├── generate_webp.py              # Main entry point
├── requirements.txt              # Python dependencies
└── README.md                     # This file
```

---

## 🙏 Credits

Based on [gh-space-shooter](https://github.com/czl9707/gh-space-shooter) by [czl9707](https://github.com/czl9707).

---

## 📄 License

MIT License - Feel free to customize and share!
