# GAIVS - Historiska Bilder & Almanackor

This is a Swedish e-commerce website selling historical imagery products (almanacs, postcards, posters) for Stockholm and Gothenburg.

## Project Structure

**Two-City Architecture**: The site uses a location-based directory structure:
- `sth/` - Stockholm (STHLM) version
- `gbg/` - Gothenburg (GBG) version  
- Root `index.html` - City selection landing page

Each city folder is a **complete standalone site** with identical structure but city-specific content.

## Key Patterns

### HTML Structure
- **Swedish Language**: All content, meta tags, and structured data are in Swedish (`lang="sv"`)
- **SEO-Heavy**: Extensive meta tags (Open Graph, Twitter Cards, Schema.org JSON-LD) on every page
- **Bootstrap 5.3.3**: Uses Bootstrap grid, utilities, and components with CDN links
- **Google Fonts**: Cormorant Garamond (headings) + Lato (body text) loaded from Google Fonts API
- **Schema.org Products**: All products use itemscope/itemtype markup with structured pricing data

### CSS Architecture
- **CSS Variables**: Design system defined in `:root` with color scheme and typography variables
- **Three CSS Files Per City**: 
  - `gaius.css` - Main styles shared across sections
  - `gaius2.css` - Additional component styles
  - `gaius3.css` - Extended styles
- **Product Card Variants**: Classes like `.product-card6`, `.product-card7`, `.product-card8` with different background patterns (`.bg-pattern-1`, `.bg-pattern-2`)
- **Vintage Theme**: Uses earthy tones (`--main-bg-color: #e4d8c8`, `--vintage-bg-1: #f5efe6`)

### Product Display Pattern
Each product follows this HTML structure:
```html
<article class="product-card[N] bg-pattern-[1|2] mb-5" itemscope itemtype="https://schema.org/Product">
    <div class="row g-0 align-items-center">
        <div class="col-lg-6 order-lg-2 prodposs">
            <img src="..." alt="..." class="img-fluid" itemprop="image">
        </div>
        <div class="col-lg-6">
            <div class="product-content prod-bg-text-color[N] text-center text-lg-start">
                <a href="..." class="btn-buy mb-2">Köp</a>
                <p class="price mb-1" itemprop="offers" itemscope itemtype="https://schema.org/Offer">
                    <span itemprop="price">249</span> <span itemprop="priceCurrency" content="SEK">kr</span>
                </p>
                <h2 class="product-title" itemprop="name">Product Name</h2>
                <p class="product-description" itemprop="description">Description...</p>
            </div>
        </div>
    </div>
</article>
```

### External Integration
- **WordPress Backend**: Buy links point to `https://gaius.se/wpAdmin/produkt/...` for checkout
- **Image CDN**: Product images served from `https://gaius.se/wpAdmin/wp-content/uploads/...` and local `img/` folders
- **Development URL**: Some assets reference `https://dev.frontdata.se/gaius/...`

## Common Tasks

### Adding a New Product
1. Copy existing `<article class="product-card[N]">` block
2. Update product-card variant number (6, 7, 8 etc.) and bg-pattern class
3. Replace image URL, alt text, and Schema.org metadata
4. Update price, title, description, and WordPress product URL
5. Ensure both `sth/` and `gbg/` versions are updated if product is city-specific

### Modifying Styles
- **Color Changes**: Edit CSS variables in `:root` of `gaius.css`
- **Typography**: Adjust `--heading-font` and `--body-font` variables
- **Product Cards**: Modify `.product-card[N]` classes and `.prod-bg-text-color[N]` for specific variants

### SEO Content Updates
- Check `seo/` folders for copywriting templates (e.g., `Säljtext STHLM.txt`, `Säljtexter GBG.txt`)
- Update meta descriptions, OG tags, and JSON-LD structured data together
- Keep city names consistent: "Stockholm" (not STHLM) and "Göteborg" (not GBG) in user-facing text

## Version Control
- Commits use date-based versioning: `git commit -m "2026-01-26 version 1"`
- Working directory: `H:\frontdatadisken_live\wwwroot\gaius2026\live`

## Important Notes
- **No Build Process**: Static HTML/CSS served directly (no bundler, preprocessor, or package.json)
- **City Parity**: When editing content, remember both `sth/` and `gbg/` need parallel updates
- **Disabled Buy Buttons**: Some products use `pointer-events: none; opacity: 0.5` when out of stock
- **Accessibility**: Uses semantic HTML5 (`<header>`, `<main>`, `<article>`, `role`, `aria-label` attributes)
