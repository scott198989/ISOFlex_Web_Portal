# ISOFlex Hub - Deployment Guide

## 🚀 Quick Deploy to Cloudflare Pages

### Method 1: Direct Upload (Fastest - 5 minutes)

1. **Prepare files:**
   - Main hub: `index.html`
   - 3D view: `3d.html`

2. **Deploy:**
   - Go to: https://dash.cloudflare.com/
   - Click: **Workers & Pages** → **Create** → **Pages** → **Upload assets**
   - Upload both HTML files
   - Project name: `isoflex-hub`
   - Click: **Deploy site**

3. **Access:**
   - Hub: `https://isoflex-hub.pages.dev/`
   - 3D: `https://isoflex-hub.pages.dev/3d.html`

---

### Method 2: GitHub Integration (Recommended for continuous deployment)

This connects your GitHub repo to Cloudflare Pages so every push auto-deploys.

#### Step 1: Connect GitHub to Cloudflare

1. Go to: https://dash.cloudflare.com/
2. Click: **Workers & Pages** → **Create** → **Pages** → **Connect to Git**
3. Authorize Cloudflare to access your GitHub
4. Select your repository: `isoflex-hub`

#### Step 2: Configure Build Settings

Since this is a simple HTML site (no build step needed):

- **Build command:** (leave empty)
- **Build output directory:** `/`
- **Root directory:** (leave as default)

Click **Save and Deploy**

#### Step 3: Done!

- Every push to `main` branch auto-deploys
- Preview deployments for pull requests
- Automatic HTTPS
- Global CDN
- Instant rollbacks

---

## 🔗 Custom Domain (Optional)

### Add Your Own Domain

1. In Cloudflare Pages project settings
2. Click **Custom domains**
3. Add your domain (e.g., `app.isoflex.com`)
4. Follow DNS setup instructions
5. SSL automatically provisioned

---

## 🔄 Updating the Site

### With GitHub Integration:
```bash
# Make changes to your files
git add .
git commit -m "Updated dashboard"
git push origin main

# Cloudflare automatically deploys in ~30 seconds
```

### With Direct Upload:
- Go back to Pages project
- Upload new files
- Old version automatically replaced

---

## 🌐 Environment Setup (For Future API Integration)

When you add Workers/D1 database:

### 1. Create wrangler.toml
```toml
name = "isoflex-hub"
compatibility_date = "2024-01-01"

pages_build_output_dir = "dist"

[[d1_databases]]
binding = "DB"
database_name = "isoflex_production"
database_id = "your-database-id"

[[r2_buckets]]
binding = "STORAGE"
bucket_name = "isoflex-files"
```

### 2. Add Environment Variables
In Cloudflare dashboard → Settings → Environment variables:
```
API_URL=https://your-worker.workers.dev
DB_ID=your-database-id
```

---

## 📊 Connecting NCM Dashboard

### Current Setup:
- NCM dashboard is separate: `https://ncm-analytics-db.pages.dev/`
- ISOFlex Hub links to it

### Future Integration Options:

**Option A: Keep Separate (Current)**
- ✅ Simple, already working
- ✅ NCM dashboard can be updated independently
- ❌ Different URLs

**Option B: Proxy Through Hub**
Create a Worker to proxy requests:
```javascript
// _worker.js
export default {
  async fetch(request, env) {
    const url = new URL(request.url);
    
    // Proxy NCM dashboard
    if (url.pathname.startsWith('/ncm-data')) {
      return fetch('https://ncm-analytics-db.pages.dev' + url.pathname);
    }
    
    // Serve static files
    return env.ASSETS.fetch(request);
  }
}
```

**Option C: Merge Projects**
- Move NCM dashboard files into this repo
- Deploy as one unified app
- Single URL for everything

---

## 🔐 Adding Authentication

### Cloudflare Access (Free for 50 users)

1. Go to: Zero Trust → Access → Applications
2. Create application:
   - Name: `ISOFlex Hub`
   - Domain: `isoflex-hub.pages.dev`
3. Add access policy:
   - Allow emails: `you@company.com`, `boss@company.com`
4. Save

Now the entire site requires login via email verification.

### Custom Auth with Workers

For more control, build custom auth:
- Workers handle login/logout
- D1 stores user sessions
- Cookies for authentication
- Role-based access control

---

## 📈 Monitoring & Analytics

### Built-in Cloudflare Analytics
- Go to your Pages project
- Click **Analytics** tab
- See: visitors, bandwidth, requests, performance

### Add Custom Analytics

**Option 1: Cloudflare Web Analytics** (Privacy-focused)
```html
<!-- Add to <head> of index.html -->
<script defer src='https://static.cloudflareinsights.com/beacon.min.js' 
        data-cf-beacon='{"token": "your-token"}'></script>
```

**Option 2: Umami** (Self-hosted)
```html
<script async src="https://umami.yourdomain.com/script.js" 
        data-website-id="your-id"></script>
```

---

## 🐛 Troubleshooting

### Site Not Loading
- Check DNS propagation: https://dnschecker.org
- Clear browser cache: Ctrl+Shift+Delete
- Check Cloudflare status: https://cloudflarestatus.com

### Changes Not Appearing
- GitHub integration: Check deployment status in Pages dashboard
- Direct upload: Hard refresh: Ctrl+Shift+R
- Wait 1-2 minutes for CDN propagation

### SSL Certificate Issues
- Wait 24-48 hours after adding custom domain
- Check DNS settings in Cloudflare dashboard
- Ensure proxy (orange cloud) is enabled

---

## 📱 Testing

### Desktop Browsers
- Chrome/Edge: Primary testing
- Firefox: Check compatibility
- Safari: Test on Mac if available

### Mobile Devices
- Chrome mobile: Android testing
- Safari mobile: iOS testing
- Test in landscape and portrait

### Tablets
- iPad: Factory floor usage
- Android tablet: Alternative testing

---

## 🚀 Performance Optimization

### Current Setup
Already optimized:
- ✅ Cloudflare CDN (global distribution)
- ✅ HTML minification
- ✅ Brotli compression
- ✅ HTTP/3 support

### Future Improvements
When scaling to full React app:
- Code splitting
- Lazy loading
- Image optimization
- Service worker for offline support

---

## 📞 Support Resources

### Cloudflare Docs
- Pages: https://developers.cloudflare.com/pages/
- Workers: https://developers.cloudflare.com/workers/
- D1: https://developers.cloudflare.com/d1/

### Community
- Discord: https://discord.gg/cloudflaredev
- Forum: https://community.cloudflare.com/
- Stack Overflow: Tag `cloudflare-workers`

---

## ✅ Deployment Checklist

- [ ] Repository created on GitHub
- [ ] Files pushed to main branch
- [ ] Connected to Cloudflare Pages
- [ ] Site deployed successfully
- [ ] Tested on desktop browser
- [ ] Tested on mobile device
- [ ] Custom domain added (if applicable)
- [ ] SSL certificate active
- [ ] Team members can access
- [ ] Analytics configured

---

**Your site is production-ready. Ship it.** 🚀
