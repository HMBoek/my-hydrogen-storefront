# 🔐 GitHub Repository Secrets Setup

This guide explains how to configure the required secrets for automated deployment.

## Required Secrets

Navigate to your GitHub repository → Settings → Secrets and Variables → Actions → Repository secrets

### Core Shopify Configuration
```
SESSION_SECRET=foobar
PUBLIC_STORE_DOMAIN=weaverse-hydrogen.myshopify.com
PUBLIC_STOREFRONT_API_TOKEN=939ac830f7c7c6d229a24dd78f4258f0
PUBLIC_CUSTOMER_ACCOUNT_API_CLIENT_ID=shp_182e9ed0-270f-473a-be74-e3073f852c39
SHOP_ID=72804106547
PUBLIC_CHECKOUT_DOMAIN=www.weaverse.dev
WEAVERSE_PROJECT_ID=a6473a2zkbpfydf20necln06
METAOBJECT_COLORS_TYPE=shopify--color-pattern
CUSTOM_COLLECTION_BANNER_METAFIELD=custom.collection_banner
```

### Deployment Platform Secrets

#### For Shopify Oxygen Deployment
```
SHOPIFY_CLI_TOKEN=your-shopify-cli-token
```
*Get this by running `shopify auth login` locally and finding the token*

#### For Vercel Deployment (Alternative)
```
VERCEL_TOKEN=your-vercel-token
VERCEL_ORG_ID=your-vercel-org-id
VERCEL_PROJECT_ID=your-vercel-project-id
```
*Get these from your Vercel dashboard → Settings → Tokens*

## How to Add Secrets

1. **Go to Repository Settings**
   ```
   https://github.com/HMBoek/my-hydrogen-storefront/settings/secrets/actions
   ```

2. **Click "New repository secret"**

3. **Add each secret one by one:**
   - Name: `SESSION_SECRET`
   - Value: `foobar`
   - Click "Add secret"

4. **Repeat for all secrets listed above**

## Verifying Secrets

After adding secrets, your GitHub Actions workflow will:
- ✅ Build your Hydrogen storefront
- ✅ Run type checking
- ✅ Deploy to Shopify Oxygen (if configured)
- ✅ Deploy to Vercel (if configured)
- ✅ Run security scans

## Local Development

Keep your local `.env` file for development:
```bash
cp .env.example .env
# Edit .env with your values
```

## Deployment Status

- 🟢 **Build**: Automatic on every push
- 🟡 **Oxygen**: Requires Shopify Partner account
- 🟢 **Vercel**: Ready for deployment
- 🟢 **Security**: Automated scanning enabled

## Next Steps

1. ✅ Add repository secrets (above)
2. ✅ Push code to trigger deployment
3. ✅ Monitor GitHub Actions tab
4. ✅ Configure custom domain
5. ✅ Set up monitoring & analytics