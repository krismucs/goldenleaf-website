# Goldenleaf Technologies — Deployment Guide

## Option 1: Squarespace (Recommended for You)

Since you already have a Squarespace site at goldenleaf-ai.com, there are two approaches:

### Approach A: Use Squarespace's Built-In Editor + Custom Code Injection

This is the easiest path. Use Squarespace's drag-and-drop editor for the overall site structure, then inject custom styling and sections.

**Steps:**

1. **Log into Squarespace** → Go to your site dashboard
2. **Go to Settings → Advanced → Code Injection**
3. **In the "Header" box**, paste the Google Fonts link and any custom CSS wrapped in `<style>` tags
4. **Build pages using Squarespace's editor** (Home, About, Services, Learn AI, Blog, Contact)
5. **For each page section**, use Squarespace's "Code Block" to paste custom HTML snippets from `index.html`

**What to inject in Code Injection → Header:**
```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=Playfair+Display:wght@600;700&display=swap" rel="stylesheet">
<style>
  /* Paste the color variables and any global overrides from the CSS in index.html */
  :root {
    --gold: #C9A84C;
    --green: #2D5A3D;
    --green-dark: #1A3626;
    --cream: #FDF8EF;
  }
</style>
```

**What to inject in Code Injection → Footer:**
```html
<script>
  // Paste the JavaScript from the bottom of index.html
</script>
```

### Approach B: Replace Squarespace with a Custom Code Page

If you want the exact website I built (as a single page):

1. In Squarespace, go to **Pages → Add Page → "Blank" page**
2. Add a **Code Block** (from the block inserter)
3. Toggle **"Display Source"** on
4. Paste the **entire contents** of `index.html`
5. **Note:** Squarespace may strip some HTML. This works best on Business plan or higher.

### Approach C: Use a Squarespace Template + Match the Design

The most maintainable long-term option:

1. Choose a **clean, minimal Squarespace template** (e.g., Brine, Bedford, or Skye family)
2. Set your **site-wide fonts** to Inter (body) and Playfair Display (headings) under Design → Fonts
3. Set your **color palette** to match: Gold (#C9A84C), Green (#2D5A3D), Cream (#FDF8EF)
4. Recreate each section using Squarespace's native blocks
5. Use **Code Injection** for the scroll animations and any custom styling


## Option 2: Google Cloud Hosting

If you want full control and to host the standalone HTML site:

### Using Google Cloud Storage (Static Site Hosting)

1. **Install Google Cloud CLI:**
   ```bash
   curl https://sdk.cloud.google.com | bash
   gcloud init
   ```

2. **Create a Cloud Storage bucket** named after your domain:
   ```bash
   gsutil mb gs://goldenleaf-ai.com
   ```

3. **Upload the website files:**
   ```bash
   gsutil -m cp -r ./goldenleaf-website/* gs://goldenleaf-ai.com/
   ```

4. **Make files publicly readable:**
   ```bash
   gsutil iam ch allUsers:objectViewer gs://goldenleaf-ai.com
   ```

5. **Set the main page:**
   ```bash
   gsutil web set -m index.html gs://goldenleaf-ai.com
   ```

6. **Point your domain DNS** to Google Cloud Storage:
   - Add a CNAME record: `www` → `c.storage.googleapis.com`
   - For the root domain, you'll need a load balancer (see Google's docs)

### Using Firebase Hosting (Easier Alternative on Google Cloud)

1. **Install Firebase CLI:**
   ```bash
   npm install -g firebase-tools
   firebase login
   ```

2. **Initialize project:**
   ```bash
   firebase init hosting
   ```
   - Select your Google Cloud project
   - Set public directory to `goldenleaf-website`
   - Configure as single-page app: **No**

3. **Deploy:**
   ```bash
   firebase deploy
   ```

4. **Connect your custom domain:**
   - Go to Firebase Console → Hosting → Add custom domain
   - Follow the DNS verification steps for goldenleaf-ai.com


## Option 3: Other Easy Hosting Alternatives

### Netlify (Free tier available)
1. Go to [netlify.com](https://netlify.com)
2. Drag and drop the `goldenleaf-website` folder onto the page
3. Your site is live instantly
4. Add your custom domain in Site Settings → Domain Management

### Vercel (Free tier available)
1. Go to [vercel.com](https://vercel.com)
2. Import or drag-drop the folder
3. Add your domain


## Customization Checklist

Before going live, update these placeholders in the HTML:

- [ ] Replace placeholder phone number with your real number
- [ ] Replace `hello@goldenleaf-ai.com` with your actual email
- [ ] Update the trust bar company names with real clients (or remove the section)
- [ ] Update stats in the About section with your actual numbers
- [ ] Add real YouTube/video links to the video cards
- [ ] Update blog post content with real articles
- [ ] Add your real social media links in the footer
- [ ] Update the contact form to connect to a real backend (Formspree, Netlify Forms, etc.)
- [ ] Add a favicon (replace the default browser icon)
- [ ] Add Google Analytics or another analytics tool
