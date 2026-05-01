# PS04 Complete Deployment Checklist

## 📦 Files Ready for Deployment

All files are properly configured for Render deployment:

✅ **render.yaml** - Render deployment configuration (auto-deploy from GitHub)
✅ **runtime.txt** - Python version specification (3.11.9)
✅ **Procfile** - Web process definition for Render
✅ **requirements.txt** - All Python dependencies
✅ **.gitignore** - Prevents sensitive files from committing
✅ **DEPLOYMENT_TO_RENDER.md** - Step-by-step deployment guide
✅ **.env.example** - Environment variables template
✅ **dv_support/settings.py** - Production-ready Django config

---

## 🚀 Quick Start (3 Steps)

### Step 1: Clone verification
```bash
# Your repo is ready
# URL: https://github.com/k12400033266/pfsad-re.git
```

### Step 2: Create PostgreSQL on Render
- Go to https://render.com
- New + → PostgreSQL
- Name: ps04-db
- **Copy the Internal Database URL** 🔑

### Step 3: Deploy Web Service
- New + → Web Service
- Connect your GitHub repo (pfsad-re)
- **Render will auto-detect** render.yaml
- Add environment variables (see .env.example)
- Click Deploy ✨

---

## 📋 Required Environment Variables

Add these in Render Dashboard under "Environment":

```
SECRET_KEY=<generated-key>
DATABASE_URL=<from-postgresql>
DEBUG=false
RENDER=true
ALLOWED_HOSTS=your-app-name.onrender.com
CSRF_TRUSTED_ORIGINS=https://*.onrender.com
```

---

## 🔧 File-by-File Breakdown

### render.yaml
- **Location:** Root directory
- **Purpose:** Main Render configuration
- **Auto-deploys:** When you push to GitHub
- **Does:** Installs deps, runs migrations, collects static files

### runtime.txt
- **Location:** Root directory
- **Purpose:** Specifies Python version
- **Value:** python-3.11.9
- **Why:** Ensures compatibility

### Procfile
- **Location:** Root directory
- **Purpose:** Defines startup command
- **Command:** `gunicorn dv_support.wsgi`
- **Why:** Tells Render how to run your app

### requirements.txt
- **Location:** Root directory
- **Current contents:**
  - Django==6.0.2
  - gunicorn==25.1.0
  - psycopg2-binary==2.9.11
  - whitenoise==6.11.0
  - (and 4 more)
- **Why:** Tells pip what to install

### .gitignore (ENHANCED)
- **Location:** Root directory
- **Ignores:**
  - Virtual environments
  - SQLite database
  - Python bytecode
  - IDE files
  - .env files
- **Why:** Prevents committing sensitive/unnecessary files

### dv_support/settings.py
- **Already configured for:**
  - WhiteNoise static files
  - PostgreSQL database
  - Render environment variables
  - Security headers
  - CORS settings
- **No changes needed**

### .env.example
- **Location:** Root directory
- **Purpose:** Template for environment variables
- **Includes:** All required vars with descriptions
- **How to use:** Copy values and add to Render dashboard

---

## ✅ Pre-Deployment Checklist

- [x] render.yaml in root
- [x] runtime.txt in root
- [x] Procfile in root
- [x] requirements.txt populated
- [x] .gitignore configured
- [x] settings.py production-ready
- [x] .env.example created
- [x] All files committed to GitHub
- [x] GitHub repo accessible

---

## 🚨 Common Issues & Fixes

### Issue: "404 Not Found"
**Cause:** Render can't find your app
**Fix:** Check ALLOWED_HOSTS in environment variables

### Issue: "Error R10 (Boot timeout)"
**Cause:** App taking too long to start
**Fix:** Check if migrations are failing in Build Logs

### Issue: "Database connection refused"
**Cause:** Wrong DATABASE_URL
**Fix:** Use INTERNAL URL from Render PostgreSQL, not External

### Issue: "ModuleNotFoundError"
**Cause:** Package not in requirements.txt
**Fix:** Check requirements.txt is in repo

### Issue: "Static files not loading"
**Cause:** collectstatic failed
**Fix:** WhiteNoise handles it, check if CSS/JS paths are correct in templates

---

## 📊 What Happens During Deployment

1. **Build Phase:**
   ```
   pip install -r requirements.txt
   python manage.py collectstatic --noinput
   python manage.py migrate
   ```

2. **Runtime Phase:**
   ```
   gunicorn dv_support.wsgi:application --bind 0.0.0.0:$PORT
   ```

3. **Auto-assign URL:**
   ```
   https://ps04-dv-support.onrender.com
   ```

---

## 🔐 Security Notes

1. **SECRET_KEY** - Generated randomly, never commit
2. **DATABASE_URL** - Use INTERNAL URL on Render (stays private)
3. **DEBUG=false** - Never use true in production
4. **ALLOWED_HOSTS** - Restricts who can access
5. **CSRF_TRUSTED_ORIGINS** - Protects against CSRF attacks

---

## 📱 Demo Accounts

After deployment succeeds, test with:

| Role | Username | Password |
|------|----------|----------|
| Admin | Mohan | Mohan2006@ |
| Survivor | raju | common |
| Counsellor | Karthik | common |
| Legal Advisor | nakul | common |

---

## 🎉 Success Indicators

✅ Build logs show "Deployed successfully"
✅ URL is accessible without 404
✅ Database migrations completed
✅ Static files load (CSS/images visible)
✅ Can login with demo accounts
✅ Dashboards display data

---

## 📞 Need Help?

- Check Render Logs: View in Dashboard → Logs
- Check Build Logs: During deployment
- Check Django Logs: Should print to stdout
- Verify: All env vars are set correctly

---

**Your app is deployment-ready! 🚀**

Ready to deploy? Go to: https://render.com
