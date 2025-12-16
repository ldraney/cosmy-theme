# Cosmy Theme

Custom Shopify theme for the Cosmy cosmetics manufacturing demo. Based on Dawn (Shopify's reference theme).

## What This Is

This theme powers the Cosmy storefront - a demo of a private label/custom manufacturing cosmetics business. It needs to look polished and professional while showcasing:

- Private label product catalog
- Custom manufacturing services
- B2B wholesale portal (MOQs, tiered pricing, NET terms)

The theme is part of a larger demo system (see `~/cosmy-project/CLAUDE.md`) where Shopify orders trigger Monday.com tasks and Inflow inventory operations.

## Theme Structure

```
cosmy-theme/
├── assets/          # CSS, JS, images, fonts
│   ├── base.css     # Foundation styles
│   └── *.js         # JavaScript modules
├── config/
│   └── settings_schema.json  # Theme customizer options
├── layout/
│   └── theme.liquid          # Master template (wraps everything)
├── locales/         # Translation strings (i18n)
├── sections/        # Building blocks for the theme editor
│   ├── header.liquid
│   ├── footer.liquid
│   ├── main-product.liquid
│   └── ...
├── snippets/        # Reusable partials (components)
│   ├── card-product.liquid
│   ├── icon-*.liquid
│   └── ...
└── templates/       # JSON files composing sections into pages
    ├── index.json           # Homepage
    ├── product.json         # Product detail page
    ├── collection.json      # Collection/category page
    └── page.*.json          # Custom pages
```

## Key Concepts

### Sections (OS 2.0)
Sections are the building blocks. Each section:
- Has its own Liquid template (`sections/*.liquid`)
- Defines a `{% schema %}` block with settings
- Can be added/removed/reordered in the theme editor
- Is self-contained (styles, markup, settings)

### Snippets
Reusable partials. Use `{% render 'snippet-name' %}` to include them.
Good for: product cards, icons, repeated UI patterns.

### Templates (JSON)
Define which sections appear on each page type. Example `templates/index.json`:
```json
{
  "sections": {
    "hero": { "type": "hero-banner" },
    "featured": { "type": "featured-collection" }
  },
  "order": ["hero", "featured"]
}
```

### Settings Schema
`config/settings_schema.json` defines global theme settings (colors, fonts, logo, etc.) that appear in the Shopify admin under Theme Settings.

## Figma → Theme Workflow

When converting Figma designs to theme code:

1. **Identify sections** - What are the major page blocks?
2. **Map to existing sections** - Does Dawn already have something similar?
3. **Create/modify sections** - Add new `.liquid` files in `sections/`
4. **Extract components** - Repeated UI → `snippets/`
5. **Define settings** - What should merchants customize?
6. **Update templates** - Wire sections into page templates

## Development Commands

```bash
# Install Shopify CLI (if not installed)
brew tap shopify/shopify
brew install shopify-cli

# Start local development server
shopify theme dev --store=your-store.myshopify.com

# Push theme to Shopify
shopify theme push

# Pull latest from Shopify
shopify theme pull

# Check theme for errors
shopify theme check
```

## Code Style

- **Liquid** - Keep logic minimal in templates; use snippets for complexity
- **CSS** - Use CSS custom properties for theming; BEM-ish naming
- **JS** - Vanilla JS preferred; minimal dependencies
- **Accessibility** - Semantic HTML, ARIA labels, keyboard navigation

## Customization Priorities

For Cosmy specifically:

1. [ ] Branding - Colors, typography, logo placement
2. [ ] Homepage - Hero, featured products, value props
3. [ ] Product page - Optimized for cosmetics (ingredients, usage, variants)
4. [ ] Collection page - Grid layout, filtering for product types
5. [ ] B2B elements - Wholesale pricing display, MOQ notices
6. [ ] Custom pages - About, Services (private label vs custom manufacturing)

## Useful References

- [Dawn GitHub](https://github.com/Shopify/dawn)
- [Shopify Liquid Docs](https://shopify.dev/docs/api/liquid)
- [Theme Architecture](https://shopify.dev/docs/themes/architecture)
- [Section Schema](https://shopify.dev/docs/themes/architecture/sections/section-schema)

## Notes for Claude

- This is a visual-first project - changes should be demo-able
- When editing sections, always check the `{% schema %}` block for available settings
- Test changes with `shopify theme dev` before pushing
- Keep Dawn's performance optimizations intact when customizing
- The audience is cosmetics business owners, not developers
