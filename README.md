# ISOFlex Manufacturing Hub

**Your central operations platform for real-time manufacturing intelligence**

## 🚀 Quick Start

### Immediate Deployment (5 minutes)

1. **Rename the file:**
   ```
   isoflex-hub.html → index.html
   ```

2. **Deploy to Cloudflare Pages:**
   - Go to: https://dash.cloudflare.com/
   - Click: Workers & Pages → Create → Pages → Upload assets
   - Upload `index.html`
   - Project name: `isoflex-hub`
   - Click: Deploy site

3. **Done!** Your site is live at: `https://isoflex-hub.pages.dev`

### Add 3D Visualization

1. Upload `3d-ncm-dashboard.html` as `3d.html` to same project
2. Access at: `https://isoflex-hub.pages.dev/3d.html`
3. Or update the NCM page to link directly to it

---

## 📦 Current Modules

### ✅ Live
- **Dashboard** - Central hub with all modules
- **NCM Analytics** - Links to existing dashboard + 3D view

### 🚧 Coming Soon
- **Certificates of Analysis** - Document management + OCR
- **Silo Resin Levels** - Real-time inventory monitoring
- **Shipping & Logistics** - Order tracking
- **Advanced Analytics** - Predictive insights

---

## 🛠️ Tech Stack

- **React 18** - UI framework
- **React Router** - Navigation
- **Tailwind CSS** - Styling
- **Cloudflare Pages** - Hosting
- **Cloudflare Workers** - API layer (when needed)
- **Cloudflare D1** - Database

---

## 📈 Roadmap

### Phase 1: Foundation (✅ DONE)
- [x] Landing page / hub
- [x] Navigation system
- [x] NCM module integration
- [x] 3D visualization
- [x] Responsive design

### Phase 2: CoA Module (NEXT)
- [ ] Upload interface (PDF/images)
- [ ] Cloudflare R2 storage
- [ ] OCR for searchability
- [ ] Metadata extraction
- [ ] Search and filter
- [ ] Download/share links

### Phase 3: Silo Monitoring
- [ ] Data input method (sensors/manual)
- [ ] Real-time dashboard
- [ ] Low-level alerts
- [ ] Usage trends/predictions
- [ ] Historical data

### Phase 4: Shipping & Logistics
- [ ] Order entry system
- [ ] Delivery schedule tracker
- [ ] Customer notifications
- [ ] Integration with existing systems

### Phase 5: Advanced Analytics
- [ ] Cross-module data correlation
- [ ] Predictive analytics (ML)
- [ ] Custom report builder
- [ ] Executive dashboards
- [ ] Export capabilities

---

## 🔧 Expanding to Full Project

When ready to scale with TypeScript and build tools:

### 1. Initialize Project
```bash
npm create vite@latest isoflex-hub -- --template react-ts
cd isoflex-hub
npm install
```

### 2. Install Dependencies
```bash
npm install react-router-dom @tanstack/react-query zustand framer-motion
npm install -D tailwindcss postcss autoprefixer wrangler
```

### 3. Setup Tailwind
```bash
npx tailwindcss init -p
```

### 4. Project Structure
```
isoflex-hub/
├── src/
│   ├── components/      # Reusable UI components
│   ├── pages/           # Page components
│   ├── layouts/         # Layout wrappers
│   ├── hooks/           # Custom hooks
│   ├── services/        # API calls
│   ├── store/           # State management
│   ├── types/           # TypeScript types
│   └── utils/           # Helpers
├── public/              # Static assets
└── package.json
```

### 5. Deploy with Wrangler
```bash
npm run build
wrangler pages deploy dist
```

---

## 🎨 Customization

### Colors
Edit the Tailwind config in the HTML file:
```javascript
tailwind.config = {
  theme: {
    extend: {
      colors: {
        primary: '#3b82f6',    // Change these
        secondary: '#8b5cf6',
        accent: '#06b6d4',
      }
    }
  }
}
```

### Branding
Replace "ISOFlex" with your brand name in:
- Page title
- Navigation logo
- Footer

### Modules
Add new modules by copying the module card structure in `DashboardPage`.

---

## 🔐 Adding Authentication (Later)

When you need to lock down the app:

### Option 1: Cloudflare Access (Easy)
- Free for up to 50 users
- Email-based authentication
- Zero code changes needed
- Setup in Cloudflare dashboard

### Option 2: Custom Auth (Advanced)
- Build login system
- Use Cloudflare Workers + D1
- JWT tokens
- Role-based access

---

## 📊 Connecting to Real Data

### Current Setup
- NCM data: Links to existing dashboard
- All other data: Coming soon

### Future API Structure
```javascript
// Example Worker endpoint
export default {
  async fetch(request, env) {
    const url = new URL(request.url);
    
    if (url.pathname === '/api/ncm') {
      const db = env.DB; // D1 database
      const { results } = await db.prepare(
        'SELECT * FROM ncm_data ORDER BY date DESC LIMIT 100'
      ).all();
      return Response.json(results);
    }
    
    // Add more endpoints...
  }
}
```

### In React (with TanStack Query)
```typescript
import { useQuery } from '@tanstack/react-query';

function useNCMData() {
  return useQuery({
    queryKey: ['ncm'],
    queryFn: async () => {
      const res = await fetch('/api/ncm');
      return res.json();
    },
    refetchInterval: 30000, // Refresh every 30s
  });
}
```

---

## 🚀 Next Steps

1. **Deploy the hub** → Get it live NOW
2. **Test on mobile** → Make sure it works everywhere
3. **Show leadership** → Get feedback and buy-in
4. **Pick next module** → CoA is probably easiest to start
5. **Build iteratively** → Ship features as you complete them

---

## 💡 The Business Model

This isn't just a dashboard - it's **the product**.

### Your Path:
1. **Prove it works** - Use it daily at your plant
2. **Show results** - Document time savings, error reduction
3. **Get testimonial** - From your leadership
4. **Package it** - Clean up, document, make it deployable
5. **Sell it** - To other mid-size manufacturers

### Pricing Ideas:
- **Self-hosted**: $5k setup + $500/month
- **Managed**: $10k setup + $1,500/month (you host and support)
- **Custom modules**: $2-5k per module

You've got 9 years of manufacturing experience. You know the pain points. You built the solution. Now you own the IP.

---

## 📝 License

Proprietary - © 2025 Scott Tuschl / ISOFlex

---

## 🤝 Support

Built by: Scott Tuschl
With: Claude (Anthropic)
Stack: React + Cloudflare
Status: 🟢 Production Ready

**Let's fucking go.** 🚀