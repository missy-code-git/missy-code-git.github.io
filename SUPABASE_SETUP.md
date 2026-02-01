# Supabase OAuth Setup Guide

This PhD Tracker now includes secure authentication using Supabase OAuth. Follow these steps to set it up:

## Step 1: Create a Supabase Project

1. Go to [supabase.com](https://supabase.com) and sign up for a free account
2. Create a new project:
   - Click "New Project"
   - Choose your organization
   - Enter project name: `phd-tracker`
   - Set a database password
   - Select your region (closest to you)
   - Click "Create new project"

## Step 2: Get Your Supabase Credentials

1. Once your project is created, go to **Settings** → **API**
2. Copy your:
   - **Project URL**: `https://qkoeclfnwiowjpcuqrfj.supabase.co` ✓ (already set)
   - **Public API Key** (anon key) - you still need to get this

## Step 3: Update index.html with Your Credentials

In `index.html`, find this section (around line 5822):

```javascript
const SUPABASE_URL = 'https://qkoeclfnwiowjpcuqrfj.supabase.co'; // ✓ Already set
const SUPABASE_KEY = 'YOUR-SUPABASE-PUBLIC-KEY'; // ← Update this
```

Replace `YOUR-SUPABASE-PUBLIC-KEY` with your actual Public API Key from Step 2.

## Step 4: Configure OAuth Providers

### GitHub OAuth:
1. In Supabase, go to **Authentication** → **Providers**
2. Click on **GitHub**
3. Enable the provider
4. Go to [GitHub Settings → Developer settings → OAuth Apps](https://github.com/settings/developers)
5. Create a new OAuth App:
   - **Application name:** PhD Tracker
   - **Homepage URL:** `https://missy-code-git.github.io`
   - **Authorization callback URL:** `https://YOUR-PROJECT-ID.supabase.co/auth/v1/callback`
6. Copy your **Client ID** and **Client Secret**
7. Paste them into the Supabase GitHub provider settings

### Google OAuth:
1. In Supabase, go to **Authentication** → **Providers** → **Google**
2. Enable the provider
3. Go to [Google Cloud Console](https://console.cloud.google.com/)
4. Create a new project or select existing
5. Create OAuth 2.0 credentials (OAuth consent screen):
   - User type: External
   - Add required scopes: `email, profile`
6. Create OAuth Client ID:
   - Type: Web application
   - Authorized redirect URIs: `https://YOUR-PROJECT-ID.supabase.co/auth/v1/callback`
7. Copy **Client ID** and **Client Secret**
8. Paste into Supabase Google provider settings

### Microsoft Azure OAuth:
1. In Supabase, go to **Authentication** → **Providers** → **Azure**
2. Enable the provider
3. Go to [Azure Portal](https://portal.azure.com/)
4. Register a new application:
   - Name: PhD Tracker
   - Supported account types: Multitenant
5. In Certificates & secrets, create a new client secret
6. In Redirect URI, add: `https://YOUR-PROJECT-ID.supabase.co/auth/v1/callback`
7. Copy your **Application (client) ID** and **Client Secret value**
8. Paste into Supabase Azure provider settings

## Step 5: Update Redirect URL in index.html

The OAuth redirect is currently set to `window.location.origin`. If your site is at `https://missy-code-git.github.io`, this will work automatically.

For custom domains, update the `redirectTo` in each login function if needed.

## Step 6: Deploy to GitHub Pages

```bash
cd c:\git\missy-code-git.github.io
git add .
git commit -m "Add Supabase OAuth authentication"
git push
```

## Step 7: Test the Login

1. Go to your GitHub Pages site: `https://missy-code-git.github.io`
2. You should see the login screen
3. Click any OAuth provider button to test
4. After successful login, you'll see the PhD Tracker with your email displayed

## Troubleshooting

- **"Redirect URL not allowed"**: Make sure the redirect URL in your OAuth provider settings exactly matches Supabase's callback URL
- **Blank login screen**: Check browser console (F12) for errors. Make sure `SUPABASE_URL` and `SUPABASE_KEY` are correctly set
- **OAuth provider not showing**: Enable it in Supabase Authentication → Providers settings

## Data Privacy

- User credentials are handled securely by Supabase
- Supabase is SOC 2 compliant
- Your data is encrypted in transit and at rest
- You control all data in your Supabase database

## Additional Features

You can now:
- Track user information in Supabase
- Sync PhD Tracker data across devices
- Add collaborative features
- Set up automatic backups

For more info, see [Supabase Docs](https://supabase.com/docs)
