# SwingLab — AI Baseball Swing Analyzer

Upload a swing video, get instant AI-powered coaching feedback compared to pro MLB hitters.

---

## Project Structure

```
swinglab/
├── public/
│   └── index.html      ← Frontend (copy index.html here)
├── server.js           ← Secure backend (hides your API key)
├── package.json
├── .env.example        ← Copy to .env and add your API key
└── .gitignore
```

**Important:** Move `index.html` into a `public/` folder before running.

---

## Local Setup (run on your computer)

### 1. Install Node.js
Download from https://nodejs.org (LTS version)

### 2. Set up the project
```bash
# Create the public folder and move index.html into it
mkdir public
mv index.html public/

# Install dependencies
npm install

# Set up your API key
cp .env.example .env
# Open .env and paste your Anthropic API key
```

### 3. Get your Anthropic API key
- Go to https://console.anthropic.com
- Create an account / sign in
- Go to API Keys → Create Key
- Copy the key and paste it into your .env file

### 4. Run the app
```bash
npm start
```
Open http://localhost:3000 in your browser. Done!

---

## Deploy to the Web (Render — Free)

Render.com is the easiest free hosting option for this backend.

### 1. Push to GitHub
```bash
git init
git add .
git commit -m "Initial SwingLab commit"
```
Create a new repo at github.com and push:
```bash
git remote add origin https://github.com/YOURUSERNAME/swinglab.git
git push -u origin main
```

### 2. Deploy on Render
1. Go to https://render.com and sign up (free)
2. Click **New → Web Service**
3. Connect your GitHub repo
4. Configure:
   - **Build Command:** `npm install`
   - **Start Command:** `npm start`
   - **Environment:** Node
5. Add environment variable:
   - Key: `ANTHROPIC_API_KEY`
   - Value: your Anthropic API key
6. Click **Deploy**

Render gives you a free URL like `https://swinglab.onrender.com` 🎉

---

## Deploy to the Web (Railway — Alternative)

1. Go to https://railway.app
2. New Project → Deploy from GitHub
3. Add `ANTHROPIC_API_KEY` environment variable
4. Done — Railway auto-detects Node.js

---

## How It Works

1. User uploads their swing video in the browser
2. Browser extracts 8 frames using the Canvas API (no upload needed for this step)
3. Frames are sent as base64 images to `/api/analyze` on your server
4. Your server securely forwards them to the Anthropic API with your hidden API key
5. Claude analyzes all 5 swing mechanics and returns scored feedback
6. Results displayed with scores, comparisons, and coaching tips

---

## API Cost Estimate

Each analysis call sends ~5 images + text to Claude.
Approximate cost: **$0.02–0.05 per analysis** depending on image sizes.

---

## Customization Ideas

- Add user accounts to save swing history
- Add more pro players for comparison
- Add slow-motion frame scrubbing
- Add email/PDF report export
- Add a leaderboard for teams
