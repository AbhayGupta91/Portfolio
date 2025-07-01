# Deployment Guide

This document outlines how to deploy the Abhay Gupta Portfolio website to various platforms.

## 🚀 Netlify Deployment (Recommended)

### Automatic Deployment from GitHub

1. **Connect Repository**
   - Go to [Netlify](https://netlify.com)
   - Click "New site from Git"
   - Choose GitHub and authorize
   - Select your portfolio repository

2. **Build Settings**
   - Build command: `npm run build`
   - Publish directory: `dist`
   - Node version: 18 or higher

3. **Environment Variables**
   - No environment variables needed for this static site

4. **Custom Domain (Optional)**
   - Go to Site settings → Domain management
   - Add your custom domain
   - Configure DNS settings

### Manual Deployment

1. Build the project locally:
```bash
npm run build
```

2. Drag and drop the `dist` folder to Netlify

## 🌐 Vercel Deployment

1. **Connect Repository**
   - Go to [Vercel](https://vercel.com)
   - Import your GitHub repository
   - Configure project settings

2. **Build Settings**
   - Framework Preset: Vite
   - Build Command: `npm run build`
   - Output Directory: `dist`

## 📦 GitHub Pages

1. **Enable GitHub Pages**
   - Go to repository Settings → Pages
   - Source: Deploy from a branch
   - Branch: `gh-pages` (you'll need to create this)

2. **Setup GitHub Actions** (create `.github/workflows/deploy.yml`):
```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    
    - name: Setup Node.js
      uses: actions/setup-node@v2
      with:
        node-version: '18'
        
    - name: Install dependencies
      run: npm install
      
    - name: Build
      run: npm run build
      
    - name: Deploy
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./dist
```

## 🔧 Build Optimization

### Performance Tips
- Images are optimized and served from external CDNs
- CSS is minified and tree-shaken
- JavaScript is bundled and optimized
- Lazy loading implemented where appropriate

### SEO Optimization
- Meta tags configured in `index.html`
- Semantic HTML structure
- Proper heading hierarchy
- Alt texts for images

## 📊 Analytics Setup

### Google Analytics (Optional)
Add to `index.html` before closing `</head>`:
```html
<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=GA_MEASUREMENT_ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'GA_MEASUREMENT_ID');
</script>
```

## 🚨 Troubleshooting

### Common Issues

1. **Build Fails**
   - Check Node.js version (18+ required)
   - Clear node_modules and reinstall
   - Check for TypeScript errors

2. **Routing Issues**
   - Configure redirects for SPA routing
   - Add `_redirects` file to public folder:
   ```
   /*    /index.html   200
   ```

3. **Performance Issues**
   - Optimize images
   - Check bundle size with `npm run build -- --analyze`
   - Implement code splitting if needed

## 📱 Mobile Testing

Before deployment, test on:
- Various screen sizes
- Different browsers
- Touch interactions
- Loading performance

## 🔒 Security

- No sensitive data exposed
- HTTPS enabled by default on modern platforms
- Content Security Policy headers recommended

## 📈 Monitoring

After deployment:
- Monitor Core Web Vitals
- Check for broken links
- Verify all features work correctly
- Test contact form functionality

---

For any deployment issues, contact: guptaxabhay@gmail.com