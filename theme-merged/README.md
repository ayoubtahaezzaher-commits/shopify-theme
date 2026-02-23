# Merged Shopify Theme — Merrachi + Ritual

## Overview

This theme is a **merged combination** of two Shopify themes:

| Theme | Source | Description |
|-------|--------|-------------|
| **Merrachi** | `theme-merrachi/theme merrachi/` | Feature-rich Halo framework theme with extensive section library, multiple header/footer variants, custom popups, and advanced product layouts |
| **Ritual** | `theme-ritual/theme_export__www-dubaivie-fr-ritual__23FEB2026-0239pm/` | Modern, content-focused theme with blocks architecture, layered slideshows, hero sections, and clean editorial layouts |

The merge strategy keeps **Merrachi as the primary theme** (its `theme.liquid` is the active layout). All Ritual files that conflict with Merrachi are available under the `ritual-` prefix.

---

## Directory Structure

```
theme-merged/
├── assets/          # 354 files (242 Merrachi + 112 Ritual, conflicts prefixed ritual-)
├── blocks/          # 94 files (all from Ritual — app blocks architecture)
├── config/          # settings_schema.json (merged), settings_data.json (Merrachi base)
├── layout/          # theme.liquid (Merrachi), theme-ritual.liquid (Ritual), password.liquid, password-ritual.liquid
├── locales/         # 59 files — en.default.json merged, all others from Merrachi
├── sections/        # 179 files (Merrachi + Ritual, conflicts prefixed ritual-)
├── snippets/        # 462 files (Merrachi + Ritual, conflicts prefixed ritual-)
└── templates/       # 82 files (Merrachi + Ritual, conflicts prefixed ritual-)
    └── customers/   # 7 customer account templates (Merrachi)
```

---

## Naming Convention

| Prefix | Origin | Example |
|--------|--------|---------|
| *(no prefix)* | **Merrachi** (primary) | `collection-list.liquid` |
| `ritual-` | **Ritual** (renamed to avoid conflict) | `ritual-collection-list.liquid` |
| `theme-ritual.liquid` | Ritual layout | `layout/theme-ritual.liquid` |

All Ritual `.liquid` sections and snippets that were renamed due to conflicts have the comment `{% comment %}Origin: Ritual Theme{% endcomment %}` prepended to their content.

---

## Conflicting Files (Both Themes Had These)

### Sections — Merrachi kept as-is, Ritual renamed with `ritual-` prefix

| Merrachi (active) | Ritual (available) |
|-------------------|--------------------|
| `collection-list.liquid` | `ritual-collection-list.liquid` |
| `custom-liquid.liquid` | `ritual-custom-liquid.liquid` |
| `featured-product.liquid` | `ritual-featured-product.liquid` |
| `footer-group.json` | `ritual-footer-group.json` |
| `header-group.json` | `ritual-header-group.json` |
| `main-404.liquid` | `ritual-main-404.liquid` |
| `main-blog.liquid` | `ritual-main-blog.liquid` |
| `main-cart.liquid` | `ritual-main-cart.liquid` |
| `main-page.liquid` | `ritual-main-page.liquid` |
| `marquee.liquid` | `ritual-marquee.liquid` |
| `predictive-search.liquid` | `ritual-predictive-search.liquid` |
| `product-recommendations.liquid` | `ritual-product-recommendations.liquid` |
| `quick-order-list.liquid` | `ritual-quick-order-list.liquid` |

### Snippets — Merrachi kept as-is, Ritual renamed with `ritual-` prefix

| Merrachi (active) | Ritual (available) |
|-------------------|--------------------|
| `gift-card-recipient-form.liquid` | `ritual-gift-card-recipient-form.liquid` |
| `meta-tags.liquid` | `ritual-meta-tags.liquid` |
| `price.liquid` | `ritual-price.liquid` |
| `product-card.liquid` | `ritual-product-card.liquid` |
| `swatch.liquid` | `ritual-swatch.liquid` |

### Templates — Merrachi kept as-is, Ritual renamed with `ritual-` prefix

| Merrachi (active) | Ritual (available) |
|-------------------|--------------------|
| `404.json` | `ritual-404.json` |
| `article.json` | `ritual-article.json` |
| `blog.json` | `ritual-blog.json` |
| `cart.json` | `ritual-cart.json` |
| `collection.json` | `ritual-collection.json` |
| `gift_card.liquid` | `ritual-gift_card.liquid` |
| `index.json` | `ritual-index.json` |
| `list-collections.json` | `ritual-list-collections.json` |
| `page.json` | `ritual-page.json` |
| `product.json` | `ritual-product.json` |
| `search.json` | `ritual-search.json` |

