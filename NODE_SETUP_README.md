# Node.js 18 Setup Guide

## ? Configuration Complete

Your React + Vite project is now configured to use Node.js 18 and compatible packages.

## What Was Done

### 1. **package.json** - Added Node.js engine requirement
```json
"engines": {
  "node": ">=18.0.0",
  "npm": ">=9.0.0"
}
```

### 2. **.nvmrc** - Created for local Node.js version management
- Specifies Node.js 18.20.5 (LTS)
- If you use `nvm`, run: `nvm use`

### 3. **GitHub Actions Workflow** - `.github/workflows/azure-deploy.yml`
- Uses Node.js 18.x for builds
- Builds the Vite app
- Deploys to Azure App Service
- Includes web.config for SPA routing

## Current Package Versions (All Compatible with Node.js 18+)

| Package | Version | Node.js Requirement |
|---------|---------|---------------------|
| React | 19.1.1 | >=18 |
| Vite | 7.1.7 | >=18 |
| TypeScript | 5.9.3 | >=14.17 |
| ESLint | 9.36.0 | >=18 |

## Local Development

### Using NVM (Node Version Manager)
```bash
# Install the specified Node.js version
nvm install 18.20.5

# Use the version
nvm use

# Verify
node -v  # Should show v18.20.5 (or your current version)
```

### Without NVM
Ensure you have Node.js 18.x or higher installed:
```bash
node -v  # Should show v18.x.x or higher
```

## Build & Run Commands

```bash
# Install dependencies
npm ci

# Run development server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview

# Lint code
npm run lint
```

## Azure Deployment

### Prerequisites
- Azure App Service (Windows) created
- GitHub repository connected
- Azure secrets configured in GitHub:
  - `AZUREAPPSERVICE_CLIENTID_E3BC0BBEE0654254B7DB993BF54AC263`
  - `AZUREAPPSERVICE_TENANTID_016ECB5C6F2F48CF81C76BD6080CF1AE`
  - `AZUREAPPSERVICE_SUBSCRIPTIONID_671887B85C2848348EA864B7FA0F8D85`

### Deploy Steps
1. Commit your changes
2. Push to `master` branch
3. GitHub Actions will automatically:
   - Install dependencies with npm ci
   - Build with Node.js 18.x
   - Copy web.config for SPA routing
   - Deploy to Azure App Service

### Manual Build (Local)
```bash
npm ci
npm run build
# Build output will be in ./dist
```

## Troubleshooting

### "npm ci" fails
- Delete `node_modules` and `package-lock.json`
- Run `npm install` to regenerate lock file

### Build fails
- Ensure Node.js 18+ is installed: `node -v`
- Clear cache: `npm cache clean --force`
- Reinstall: `rm -rf node_modules && npm ci`

### Deployment fails
- Check GitHub Actions logs
- Verify Azure secrets are configured
- Ensure `web.config` exists in root directory

## Package Compatibility Notes

All current packages are compatible with Node.js 18:
- **React 19** requires Node.js >=18
- **Vite 7** requires Node.js >=18
- **TypeScript 5.9** works with Node.js 14+
- **ESLint 9** requires Node.js >=18

If you need to downgrade packages for older Node.js versions, you would need:
- Node.js 16: Use React 18, Vite 5, ESLint 8
- Not recommended - Node.js 16 reached End of Life

## Next Steps

1. **Install dependencies**: `npm ci`
2. **Test locally**: `npm run dev`
3. **Build**: `npm run build`
4. **Commit and push** to trigger Azure deployment

## Support

For issues:
- Check [Vite documentation](https://vite.dev/)
- Review [React documentation](https://react.dev/)
- Check Azure App Service logs in Azure Portal
