# Sean Langwade Plumbing & Heating website: notes for Claude

The Sean Langwade Plumbing & Heating site (family-run plumbing and heating engineer, West London), moved from Webflow
(project `langwadev2`) to Netlify. It is the plain Webflow export: static HTML, no build step. Every push to `main`
deploys automatically.

## Working on it

There is nothing to install or build. To preview locally, serve the repo root, for example:

```bash
npx serve .      # http://localhost:3000
```

## Where things live

| What | File |
| --- | --- |
| The site (one page: hero, services, contact form, footer) | `index.html` |
| Page not found | `404.html` (Netlify serves it for any unknown URL) |
| Styles | `css/langwadev2.webflow.css` (the Webflow export), `css/webflow.css`, `css/normalize.css` |
| Scripts | `js/webflow.js` (animations, mobile menu), `js/jquery-3.5.1.min.js`, `js/contact-form.js` |
| Images | `images/` (the hero photo is set in the CSS: `.hero-image`) |
| Netlify settings (redirects, headers) | `netlify.toml` |

## Contact form

The form uses **Netlify Forms** (form name `contact`). Submissions appear in the Netlify dashboard under *Forms*;
email notifications are set up there. `js/contact-form.js` sends the form and shows Webflow's thank-you or error
message. Fields: name, email, phone, address (street, city, postcode) and message. A hidden `bot-field` catches spam.

## WhatsApp button

The WhatsApp chat button (bottom right) is an Elfsight widget, still loaded from Elfsight's CDN
(`apps.elfsight.com`, widget `61adcaf9-...` at the top of `<body>`). It's managed in the Elfsight account, not here.

## Notes from the Webflow move

- Webflow's unused ecommerce template pages (checkout, PayPal checkout, order confirmation, product, category, SKU and
  the 401 password page) were left out. Their URLs redirect to the homepage in `netlify.toml`.
- The template's empty "Recent projects / Featured Products" CMS block (pottery template items with no titles) was
  removed from the homepage, along with its images and the other unused template images.
- City and Postcode shared one field name in the Webflow form, so only one was sent. They are now separate fields.
- jQuery is hosted with the site (`js/jquery-3.5.1.min.js`, the same file Webflow used). Google Fonts (via WebFont
  loader) and Elfsight still load from their own CDNs.
- All paths are root-relative (`/css/...`, `/images/...`) so the 404 page works at any URL.

## Rules for changes

- Keep the Webflow class names and `data-w-id` / `data-wf-page` / `data-wf-site` attributes. `js/webflow.js` uses
  them for the animations and the mobile menu.
- Commit to `main` with a clear message. Netlify deploys it within about a minute.
