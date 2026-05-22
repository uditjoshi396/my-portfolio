# 🚀 Complete Deployment Guide - Udit Joshi Portfolio

This guide covers deploying your MERN stack portfolio to production using **Vercel** (frontend), **Render** (backend), and **MongoDB Atlas** (database).

---

## 📋 Prerequisites & Accounts Required

Before starting, create free accounts on:

- [Vercel](https://vercel.com) - Frontend hosting
- [Render](https://render.com) - Backend hosting
- [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) - Cloud database
- [Cloudinary](https://cloudinary.com) - Image storage (optional but recommended)
- [GitHub](https://github.com) - For version control

---

## ✅ Phase 1: Local Verification (5-10 minutes)

Before deploying, ensure your project runs locally:

### 1.1 Backend Setup

```bash
cd backend
cp .env.example .env
npm install
npm run seed
npm start
```

Verify backend is running:

- Open `http://localhost:5000/api/health`
- Should show `{"status":"ok"}`

### 1.2 Frontend Setup

```bash
cd frontend
npm install
npm run dev
```

Verify frontend is running:

- Open `http://localhost:5173`
- Should load your portfolio

---

## 🗄️ Phase 2: Set Up MongoDB Atlas (10 minutes)

### 2.1 Create MongoDB Project

1. Log in to [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Click **"Create a new project"** → Name: `udit-joshi-portfolio`
3. Click **"Create Project"**

### 2.2 Create a Cluster

1. Click **"Build a Cluster"**
2. Select **M0 (Free)** tier
3. Choose your region (pick closest to your deployment)
4. Click **"Create Deployment"**
5. Wait 2-3 minutes for cluster creation

### 2.3 Set Up Database Access

1. Go to **Database Access** → **"Add New Database User"**
2. Fill in:
   - **Username**: `portfolio_user`
   - **Password**: Generate secure password (copy it!)
   - **Built-in Role**: `Atlas admin`
3. Click **"Add User"**

### 2.4 Set Up Network Access

1. Go to **Network Access** → **"Add IP Address"**
2. Click **"Allow Access from Anywhere"** (for now)
   - This allows connections from any IP
3. Click **"Confirm"**

### 2.5 Get Connection String

1. Go to **Clusters** → Click **"Connect"**
2. Select **"Drivers"** → **Node.js**
3. Copy the connection string (looks like):

```text
mongodb+srv://portfolio_user:PASSWORD@cluster.mongodb.net/DATABASE_NAME?retryWrites=true&w=majority
```

1. Replace:
   - `PASSWORD` → your actual password from step 2.3
   - `DATABASE_NAME` → `udit_joshi`

**Save this connection string** - you'll need it multiple times!

---

## ☁️ Phase 3: Deploy Backend to Render (15-20 minutes)

### 3.1 Push Code to GitHub

```bash
git init
git add .
git commit -m "Initial commit: MERN portfolio"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/UDIT-JOSHI-PORTFOLIO.git
git push -u origin main
```

Replace `YOUR_USERNAME` with your GitHub username.

### 3.2 Create Render Web Service

1. Log in to [Render](https://render.com)
2. Click **"New +"** → **"Web Service"**
3. **Connect Repository**:
   - Click **"Connect GitHub"**
   - Select your `UDIT-JOSHI-PORTFOLIO` repo
   - Click **"Connect"**

### 3.3 Configure Render Deployment

Fill in the form:

| Field | Value |
| --- | --- |
| **Name** | `udit-joshi-api` |
| **Environment** | `Node` |
| **Region** | Choose closest to you |
| **Branch** | `main` |
| **Root Directory** | `backend` |
| **Build Command** | `npm install` |
| **Start Command** | `npm start` |
| **Plan** | `Free` |

### 3.4 Add Environment Variables

Click **"Add Environment Variable"** and add these one by one:

```bash
NODE_ENV=production
MONGO_URI=mongodb+srv://portfolio_user:PASSWORD@cluster.mongodb.net/udit_joshi?retryWrites=true&w=majority
DB_NAME=udit_joshi
JWT_SECRET=your-super-secret-jwt-key-min-32-chars
JWT_EXPIRES_IN=7d
CLIENT_URL=https://your-vercel-domain.vercel.app
CLOUDINARY_CLOUD_NAME=optional-leave-empty
CLOUDINARY_API_KEY=optional-leave-empty
CLOUDINARY_API_SECRET=optional-leave-empty
STRIPE_SECRET_KEY=optional-leave-empty
```

**Important**: Use a strong JWT_SECRET (at least 32 characters)

### 3.5 Deploy

1. Click **"Create Web Service"**
2. Wait for deployment (3-5 minutes)
3. Once done, copy your backend URL (e.g., `https://udit-joshi-api.onrender.com`)
4. **Save this URL** - needed for frontend

---

## 🎨 Phase 4: Deploy Frontend to Vercel (10-15 minutes)

### 4.1 Update Backend URL in Frontend

Edit `frontend/.env.production`:

```bash
VITE_API_URL=https://udit-joshi-api.onrender.com/api
```

Push to GitHub:

```bash
git add .
git commit -m "Update backend URL for production"
git push
```

### 4.2 Deploy on Vercel

1. Go to [Vercel](https://vercel.com) → **"Add New"** → **"Project"**
2. **Import Git Repository**:
   - Click **"Import GitHub Repository"**
   - Select `UDIT-JOSHI-PORTFOLIO`
   - Click **"Import"**

### 4.3 Configure Vercel

Fill in the configuration:

| Field | Value |
| --- | --- |
| **Project Name** | `udit-joshi-portfolio` |
| **Framework** | `Vite` |
| **Root Directory** | `frontend` |
| **Build Command** | `npm run build` |
| **Output Directory** | `dist` |

### 4.4 Add Environment Variables

Click **"Environment Variables"** → Add:

```bash
VITE_API_URL=https://udit-joshi-api.onrender.com/api
```

### 4.5 Deploy

1. Click **"Deploy"**
2. Wait 2-3 minutes for deployment
3. Copy your Vercel URL (e.g., `https://udit-joshi-portfolio.vercel.app`)

---

## 🔄 Phase 5: Update Cross-Origin URLs (5 minutes)

### 5.1 Update Backend Environment Variable

Go back to **Render** dashboard:

1. Select your `udit-joshi-api` service
2. Go to **"Environment"** tab
3. Edit `CLIENT_URL` environment variable:

```bash
CLIENT_URL=https://udit-joshi-portfolio.vercel.app
```

1. Click **"Save Changes"**
2. Render will auto-redeploy (takes 1-2 minutes)

### 5.2 Verify CORS

- Open your Vercel frontend URL
- Go to **"Admin Dashboard"**
- Test creating a project (should work without CORS errors)

---

## ✨ Phase 6: Verify Full Deployment (10 minutes)

### 6.1 Test Frontend

- [ ] Open `https://your-frontend.vercel.app`
- [ ] All pages load
- [ ] Images display correctly
- [ ] Scroll and animations work

### 6.2 Test Backend Connectivity

- [ ] Go to **Admin Dashboard**
- [ ] API calls should work without errors
- [ ] Try creating a project (requires JWT token from earlier setup)

### 6.3 Test Key Features

- [ ] Contact form sends (if configured)
- [ ] Projects load and display
- [ ] Search/filter works
- [ ] Responsive on mobile

### 6.4 Check API Health

- Open `https://your-backend.onrender.com/api/health`
- Should return: `{"status":"ok"}`

---

## 🔒 Phase 7: Optional Enhancements

### 7.1 Add Cloudinary (Image Uploads)

1. Sign up at [Cloudinary](https://cloudinary.com)
2. Get credentials from **Dashboard**
3. Update environment variables on Render:

```bash
CLOUDINARY_CLOUD_NAME=your-cloud-name
CLOUDINARY_API_KEY=your-api-key
CLOUDINARY_API_SECRET=your-api-secret
```

### 7.2 Add Stripe (Payments)

1. Sign up at [Stripe](https://stripe.com)
2. Get **Secret Key** from API keys
3. Add to Render environment:

```bash
STRIPE_SECRET_KEY=sk_live_...
```

### 7.3 Custom Domain

**For Vercel:**

1. Buy domain at [Namecheap](https://namecheap.com) or similar
2. Go to Vercel → **Settings** → **Domains**
3. Add your domain and follow DNS instructions

**For Render:**

1. Go to Render service → **Settings** → **Custom Domain**
2. Add domain and configure DNS

---

## 🆘 Troubleshooting

### Issue: 502 Bad Gateway on Render

**Solution**: Check Render logs

- Go to Render → Your service → **"Logs"**
- Look for error messages
- Usually: missing environment variable or database connection

### Issue: CORS errors in browser

**Solution**:

- Verify `CLIENT_URL` is correct on Render
- Include trailing slash if needed
- Check backend logs for CORS warnings

### Issue: Frontend can't connect to backend

**Solution**:

- Update `VITE_API_URL` in frontend `.env`
- Ensure Render backend URL is correct
- Check if backend is running at the correct URL

### Issue: Database connection timeout

**Solution**:

- Verify MongoDB credentials in `MONGO_URI`
- Check IP whitelist on MongoDB Atlas (should allow anywhere for free tier)
- Test connection string locally first

---

## 📊 After Deployment Checklist

- [ ] Frontend loads on Vercel
- [ ] Backend API responds on Render
- [ ] Database connects successfully
- [ ] Admin dashboard works
- [ ] Projects display
- [ ] Contact form works (if configured)
- [ ] No CORS errors in console
- [ ] Mobile responsive
- [ ] All images load
- [ ] Performance is acceptable

---

## 🚨 Important Notes

1. **Free Tier Limitations**:
   - Render spins down after 15 min of inactivity (first request takes 30 sec)
   - MongoDB Atlas free tier has storage limits
   - Upgrade if needed for production

2. **Security**:
   - Never commit `.env` files to GitHub
   - Change `JWT_SECRET` to something unique
   - Enable 2FA on all cloud accounts

3. **Monitoring**:
   - Set up email alerts on all platforms
   - Monitor Render logs regularly
   - Check MongoDB Atlas metrics

---

## 📚 Useful Links

- [Render Documentation](https://render.com/docs)
- [Vercel Documentation](https://vercel.com/docs)
- [MongoDB Atlas Documentation](https://docs.atlas.mongodb.com)
- [Express Deployment Best Practices](https://expressjs.com/en/advanced/best-practice-performance.html)

---

**Estimated Total Time**: 45-60 minutes ⏱️
