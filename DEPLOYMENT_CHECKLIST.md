# 🚀 Quick Deployment Checklist

Time: 45-60 minutes

---

## Phase 1: Local Verification (5 min)

```bash
☐ cd backend && npm install
☐ npm run seed (creates admin user)
☐ npm start (backend running on 5000)
☐ Test: http://localhost:5000/api/health

☐ cd frontend && npm install
☐ npm run dev (frontend running on 5173)
☐ Test: http://localhost:5173
```

Admin Test Login:

- Email: `admin@uditjoshi.com`
- Password: `Admin@123`

---

## Phase 2: MongoDB Atlas Setup (10 min)

```bash
☐ Create MongoDB account
☐ Create project "udit-joshi-portfolio"
☐ Build cluster (M0 Free tier)
☐ Create database user:
   - Username: portfolio_user
   - Password: [Generate & save]
   - Role: Atlas admin

☐ Allow access from anywhere (Network Access)
☐ Get connection string
☐ SAVE THIS URL - needed multiple times
```

---

## Phase 3: Push to GitHub (5 min)

```bash
☐ git init
☐ git add .
☐ git commit -m "Initial commit"
☐ git branch -M main
☐ git remote add origin https://github.com/YOUR_USERNAME/UDIT-JOSHI-PORTFOLIO.git
☐ git push -u origin main
```

---

## Phase 4: Deploy Backend to Render (15 min)

```bash
☐ Create Render account
☐ New Web Service → Connect GitHub repo
☐ Configuration:
   - Name: udit-joshi-api
   - Environment: Node
   - Root Directory: backend
   - Build: npm install
   - Start: npm start

☐ Add Environment Variables:
   NODE_ENV = production
   MONGO_URI = [Your MongoDB connection string]
   DB_NAME = udit_joshi
   JWT_SECRET = [Min 32 chars - generate something strong]
   JWT_EXPIRES_IN = 7d
   CLIENT_URL = [Update after frontend deployment]

☐ Deploy
☐ Wait for completion (3-5 min)
☐ SAVE BACKEND URL: https://udit-joshi-api.onrender.com
```

---

## Phase 5: Deploy Frontend to Vercel (10 min)

```bash
☐ Create Vercel account
☐ Add Project → Import GitHub repo
☐ Configuration:
   - Project: udit-joshi-portfolio
   - Framework: Vite
   - Root Directory: frontend
   - Build: npm run build
   - Output: dist

☐ Environment Variable:
   VITE_API_URL = [Your Render backend URL]/api

☐ Deploy
☐ Wait for completion (2-3 min)
☐ SAVE FRONTEND URL: https://udit-joshi-portfolio.vercel.app
```

---

## Phase 6: Update Backend CLIENT_URL (3 min)

```bash
☐ Go to Render dashboard
☐ Select udit-joshi-api service
☐ Edit CLIENT_URL environment variable:
   CLIENT_URL = https://udit-joshi-portfolio.vercel.app

☐ Save (Render auto-redeploys)
☐ Wait 1-2 min for redeploy
```

---

## Phase 7: Verify Deployment (10 min)

Frontend Tests:

- [ ] Open frontend URL - loads without errors
- [ ] All pages accessible
- [ ] Images display
- [ ] Mobile responsive

Backend Tests:

- [ ] Open Render health endpoint (see Troubleshooting section for URL)
- [ ] Should show: `{"status":"ok"}`

Integration Tests:

- [ ] Admin Dashboard loads
- [ ] Create project works (with JWT)
- [ ] Projects display correctly
- [ ] No CORS errors in console

---

## Phase 8: Optional - Add More Services (10 min each)

### Cloudinary (Image Uploads)

```bash
☐ Create Cloudinary account
☐ Get credentials (Cloud Name, API Key, Secret)
☐ Add to Render environment variables:
   CLOUDINARY_CLOUD_NAME = [your-cloud-name]
   CLOUDINARY_API_KEY = [your-api-key]
   CLOUDINARY_API_SECRET = [your-api-secret]
```

### Stripe (Payments)

```bash
☐ Create Stripe account
☐ Get Secret Key from API keys
☐ Add to Render environment:
   STRIPE_SECRET_KEY = sk_live_...
```

### Custom Domain

```bash
☐ Buy domain (Namecheap, GoDaddy, etc)

For Vercel:
☐ Settings → Domains → Add domain
☐ Follow DNS instructions

For Render:
☐ Service Settings → Custom Domain
☐ Follow DNS instructions
```

---

## 🔑 Important Credentials to Save

| Service | Value |
| --- | --- |
| MongoDB Connection String | `mongodb+srv://...` |
| Render Backend URL | `https://udit-joshi-api.onrender.com` |
| Vercel Frontend URL | `https://udit-joshi-portfolio.vercel.app` |
| JWT Secret | 32+ char secret |
| MongoDB Password | portfolio_user password |

Never commit credentials to GitHub

---

## ✅ Post-Deployment

```bash
☐ Test all features work
☐ Check Render logs for errors
☐ Monitor uptime
☐ Set up alerts
☐ Share portfolio link
```

---

## 🆘 Quick Troubleshooting

502 Bad Gateway?

- Check Render logs for errors
- Verify MongoDB connection string
- Ensure all env vars are set

CORS Error?

- Update CLIENT_URL on Render
- Restart backend (redeploy)

Frontend can't reach backend?

- Check VITE_API_URL is correct
- Verify backend URL is working

Database connection error?

- Check MONGO_URI format
- Verify credentials
- Check IP whitelist on MongoDB Atlas
- Test connection locally first

---

See DEPLOYMENT_GUIDE.md for detailed instructions
