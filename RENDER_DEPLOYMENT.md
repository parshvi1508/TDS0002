# Deploy to Render - Step by Step Guide

## Prerequisites
- A Render account (free at https://render.com)
- Your project code ready (which you have!)

## Step 1: Prepare Your Environment Variables

Before deploying, you'll need to set up your Gemini API keys. In your Render dashboard:

1. Go to your service settings
2. Navigate to "Environment" tab
3. Add these environment variables:

```
gemini_api_1=your_first_gemini_api_key
gemini_api_2=your_second_gemini_api_key
gemini_api_3=your_third_gemini_api_key
# ... add up to 10 keys as needed
GOOGLE_MODEL=gemini-2.5-pro
LLM_TIMEOUT_SECONDS=240
```

## Step 2: Deploy to Render

### Option A: Using GitHub (Recommended)
1. Push your code to a GitHub repository
2. Go to [Render Dashboard](https://dashboard.render.com)
3. Click "New +" → "Web Service"
4. Connect your GitHub account
5. Select your repository
6. Render will auto-detect it's a Python app
7. Configure:
   - **Name**: `tds-data-analyst-agent` (or any name you prefer)
   - **Environment**: `Python`
   - **Build Command**: `pip install -r requirements.txt`
   - **Start Command**: `uvicorn app:app --host 0.0.0.0 --port $PORT`
   - **Plan**: Free (or paid if you need more resources)

### Option B: Using render.yaml (Blue-Green Deployment)
1. Push your code with the `render.yaml` file to GitHub
2. In Render dashboard, click "New +" → "Blueprint"
3. Connect your repository
4. Render will use the `render.yaml` configuration automatically

## Step 3: Environment Variables Setup

After creating the service, add your environment variables:

1. Go to your service dashboard
2. Click "Environment" tab
3. Add your Gemini API keys:
   ```
   gemini_api_1=your_api_key_here
   gemini_api_2=your_backup_key_here
   # ... add more as needed
   ```

## Step 4: Deploy

1. Click "Create Web Service"
2. Render will automatically:
   - Build your application
   - Install dependencies
   - Start the service
3. Your app will be available at: `https://your-app-name.onrender.com`

## Step 5: Verify Deployment

1. Visit your app URL
2. Test the `/summary` endpoint: `https://your-app-name.onrender.com/summary`
3. This will show you system diagnostics and confirm everything is working

## Troubleshooting

### Common Issues:

1. **Build Failures**: Check the build logs in Render dashboard
2. **Environment Variables**: Ensure all Gemini API keys are set
3. **Port Issues**: The app uses `$PORT` environment variable (Render sets this automatically)
4. **Memory Issues**: Free tier has 512MB RAM limit - consider upgrading if needed

### Useful Commands:
- Check logs: Render dashboard → Logs tab
- Restart service: Render dashboard → Manual Deploy
- Environment variables: Render dashboard → Environment tab

## Monitoring

- **Health Check**: Visit `/summary` endpoint for system diagnostics
- **Logs**: Available in Render dashboard
- **Metrics**: Basic metrics available in free tier

## Cost

- **Free Tier**: $0/month (with limitations)
- **Paid Plans**: Start at $7/month for more resources

Your app is now ready to be deployed! 🚀
