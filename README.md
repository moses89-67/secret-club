# Secret Club® - MVP Landing Page

Limited drops. Premium streetwear. Members only vibes.

## Features

- ✨ **Exclusive Landing Page** - Dark, modern design capturing the secret club vibe
- 📧 **Email Waitlist** - Capture early members with email validation
- 📊 **Live Stats** - Follower count, member count, exclusivity meter
- 🎁 **Drops Grid** - Showcase upcoming product drops
- 📱 **Fully Responsive** - Mobile-first design
- 🔗 **Social Links** - Instagram, Twitter, Discord integration
- ⚡ **Lightweight** - Vanilla JS, minimal dependencies

## Quick Start

### Option 1: Static Deploy (Recommended for Now)

If you just want the landing page without a backend:

```bash
# No installation needed! Just open index.html in your browser
# Or upload the HTML, CSS, JS files to any static host
```

### Option 2: With Node.js Server

```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Server will run on http://localhost:3000
```

## Project Structure

```
secret-club/
├── index.html          # Main HTML file
├── styles.css          # Styling
├── script.js           # Frontend logic
├── server.js           # Express backend (optional)
├── package.json        # Dependencies
├── .env.example        # Environment template
└── README.md           # This file
```

## Deployment Options

### 1. Vercel (Recommended - Free & Fast)

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel
```

**or** just connect your GitHub repo to Vercel dashboard.

### 2. Netlify (Free)

Drag and drop the `index.html`, `styles.css`, `script.js` files to netlify.com

### 3. Railway

```bash
# Connect your GitHub repo to Railway
# Railway will auto-detect and run with npm start
```

### 4. Self-Hosted (VPS)

```bash
# SSH into your server
ssh user@your-server.com

# Clone repo
git clone <your-repo> secret-club
cd secret-club

# Install dependencies
npm install

# Start with PM2 (keep alive)
npm install -g pm2
pm2 start server.js --name "secret-club"
pm2 startup
pm2 save
```

### 5. Fly.io

```bash
# Install Fly CLI
# https://fly.io/docs/hands-on/install-flyctl/

# Deploy
fly launch
fly deploy
```

## API Endpoints

If running with Node.js server:

### POST `/api/waitlist`
Add an email to the waitlist

```bash
curl -X POST http://localhost:3000/api/waitlist \
  -H "Content-Type: application/json" \
  -d '{"email": "user@example.com"}'
```

**Response:**
```json
{
  "success": true,
  "message": "Successfully added to waitlist",
  "count": 42
}
```

### GET `/api/waitlist`
Get all waitlist emails (for admin)

```bash
curl http://localhost:3000/api/waitlist
```

### GET `/api/health`
Server health check

```bash
curl http://localhost:3000/api/health
```

## Customization

### Change Colors

Edit the CSS variables in `styles.css`:

```css
:root {
  --color-primary: #ffffff;
  --color-bg: #0a0a0a;
  --color-accent: #ffc107;
  /* ... etc */
}
```

### Update Social Links

In `index.html`, update these URLs:

```html
<a href="https://instagram.com/secretclub.cl" ...>📷</a>
<a href="https://twitter.com/..." ...>𝕏</a>
<a href="https://discord.com/..." ...>💬</a>
```

### Customize Drops

In `index.html`, modify the drops grid:

```html
<div class="drops-grid">
  <div class="drop-card">Your Drop Name<br>Drop Details</div>
  <!-- Add more cards -->
</div>
```

## Next Steps

### Phase 1: MVP (Done ✓)
- Landing page
- Email capture
- Basic stats

### Phase 2: Backend
- [ ] Connect to real database (Supabase, Firebase, PostgreSQL)
- [ ] Send welcome emails (SendGrid, Mailgun)
- [ ] Track analytics
- [ ] Admin dashboard

### Phase 3: Products
- [ ] Product gallery with images
- [ ] Inventory management
- [ ] Stripe integration for checkout
- [ ] Order tracking

### Phase 4: Community
- [ ] Members-only Discord bot
- [ ] Early access to drops
- [ ] Exclusive content
- [ ] Leaderboard / tier system

## Environment Variables

Copy `.env.example` to `.env` and fill in your keys:

```bash
cp .env.example .env
```

### For Email (SendGrid):
1. Sign up at sendgrid.com
2. Get API key
3. Add to `.env`: `SENDGRID_API_KEY=your_key`

### For Database (Supabase):
1. Create project at supabase.com
2. Get connection string
3. Add to `.env`: `DATABASE_URL=your_connection_string`

### For Instagram Live Count:
1. Set up Instagram Graph API
2. Get access token
3. Add to `.env`: `INSTAGRAM_ACCESS_TOKEN=your_token`

## Database Schema

When you're ready for a database, here's the basic schema:

```sql
CREATE TABLE waitlist (
  id SERIAL PRIMARY KEY,
  email VARCHAR(255) UNIQUE NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  status VARCHAR(50) DEFAULT 'pending'
);

CREATE TABLE drops (
  id SERIAL PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  description TEXT,
  image_url VARCHAR(255),
  launch_date TIMESTAMP,
  quantity INT,
  status VARCHAR(50) DEFAULT 'upcoming'
);

CREATE TABLE orders (
  id SERIAL PRIMARY KEY,
  email VARCHAR(255),
  drop_id INT REFERENCES drops(id),
  quantity INT,
  amount FLOAT,
  status VARCHAR(50),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## Analytics

The site logs interactions to browser console. Integrate Google Analytics, Mixpanel, or Amplitude for production tracking.

```javascript
// Add to script.js for GA integration:
gtag('event', 'join_waitlist', {
  email_provided: true
});
```

## Troubleshooting

### "Module not found" errors
```bash
npm install
```

### Port already in use
```bash
# On Mac/Linux:
lsof -i :3000
kill -9 <PID>

# On Windows:
netstat -ano | findstr :3000
taskkill /PID <PID> /F
```

### Email validation not working
Check that email regex is correct in `script.js`:
```javascript
const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
```

## License

MIT - Feel free to use and modify

## Support

Questions or issues? Create a GitHub issue or reach out:
- Instagram: @secretclub.cl
- Discord: [Your Discord Link]

---

**Made with ♠️♦️♣️ for the Secret Club**
