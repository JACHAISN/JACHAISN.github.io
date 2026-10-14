# Jachai Samson — Architecture Portfolio

Source for [jachaisamson.github.io](https://jachaisamson.github.io/), a hand-coded, static
architecture portfolio (plain HTML/CSS/JS, no build step). It replaces the old Adobe Portfolio site.

## Structure

```
index.html                  Home page
work.html                   Project index / grid
contact.html                Contact page
projects/                   One HTML file per project
css/style.css                Design system
js/main.js                  Nav toggle + scroll reveal
images/[project-slug]/       Drop project images here
```

## Adding images to a project

1. Drop image files into `images/[project-slug]/` (e.g. `images/contemplation-pod/01.jpg`).
2. Open `projects/[project-slug].html` and find the placeholder `<figure>` blocks in the
   `.project-gallery` section.
3. Replace each placeholder:

   ```html
   <figure>
     <div class="placeholder-frame"><span>Image coming soon</span></div>
   </figure>
   ```

   with:

   ```html
   <figure>
     <img src="../images/contemplation-pod/01.jpg" alt="Describe what's in the image" loading="lazy" />
     <figcaption>Optional caption</figcaption>
   </figure>
   ```

4. Keep `alt` text descriptive (what the image shows, not just the filename) — it matters for
   accessibility and SEO.
5. Optimize images before adding them (see below) so the site stays fast.

## Optimizing images

Before dropping images in, compress and resize them:

- Aim for photos/renders no wider than ~2400px on the long edge.
- Export as JPEG (photos/renders) or PNG (line drawings with flat color) at ~75–85% quality.
- Tools: [Squoosh](https://squoosh.app) (browser, no install), or `npx @squoosh/cli` from the
  command line.

## Local preview

No build step — just open `index.html` in a browser, or serve the folder locally:

```bash
npx serve .
```

## Deployment — GitHub Pages

1. Create a new GitHub repository (public, since GitHub Pages on the free tier requires a public
   repo unless you're on GitHub Pro/Enterprise).
2. Push this folder to it (see commands below).
3. In the repo, go to **Settings → Pages**.
4. Under **Build and deployment → Source**, choose **Deploy from a branch**.
5. Pick the `main` branch and `/ (root)` folder, then **Save**.
6. GitHub will publish the site at `https://<username>.github.io/<repo-name>/` within a minute
   or two.

### Custom domain later

1. Buy a domain from any registrar (Namecheap, Google Domains successor Squarespace, Cloudflare, etc).
2. In the repo's **Settings → Pages**, enter the domain under **Custom domain** — this creates a
   `CNAME` file in the repo automatically.
3. At your domain registrar, add DNS records pointing at GitHub Pages:
   - For an apex domain (`jachaisamson.com`): four `A` records pointing to
     `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`.
   - For a subdomain (`www.jachaisamson.com`): a `CNAME` record pointing to
     `<username>.github.io`.
4. Wait for DNS to propagate (up to 24h, usually much faster), then enable **Enforce HTTPS** in
   the Pages settings once the certificate is issued.
