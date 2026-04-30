# Studio Theme Auto-Deploy

This repo uses GitHub Actions to auto-deploy the Studio theme to the u5rtvy-0a Shopify store on every push to `main`.

## Setup (One-time)

1. **Install the Theme Access app on the u5rtvy-0a store:**
   - Go to https://apps.shopify.com/theme-access
   - Install the app on u5rtvy-0a.myshopify.com
   - From the store admin, generate a Theme Access password

2. **Add the secret to this repo:**
   - Go to https://github.com/OpsAgentsAI/opsagents-studio-theme/settings/secrets/actions
   - Create a new repository secret:
     - Name: `SHOPIFY_THEME_TOKEN`
     - Value: Paste the Theme Access password (starts with `shpat_`)
   - **IMPORTANT:** Never commit this password. Store it ONLY as a GitHub Actions secret.

3. **Verify:**
   - Push any change to `main` on the theme directories (assets/, blocks/, config/, etc.)
   - Check the "Actions" tab — the workflow should run and deploy to the store
   - If it fails with "401 Invalid API key", the secret is wrong or the app isn't installed

## Usage

After setup, every push to `main` that touches the theme directories automatically deploys. No manual steps needed.

### Manual deploy (if needed)
```bash
shopify theme push --path . --store u5rtvy-0a.myshopify.com
```

## Token distinction

- **Theme Access password** (`shpat_*`) — Use this for the workflow. Generate from apps.shopify.com/theme-access.
- **Admin API access token** — Do NOT use this. Admin tokens are for the Shopify Admin API, not theme deployment.

The workflow uses `SHOPIFY_CLI_THEME_TOKEN` which expects the Theme Access password format.
