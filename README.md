# Video Downloader - Clean Deployment Package

This folder contains ONLY the files you need to upload to GitHub for deployment.

## 📁 Files Included

### Core Files (Required)
- `server.js` - Main server file
- `database.js` - Database models
- `youtube-handler.js` - YouTube download handler
- `Dockerfile` - Docker configuration (installs yt-dlp & ffmpeg)
- `package.json` - Node.js dependencies
- `.gitignore` - Git ignore rules

### Frontend Files (Required)
- `index.html` - Homepage
- `admin.html` - Admin panel
- `login.html` - Admin login page
- `styles.css` - Styles
- `script.js` - Frontend JavaScript

### Data Folders (Required)
- `data/` - Stores settings and banner configurations
  - `settings.json` - Contact info and settings (persists across deployments)
  - `banners.json` - Banner configurations (persists across deployments)
- `images/banners/` - Upload your banner images here

## 🚀 Quick Deploy to Koyeb

### Step 1: Create New Repository
```bash
cd deploy
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
git push -u origin main
```

### Step 2: Deploy on Koyeb
1. Go to [Koyeb Dashboard](https://app.koyeb.com)
2. Click "Create Service"
3. Select "GitHub" and connect your repository
4. **Important:** Set Build Method to "Docker"
5. Click "Deploy"

### Step 3: Configure Admin
Default admin credentials:
- Username: `admin`
- Password: `admin123`

**⚠️ Change these in `server.js` lines 82-83:**
```javascript
const ADMIN_USER = "your_username";
const ADMIN_PASS = "your_password";
```

## 📝 Settings Persistence

### Problem Solved
Your banner and contact settings will now **persist across deployments**!

### How It Works
- Settings stored in `data/settings.json` (committed to Git)
- Banners stored in `data/banners.json` (committed to Git)
- Banner images stored in `images/banners/` (committed to Git)
- Frontend caches settings in localStorage (loads instantly < 1 second)

### Managing Storage
When `images/banners/` gets too large:
1. Go to GitHub repository
2. Navigate to `images/banners/`
3. Delete old banner images manually
4. Koyeb will auto-redeploy

## ⚡ Fast Loading (< 1 Second)

The frontend uses **localStorage caching**:
1. First load: Fetches from server
2. Subsequent loads: Instant from cache
3. Background update: Syncs with server

This means your banners and contact info appear **instantly** on page load!

## 🎨 Adding Banners

### Via Admin Panel
1. Login to `/admin.html`
2. Upload desktop (1200x400px) and mobile (600x400px) images
3. Images saved to `images/banners/`
4. Configuration saved to `data/banners.json`
5. Commit changes to Git to persist

### Manually
1. Upload images to `images/banners/` folder
2. Edit `data/banners.json`:
```json
{
  "desktopImage": "/images/banners/your-image.jpg",
  "mobileImage": "/images/banners/your-image-mobile.jpg",
  "link": "https://example.com",
  "duration": 5,
  "transition": "fade",
  "enabled": true
}
```
3. Commit and push to GitHub

## 🔧 Configuration

### Environment Variables (Optional)
Set these in Koyeb dashboard if using MongoDB/Cloudinary:

```
MONGODB_URI=mongodb+srv://...
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
```

### Without Environment Variables
The app works perfectly with file storage (no MongoDB/Cloudinary needed)!

## 📦 What's NOT Included

These files are NOT needed for deployment:
- ❌ `universal-downloader.js` - Not used
- ❌ `cobalt-downloader.js` - Not used
- ❌ `downloader-api.js` - Not used
- ❌ `install-ytdlp.js` - Not needed (Docker installs it)
- ❌ `render-build.sh` - Not needed (using Dockerfile)
- ❌ `render.yaml` - Not needed (using Dockerfile)
- ❌ `start.sh` - Not needed (using Dockerfile)
- ❌ All `.md` documentation files

## ✅ Supported Platforms

With Docker + yt-dlp, all platforms work:
- ✅ YouTube (all qualities + MP3)
- ✅ TikTok (HD, no watermark, original title)
- ✅ Instagram (reels, posts, stories, original title)
- ✅ Facebook (HD/SD, original title)
- ✅ Twitter/X (videos, original title)

## 🐛 Troubleshooting

### Banners not showing
1. Check `data/banners.json` exists
2. Check images exist in `images/banners/`
3. Clear browser cache (Ctrl+Shift+R)

### Settings reset after deployment
1. Make sure `data/` folder is committed to Git
2. Check `.gitignore` doesn't exclude `data/`
3. Commit changes after updating settings

### Downloads not working
1. Check Koyeb logs for errors
2. Verify Docker build completed successfully
3. Check yt-dlp is installed: `yt-dlp --version`

## 📞 Support

For issues, check:
1. Koyeb deployment logs
2. Browser console (F12)
3. Server logs in Koyeb dashboard

## 🎉 That's It!

This clean package has everything you need. Just:
1. Upload to GitHub
2. Deploy on Koyeb with Docker
3. Configure admin settings
4. Add your banners

Your settings will persist, and the frontend loads in < 1 second!
