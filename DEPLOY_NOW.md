# 🚀 Deployment Instructions - GitHub ✅ | Render | Vercel

Your code has been pushed to GitHub successfully! Now deploy to Render and Vercel.

---

## ✅ STEP 1: GitHub - COMPLETED ✓

Code is now at: https://github.com/uditjoshi396/UDIT-JOSHI-POERTFOLIO

---

## 🚀 STEP 2: Deploy Backend to Render

### 2.1 Create MongoDB Atlas Connection String

If you haven't already:

1. Go to https://www.mongodb.com/cloud/atlas
2. Create cluster (M0 Free tier)
3. Create database user: `portfolio_user`
4. Copy connection string:

```
mongodb+srv://portfolio_user:PASSWORD@cluster.mongodb.net/udit_joshi?retryWrites=true&w=majority
```

**Replace PASSWORD with your actual password**

### 2.2 Deploy on Render

1. Go to https://render.com and sign up/log in
2. Click **"New +"** → **"Web Service"**
3. Click **"Connect GitHub"** and select `UDIT-JOSHI-POERTFOLIO`
4. Fill in:

| Field | Value |
| --- | --- |
| Name | `udit-joshi-api` |
| Environment | `Node` |
| Region | Choose closest region |
| Branch | `main` |
| Root Directory | `backend` |
| Build Command | `npm install` |
| Start Command | `npm start` |
| Plan | `Free` |

### 2.3 Add Environment Variables on Render

Click **"Advanced"** → **"Add Environment Variable"** for each:

```
NODE_ENV=production
MONGO_URI=mongodb+srv://portfolio_user:PASSWORD@cluster.mongodb.net/udit_joshi?retryWrites=true&w=majority
DB_NAME=udit_joshi
JWT_SECRET=generate-a-strong-32-char-secret-key-here
JWT_EXPIRES_IN=7d
CLIENT_URL=https://your-vercel-url.vercel.app
CLOUDINARY_CLOUD_NAME=optional
CLOUDINARY_API_KEY=optional
CLOUDINARY_API_SECRET=optional
STRIPE_SECRET_KEY=optional
```

**IMPORTANT: Replace these values:**
- `PASSWORD` → Your MongoDB password
- `JWT_SECRET` → A unique strong 32+ character password
- `CLIENT_URL` → Your Vercel URL (after step 3)

### 2.4 Deploy

1. Click **"Create Web Service"**
2. Wait 3-5 minutes for deployment
3. Copy your Backend URL when ready (looks like: `https://udit-joshi-api.onrender.com`)
4. **SAVE THIS URL** - you'll need it for frontend

### 2.5 Test Backend

Open: `https://udit-joshi-api.onrender.com/api/health`

Should show: `{"status":"ok"}`

---

## 🎨 STEP 3: Deploy Frontend to Vercel

### 3.1 Create Frontend Environment File

The repository already has `.env.example` for frontend. Create `.env.production`:

```
VITE_API_URL=https://udit-joshi-api.onrender.com/api
```

(Use your actual Render URL from Step 2.4)

OR commit this to git:

```bash
cd frontend
echo "VITE_API_URL=https://udit-joshi-api.onrender.com/api" > .env.production
git add .env.production
git commit -m "Add production env"
git push
```

### 3.2 Deploy on Vercel

1. Go to https://vercel.com and sign up/log in with GitHub
2. Click **"Add New"** → **"Project"**
3. Click **"Import GitHub Repository"**
4. Select `UDIT-JOSHI-POERTFOLIO`
5. Configure:

| Field | Value |
| --- | --- |
| Framework | `Vite` |
| Root Directory | `frontend` |
| Build Command | `npm run build` |
| Output Directory | `dist` |
| Environment Variables | (See below) |

### 3.3 Add Environment Variables

Add this environment variable:

```
VITE_API_URL=https://udit-joshi-api.onrender.com/api
```

### 3.4 Deploy

1. Click **"Deploy"**
2. Wait 2-3 minutes
3. Copy your Vercel URL when ready (looks like: `https://udit-joshi-portfolio.vercel.app`)
4. **SAVE THIS URL**

### 3.5 Test Frontend

Open your Vercel URL: `https://udit-joshi-portfolio.vercel.app`

Should load your portfolio!

---

## 🔄 STEP 4: Update Backend with Frontend URL

### 4.1 Update Render Environment

1. Go to https://render.com
2. Select your `udit-joshi-api` service
3. Click **"Environment"**
4. Edit `CLIENT_URL`:

```
https://udit-joshi-portfolio.vercel.app
```

5. Click **"Save Changes"**
6. Render will auto-redeploy (1-2 minutes)

---

## ✅ STEP 5: Verify Deployment

### 5.1 Test All Features

Frontend:
- [ ] Open `https://udit-joshi-portfolio.vercel.app`
- [ ] All pages load
- [ ] Images display
- [ ] Mobile responsive

Backend:
- [ ] Open `https://udit-joshi-api.onrender.com/api/health` → `{"status":"ok"}`
- [ ] Admin Dashboard loads
- [ ] Can create projects (with JWT token)

---

## 🆘 Troubleshooting

### 502 Bad Gateway on Render?
- Check Render logs for errors
- Verify `MONGO_URI` is correct
- Ensure all environment variables are set

### CORS errors in browser?
- Verify `CLIENT_URL` on Render is correct
- Check that backend URL in frontend matches Render URL

### Frontend can't connect to backend?
- Check `VITE_API_URL` in frontend environment
- Ensure Render backend URL is correct and active

### Database connection error?
- Verify MongoDB credentials
- Check IP whitelist on MongoDB Atlas (allow anywhere)
- Test connection string locally

---

## 📝 Summary

| Service | URL | Status |
| --- | --- | --- |
| GitHub | https://github.com/uditjoshi396/UDIT-JOSHI-POERTFOLIO | ✅ Done |
| Render Backend | https://udit-joshi-api.onrender.com | ⏳ Deploy now |
| Vercel Frontend | https://udit-joshi-portfolio.vercel.app | ⏳ Deploy now |

---

## 🎯 Next Steps

1. **Deploy Backend on Render** (sections 2.1-2.5)
2. **Deploy Frontend on Vercel** (sections 3.1-3.5)
3. **Update Backend Client URL** (section 4.1)
4. **Verify Everything Works** (section 5.1)

**Total time: 15-20 minutes**

Good luck! 🚀
