# 🚀 Hydrogen Storefront Deployment Guide

## Current Status
✅ **Build Complete**: Your Hydrogen storefront has been successfully built for production
✅ **Environment Configured**: All required environment variables are set
✅ **Shopify Authentication**: Connected to H.B. Madsen store

## Deployment Options

### Option 1: Shopify Oxygen (Recommended) 🎯

**Current Issue**: Your account needs Hydrogen channel access.

**Prerequisites**:
1. **Shopify Partner Account** (https://partners.shopify.com/)
2. **Hydrogen Channel** installed in Partner dashboard
3. **Create Hydrogen Storefront** through Partner interface

**Steps to Enable Oxygen Deployment**:
```bash
# 1. Create Partner Account and install Hydrogen channel
# 2. Re-authenticate with Partner credentials
npx shopify hydrogen login

# 3. Link your project to a Hydrogen storefront
npx shopify hydrogen link

# 4. Deploy to staging
npx shopify hydrogen deploy --environment staging

# 5. Deploy to production
npx shopify hydrogen deploy --environment production
```

**Oxygen Benefits**:
- ✅ Immutable snapshots ensure consistency
- ✅ Unique preview URL for each deployment
- ✅ 6+ month retention with rollback capability
- ✅ Automated CI/CD with GitHub integration
- ✅ Runtime logs available for 1 month
- ✅ Global CDN and edge computing

### Option 2: Vercel Deployment 🌟

```bash
# Install Vercel CLI
npm install -g vercel

# Deploy to Vercel
vercel

# Set environment variables in Vercel dashboard:
# - SESSION_SECRET
# - PUBLIC_STORE_DOMAIN
# - PUBLIC_STOREFRONT_API_TOKEN
# - PUBLIC_CUSTOMER_ACCOUNT_API_CLIENT_ID
# - SHOP_ID
# - PUBLIC_CHECKOUT_DOMAIN
# - WEAVERSE_PROJECT_ID
# - All other variables from your .env file
```

### Option 3: Netlify Deployment 🔥

```bash
# Install Netlify CLI
npm install -g netlify-cli

# Build and deploy
npm run build
netlify deploy --prod --dir=dist/client

# Configure environment variables in Netlify dashboard
```

### Option 4: Railway Deployment 🚂

```bash
# Install Railway CLI
npm install -g @railway/cli

# Login and deploy
railway login
railway deploy

# Environment variables will be synced from your .env file
```

### Option 5: Docker Deployment 🐳

Create a `Dockerfile`:
```dockerfile
FROM node:20-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
RUN npm run build
EXPOSE 3000
CMD ["npm", "start"]
```

Deploy to any Docker-compatible platform:
- Google Cloud Run
- AWS ECS
- Azure Container Instances
- DigitalOcean App Platform

### Option 6: Static Site Generation

For static deployment to GitHub Pages, Cloudflare Pages, etc.:

```bash
# Generate static files (if supported by your setup)
npm run build:static

# Deploy the dist/client folder to any static hosting
```

## Environment Variables Required

Make sure these are set in your deployment platform:

```bash
SESSION_SECRET="foobar"
PUBLIC_STORE_DOMAIN=weaverse-hydrogen.myshopify.com
PUBLIC_STOREFRONT_API_TOKEN=939ac830f7c7c6d229a24dd78f4258f0
PUBLIC_CUSTOMER_ACCOUNT_API_CLIENT_ID=shp_182e9ed0-270f-473a-be74-e3073f852c39
SHOP_ID=72804106547
PUBLIC_CHECKOUT_DOMAIN=www.weaverse.dev
PUBLIC_STOREFRONT_ID=1000010106
WEAVERSE_PROJECT_ID=a6473a2zkbpfydf20necln06
METAOBJECT_COLORS_TYPE="shopify--color-pattern"
CUSTOM_COLLECTION_BANNER_METAFIELD="custom.collection_banner"
```

## GitHub CI/CD Setup (Recommended)

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy to Production
on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '20'
      - run: npm ci
      - run: npm run build
      - name: Deploy to Oxygen
        run: npx shopify hydrogen deploy --environment production
        env:
          SHOPIFY_CLI_TOKEN: ${{ secrets.SHOPIFY_CLI_TOKEN }}
```

## Custom Domain Setup

1. **For Oxygen**: Configure in Shopify Partner dashboard
2. **For other platforms**: 
   - Add CNAME record pointing to platform's domain
   - Configure SSL certificate
   - Update environment variables if needed

## Monitoring & Analytics

Add to your deployment:
- Google Analytics (set PUBLIC_GOOGLE_GTM_ID)
- Sentry for error tracking
- Performance monitoring tools

## Next Steps

1. **Choose your deployment platform** based on your needs
2. **Set up environment variables** on chosen platform
3. **Configure custom domain** if needed
4. **Set up CI/CD pipeline** for automated deployments
5. **Monitor performance** and optimize as needed

## Quick Start: Vercel Deployment

Since Oxygen requires additional setup, here's the fastest way to deploy right now:

```bash
npx vercel
```

This will guide you through the deployment process and your site will be live in minutes!