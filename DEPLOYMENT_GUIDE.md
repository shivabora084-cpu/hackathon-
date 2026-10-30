# LinguaMate AI - Production Deployment Guide

This guide covers deploying the frontend to **Vercel** and the backend to **Render**.

---

## 1. Backend Deployment to Render

1. Log into your [Render Dashboard](https://dashboard.render.com/).
2. Click **New +** and select **Web Service**.
3. Connect your GitHub repository containing LinguaMate AI.
4. Configure the Web Service settings:
   - **Name**: `linguamate-backend`
   - **Root Directory**: `backend`
   - **Environment**: `Node`
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`
   - **Health Check Path**: `/api/health`
5. Under **Environment Variables**, add the following private secrets:
   ```env
   NODE_ENV=production
   PORT=10000
   FRONTEND_URL=https://your-frontend.vercel.app
   SUPABASE_URL=https://your-project.supabase.co
   SUPABASE_ANON_KEY=your_supabase_anon_key
   SUPABASE_SERVICE_ROLE_KEY=your_service_role_key
   GEMINI_API_KEY=your_gemini_api_key
   AI_MODEL=gemini-1.5-flash
   JWT_SECRET=your_long_random_jwt_secret_key_at_least_32_chars
   JWT_EXPIRES_IN=7d
   STORAGE_BUCKET=linguamate-files
   STT_PROVIDER=browser
   TTS_PROVIDER=browser
   ```
6. Click **Create Web Service**.
7. Once deployed, test your public health endpoint in your browser:
   `https://linguamate-backend.onrender.com/api/health`

---

## 2. Frontend Deployment to Vercel

1. Log into your [Vercel Dashboard](https://vercel.com/).
2. Click **Add New...** → **Project**.
3. Import your GitHub repository.
4. In the Project Configuration:
   - **Framework Preset**: `Vite`
   - **Root Directory**: Click edit and select `frontend`
   - **Build Command**: `npm run build`
   - **Output Directory**: `dist`
5. Under **Environment Variables**, add:
   ```env
   VITE_API_BASE_URL=https://linguamate-backend.onrender.com/api
   ```
6. Click **Deploy**.
7. Once deployed, open your Vercel URL and update `FRONTEND_URL` on Render to match your Vercel domain to configure CORS properly.

---

## 3. Database & Storage Deployment (Supabase)

1. Open your [Supabase Dashboard](https://supabase.com/dashboard).
2. Select your project and navigate to the **SQL Editor**.
3. Copy and paste the entire contents of `backend/database/schema.sql` and click **Run**.
4. Confirm:
   - All 12 tables appear under the **Table Editor**.
   - The bucket `linguamate-files` appears under **Storage**.
   - `pgvector` extension is active.
