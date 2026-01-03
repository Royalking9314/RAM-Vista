<div align="center">
<img width="1200" height="475" alt="GHBanner" src="https://github.com/user-attachments/assets/0aa67016-6eaf-458a-adb2-6e31a0763ed6" />
</div>

# Run and deploy your AI Studio app

This contains everything you need to run your app locally and deploy it to Cloudflare Pages.

View your app in AI Studio: https://ai.studio/apps/drive/1YHuRQZjH5cPenKuTS-UAMtbKuIX8Ph4E

## Run Locally

**Prerequisites:** Node.js

1. Install dependencies:
   ```bash
   npm install
   ```

2. Set up your environment variables:
   ```bash
   cp .env.example .env.local
   ```
   
3. Add your Gemini API key to `.env.local`:
   ```
   GEMINI_API_KEY=your_gemini_api_key_here
   ```
   Get your API key from: https://aistudio.google.com/apikey

4. Run the app:
   ```bash
   npm run dev
   ```

## Deployment to Cloudflare Pages

This project is configured to deploy to **Cloudflare Pages** (not Cloudflare Workers). There are two deployment methods available:

### Method 1: Git-based Deployment (Recommended)

This is the easiest method and provides automatic deployments on every push.

1. **Connect your repository to Cloudflare Pages:**
   - Log in to your [Cloudflare Dashboard](https://dash.cloudflare.com/)
   - Go to **Workers & Pages** → **Create application** → **Pages** → **Connect to Git**
   - Select your repository (`ram-vista`)
   - Configure the build settings:
     - **Build command:** `npm run build`
     - **Build output directory:** `dist`
     - **Root directory:** `/` (leave empty)
   
2. **Add environment variables in Cloudflare Dashboard:**
   - In your Pages project settings, go to **Settings** → **Environment variables**
   - Add `GEMINI_API_KEY` with your API key
   
3. **Deploy:**
   - Cloudflare will automatically build and deploy on every push to your main branch
   - You can also trigger manual deployments from the dashboard

**Advantages:**
- No local authentication required
- Automatic deployments on every push
- Built-in preview deployments for pull requests
- Easy rollback to previous deployments

### Method 2: CLI-based Deployment (Manual)

Use this method for manual deployments via command line.

1. **Install Wrangler globally (optional):**
   ```bash
   npm install -g wrangler
   ```

2. **Authenticate with Cloudflare:**
   ```bash
   npx wrangler login
   ```

3. **Build your application:**
   ```bash
   npm run build
   ```

4. **Deploy to Cloudflare Pages:**
   ```bash
   npm run pages:deploy
   ```

**Note:** The first deployment will create a new Pages project named `ram-vista`. Subsequent deployments will update the existing project.

## Project Structure

This is a **static React application** built with:
- **Vite** - Build tool and dev server
- **React** - UI framework
- **TypeScript** - Type safety
- **Cloudflare Pages** - Hosting platform

The build process compiles the React app into static files in the `dist/` directory, which are then deployed to Cloudflare Pages.

## Configuration Files

- `wrangler.toml` - Cloudflare Pages configuration
- `vite.config.ts` - Vite build configuration
- `.env.local` - Local environment variables (not committed)
- `.env.example` - Example environment variables template
