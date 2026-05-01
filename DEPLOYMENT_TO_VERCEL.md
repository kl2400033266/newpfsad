# 🚀 Deploy to Vercel (Frontend)

## Architecture

```
┌─────────────────────────────────────────────────────┐
│  Vercel (Frontend - This Site)                      │
│  - index.html (landing page)                        │
│  - Static files                                     │
│  └─> Links to Live App on Render                   │
└──────────────────────┬───────────────────────────────┘
                       │ API Calls
                       ▼
┌─────────────────────────────────────────────────────┐
│  Render (Backend - Live App)                        │
│  - Django API                                       │
│  - PostgreSQL Database                              │
│  - Demo Accounts & Data                             │
└─────────────────────────────────────────────────────┘
```

---

## 📋 Vercel Deployment Steps

### Step 1: Connect GitHub to Vercel

1. Go to: **https://vercel.com**
2. Click: **"Add New" → "Project"**
3. Select: **"Import Git Repository"**
4. Paste: `https://github.com/kl2400033266/newpfsad`
5. Click: **"Import"**

### Step 2: Configure Project

Vercel should auto-detect the settings:
- **Project Name:** ps04-dv-support-frontend
- **Framework:** Other → Static
- **Build Command:** (leave blank)
- **Output Directory:** public
- **Root Directory:** ./

✅ If auto-detection works, you're good to go!

### Step 3: Deploy

1. Click: **"Deploy"**
2. Wait 30-60 seconds
3. Your site is live! 🎉

---

## 🔗 Your Vercel URL

After deployment, Vercel gives you:
```
https://newpfsad.vercel.app
```

You can also create a custom domain!

---

## 📁 What Vercel Deploys

From the `public/` folder:
- ✅ `index.html` - Landing page with demo credentials
- ✅ Links to live Render Django app
- ✅ Demo account information
- ✅ Technical documentation

---

## 🔄 Automatic Redeploys

Every time you push to GitHub:
```bash
git add .
git commit -m "your message"
git push
```

Vercel automatically redeploys your frontend! ✨

---

## ✏️ Edit & Update

To update the landing page:

1. Edit `/public/index.html`
2. Commit and push:
   ```bash
   git add public/index.html
   git commit -m "Update landing page"
   git push
   ```
3. Vercel redeploys automatically (takes ~30 seconds)

---

## 🌐 Linking Frontend & Backend

The frontend (`public/index.html`) links to:
```
https://ps04-dv-support.onrender.com
```

This is your Django app on Render. Make sure:
- [ ] Django app is deployed on Render
- [ ] PostgreSQL is created and connected
- [ ] Environment variables are set
- [ ] Backend is running (check status)

---

## 🎯 Final Setup Checklist

- [ ] GitHub repo exists: `newpfsad`
- [ ] `public/index.html` created
- [ ] `vercel.json` in root
- [ ] Connect GitHub to Vercel account
- [ ] Deploy from Vercel dashboard
- [ ] Verify site is live
- [ ] Test links to Render backend

---

## 😄 You Now Have:

✅ **Frontend on Vercel:**
```
https://newpfsad.vercel.app (or custom domain)
```

✅ **Backend on Render:**
```
https://ps04-dv-support.onrender.com
```

✅ **Database on Render:**
```
PostgreSQL (private)
```

---

## 📊 Production URLs

| Component | URL | Status |
|-----------|-----|--------|
| Frontend | https://newpfsad.vercel.app | Vercel |
| Backend | https://ps04-dv-support.onrender.com | Render |
| Database | PostgreSQL (Render) | Private |
| GitHub | github.com/kl2400033266/newpfsad | Source |

---

## 🆘 Troubleshooting

### "404 Not Found"
- Ensure `public/index.html` exists
- Check `vercel.json` configuration
- Restart deployment

### "Links not working"
- Make sure Render backend is running
- Check URL in `index.html`
- Verify PostgreSQL connection

### "Changes not deploying"
- Check if you pushed to GitHub
- Vercel automatically redeploys
- Wait 30-60 seconds
- Check Deployment Logs in Vercel dashboard

---

## 🎉 Success!

Your PS04 app is now:
- 📍 Frontend hosted on **Vercel** (this landing page)
- 🔌 Backend running on **Render** (live Django app)
- 🌍 Globally accessible and fast

**Both services are production-ready and free-tier eligible!**
