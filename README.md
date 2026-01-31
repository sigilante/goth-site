# goth.pink - Jekyll Site

A gloriously nostalgic 90s-inspired Jekyll website for the Goth programming language.

## Features

- 🎀 Hot pink gradient background with 90s grunge texture
- 🖤 Black frames with neon pink borders
- ⚡ Fixed sidebar navigation with floating goth mascot
- 📜 Scrollable main content area
- ✨ Sacred geometry (Metatron's Cube)
- 💅 Syntax-highlighted Goth code examples
- 📱 Responsive design

## Local Development

### Prerequisites

- Ruby 2.7+ (check with `ruby -v`)
- Bundler (`gem install bundler`)

### Setup

```bash
# Install dependencies
bundle install

# Serve locally
bundle exec jekyll serve

# Visit http://localhost:4000
```

### Live Reload (Optional)

```bash
bundle exec jekyll serve --livereload
```

## Deploying to GitHub Pages

### Option 1: Direct Push (Easiest)

1. Create a new repository on GitHub named `goth.pink` or `yourusername.github.io`

2. Initialize and push:
```bash
cd jekyll-site
git init
git add .
git commit -m "Initial commit: goth.pink website"
git branch -M main
git remote add origin https://github.com/yourusername/goth.pink.git
git push -u origin main
```

3. Enable GitHub Pages:
   - Go to repository Settings → Pages
   - Source: Deploy from a branch
   - Branch: `main` / `(root)`
   - Save

4. Your site will be at: `https://yourusername.github.io/goth.pink/`

### Option 2: GitHub Actions (Recommended)

Create `.github/workflows/jekyll.yml`:

```yaml
name: Deploy Jekyll site to Pages

on:
  push:
    branches: ["main"]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Setup Ruby
        uses: ruby/setup-ruby@v1
        with:
          ruby-version: '3.1'
          bundler-cache: true
      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v4
      - name: Build with Jekyll
        run: bundle exec jekyll build --baseurl "${{ steps.pages.outputs.base_path }}"
        env:
          JEKYLL_ENV: production
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

Then:
1. Push to GitHub
2. Settings → Pages → Source: "GitHub Actions"
3. Site deploys automatically on every push!

### Custom Domain (goth.pink)

1. In your repository:
   - Settings → Pages → Custom domain
   - Enter: `goth.pink`
   - Save

2. In your domain registrar (Namecheap, etc.):
   - Add A records pointing to GitHub Pages IPs:
     ```
     185.199.108.153
     185.199.109.153
     185.199.110.153
     185.199.111.153
     ```
   - Or add CNAME record: `yourusername.github.io`

3. Wait for DNS propagation (can take up to 24 hours)

4. Enable HTTPS in repository settings once DNS resolves

## Project Structure

```
jekyll-site/
├── _config.yml           # Jekyll configuration
├── _layouts/
│   └── default.html      # Main layout template
├── _includes/
│   ├── sidebar.html      # Sidebar navigation
│   └── metatron.html     # Sacred geometry SVG
├── assets/
│   ├── css/
│   │   └── style.css     # All the pink glory
│   └── images/
│       └── header-pink-transparent.png  # Goth mascot
├── index.html            # Homepage
├── Gemfile               # Ruby dependencies
└── README.md             # This file
```

## Adding Content

### New Page

Create a file like `about.md`:

```markdown
---
layout: default
title: About Goth
---

# About

Content here...
```

### New Blog Post

Create `_posts/2026-01-31-my-post.md`:

```markdown
---
layout: default
title: My First Post
---

Content here...
```

### New Doc

Create `_docs/keywords.md`:

```markdown
---
layout: default
title: Keywords Reference
---

# Keywords

...
```

## Customization

### Colors

Edit `assets/css/style.css`:

```css
/* Main gradient background */
background: linear-gradient(135deg, 
    #ff69b4 0%,    /* Hot pink */
    #ff1493 25%,   /* Deep pink */
    #c71585 50%,   /* Medium violet red */
    ...
);

/* Frame borders */
border: 3px solid #ff1493;
```

### Fonts

Current setup:
- **Headers:** Blackletter/Gothic (with system fallbacks)
- **Code:** Fira Code (from Google Fonts)
- **Body:** Fira Code

To add custom fonts, place them in `assets/fonts/` and update CSS.

### Configuration

Edit `_config.yml`:

```yaml
title: goth
description: the language for machine spirits
url: "https://goth.pink"
github_repo: "https://github.com/yourusername/goth"
```

## Troubleshooting

### "Bundler version mismatch" error
```bash
gem install bundler
bundle update --bundler
```

### "Cannot load such file" error
```bash
bundle install
```

### GitHub Pages build failing
- Check Actions tab for error details
- Ensure Gemfile only includes GitHub Pages-compatible plugins
- Check `_config.yml` syntax

### Custom domain not working
- Verify DNS records with `dig goth.pink`
- Wait for DNS propagation (24-48 hours)
- Check CNAME file was created in repository root

## Performance

- SVG graphics (scalable, no HTTP requests)
- Inline critical CSS (loads instantly)
- Single font load (Fira Code from Google)
- Minimal JavaScript (none currently)

## Browser Support

- ✅ Chrome/Edge (full support)
- ✅ Firefox (full support)
- ✅ Safari (full support)
- ⚠️  IE11 (works but no CSS Grid)

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test locally with `bundle exec jekyll serve`
5. Submit a pull request

## License

Do whatever you want with this. It's a website. 💖

---

**Built with 💗 and excessive amounts of hot pink**

*The Goth Language - where machine spirits meet sacred geometry*
