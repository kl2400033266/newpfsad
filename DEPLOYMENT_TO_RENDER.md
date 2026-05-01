# 🚀 Deploying PS04 to Render

## Step 1: Prepare Your Repository
```bash
git add .
git commit -m "Add Render deployment configuration"
git push
```

## Step 2: Create PostgreSQL Database on Render

1. Go to **[render.com](https://render.com)**
2. Click **New +** → **PostgreSQL**
3. Name: `ps04-db`
4. Region: Pick closest to you
5. Click **Create Database**
6. Copy the **Internal Database URL** (looks like: `postgresql://user:password@host:5432/dbname`)

## Step 3: Create Web Service on Render

1. Click **New +** → **Web Service**
2. Connect your GitHub repo `pfsad-re`
3. Settings:
   - **Name:** `ps04-dv-support`
   - **Runtime:** Python
   - **Build Command:** `pip install -r requirements.txt && python manage.py collectstatic --noinput && python manage.py migrate`
   - **Start Command:** `gunicorn dv_support.wsgi:application`
   - **Plan:** Free

## Step 4: Add Environment Variables

In Render dashboard, go to **Environment** and add:

```
DATABASE_URL=[paste your PostgreSQL URL]
SECRET_KEY=your-secret-key-here-make-it-long-and-random
DEBUG=false
ALLOWED_HOSTS=*.onrender.com
RENDER=true
```

**Generate a secret key:**
```bash
python -c "from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())"
```

## Step 5: Deploy

1. Click **Deploy**
2. Wait for build to complete (takes ~2-5 minutes)
3. Check logs if deployment fails
4. Access at: `https://your-service-name.onrender.com`

## ✅ Post-Deployment

After deployment succeeds:

1. Run migrations (if needed):
   ```bash
   # Via Render Shell or add to Build Command
   python manage.py migrate
   ```

2. Create admin user:
   ```bash
   python manage.py createsuperuser
   ```

3. Seed demo users:
   ```bash
   python manage.py seed_demo_users
   ```

## 🔧 Troubleshooting

- **500 Error:** Check Build Logs in Render dashboard
- **DATABASE_URL not working:** Ensure it's the Internal URL from Render
- **Static files not loading:** They're automatically handled by WhiteNoise
- **Migrations failing:** Add them to Build Command

---

**Your app will be live within minutes!** 🎉

Your live URL will be: `https://ps04-dv-support.onrender.com`