### Assets — Merrachi kept as-is, Ritual renamed with `ritual-` prefix

| Merrachi (active) | Ritual (renamed) |
|-------------------|------------------|
| `base.css` | `ritual-base.css` |
| `blog-posts-list.js` | `ritual-blog-posts-list.js` |
| `predictive-search.js` | `ritual-predictive-search.js` |
| `price-per-item.js` | `ritual-price-per-item.js` |
| `product-form.js` | `ritual-product-form.js` |
| `quick-order-list.js` | `ritual-quick-order-list.js` |
| `show-more.js` | `ritual-show-more.js` |
| `sticky-add-to-cart.js` | `ritual-sticky-add-to-cart.js` |
| `template-giftcard.css` | `ritual-template-giftcard.css` |

---

## Layout Files

| File | Source | Purpose |
|------|--------|---------|
| `layout/theme.liquid` | Merrachi | **Primary layout** — used by default |
| `layout/theme-ritual.liquid` | Ritual | Ritual layout — use by referencing in templates |
| `layout/password.liquid` | Merrachi | Password page layout |
| `layout/password-ritual.liquid` | Ritual | Ritual password layout |

---

## Blocks Directory (Ritual)

Ritual uses a `blocks/` directory for its app-block architecture. All 94 block files are copied as-is from Ritual. These are used internally by Ritual sections and templates (prefixed `ritual-` or unique Ritual sections).

---

## Config

- **`settings_schema.json`**: Merged — Merrachi's 28 entries first, then Ritual's 17 non-conflicting entries appended (entries with the same `name` as Merrachi are skipped).
- **`settings_data.json`**: Merrachi's version used as-is (contains active theme customization data).

---

## Locales

- **`en.default.json`**: Merged — Merrachi as base; Ritual-only top-level keys added: `actions`, `blocks`, `content`, `fields`, `placeholders`.
- **`en.default.schema.json`**: Merged — Merrachi as base; Ritual-only keys added.
- **`fi.schema.json`**, **`nb.schema.json`**: Ritual-only files, copied as-is (not present in Merrachi).
- All other locale files: Merrachi's version used.

---

## Installation Guide

### Option 1: Shopify CLI

```bash
# Install Shopify CLI if not already installed
npm install -g @shopify/cli @shopify/theme

# Login to your store
shopify auth login --store your-store.myshopify.com

# Push the merged theme
shopify theme push --path /path/to/theme-merged --store your-store.myshopify.com
```

### Option 2: Shopify Admin Upload

1. Zip the `theme-merged/` directory contents.
2. In Shopify Admin → **Online Store → Themes** → **Add theme → Upload zip file**.
3. Upload the zip and click **Publish** when ready.

### Option 3: Theme Kit

```bash
theme push --dir=/path/to/theme-merged
```

---

## Using Ritual Sections in the Merrachi Layout

To use a Ritual section in a Merrachi-based template, add it to any `.json` template file:

```json
{
  "sections": {
    "hero": {
      "type": "hero",
      "settings": {}
    },
    "ritual-marquee": {
      "type": "ritual-marquee",
      "settings": {}
    }
  },
  "order": ["hero", "ritual-marquee"]
}
```

Ritual-only sections (no prefix, unique to Ritual) can be used directly:
- `hero`, `carousel`, `slideshow`, `layered-slideshow`
- `media-with-content`, `divider`, `product-hotspots`
- `featured-blog-posts`, `featured-product-information`
- `collection-links`, `product-list`, `product-information`

---

## Switching to the Ritual Layout

To use specific templates with the Ritual layout, update the template's `layout` property:

```json
{
  "layout": "theme-ritual",
  "sections": { ... }
}
```

---

## Customization Notes

- **Merrachi Halo components** (popups, sidebars, mega menus) are controlled via `settings_data.json` and the Merrachi header/footer sections.
- **Ritual blocks** (`blocks/` directory) are used by Ritual's section architecture and are not directly compatible with Merrachi's layout without the Ritual layout wrapper.
- When customizing the theme in the Shopify Theme Editor, sections will appear from both themes — Merrachi sections are the default, Ritual sections appear with their original names (the `ritual-` prefix is the filename, not the display name in the editor).
