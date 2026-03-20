# Vercel Frontend Deployment

This folder contains the frontend ready to deploy on Vercel with backend proxying.

## Setup Instructions

1. **Update `vercel.json`**
   - Replace `YOUR_ELASTIC_IP:PORT` with your actual Elastic IP and port
   - Example: `http://54.123.45.67:8000/api/:path*`

2. **Initialize Git Repository**
   ```bash
   cd demo/vercel-demo
   git init
   ```

3. **Create GitHub Repository**
   - Create a new repository on GitHub
   - Push this folder to that repository

4. **Deploy to Vercel**
   - Go to [vercel.com](https://vercel.com)
   - Click "Add New Project"
   - Select your GitHub repository
   - Vercel will automatically detect `vercel.json` and use the rewrite configuration
   - Click "Deploy"

5. **That's it!**
   - Your frontend will be live at `https://your-project.vercel.app`
   - All `/api/*` requests will be proxied to your EC2 backend
   - Browser sees everything as HTTPS (mixed content handled automatically)

## How It Works

- Browser requests `/api/training/narrative/1`
- Vercel receives the HTTPS request
- Vercel checks `vercel.json` rewrites
- Vercel forwards to `http://your-elastic-ip:8000/api/training/narrative/1`
- EC2 backend responds over HTTP
- Vercel returns response to browser as HTTPS
- No mixed content errors ✅

## Files Included

- `index.html` - Your frontend application
- `vercel.json` - Rewrite configuration for proxying to EC2
- `README.md` - This file

## Important Notes

- Your EC2 security group should allow inbound traffic on your backend port
- Ensure your FastAPI backend has CORS configured for `*.vercel.app`
- The rewrite happens server-side, so no changes to your HTML code are needed
