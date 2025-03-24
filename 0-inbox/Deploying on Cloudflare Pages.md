# Deploying on Cloudflare Pages
```bash
# Install Wrangler CLI
npm install -g wrangler

# Login to Cloudflare account from CLI
wrangler login

# Run your build command
npm run build

# Create new deployment
npx wrangler pages deploy dist
```