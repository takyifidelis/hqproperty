# HQ Property Valuation & Consulting - AI Agent Instructions

## Project Overview

Single-page static website for HQ Valuation and Property Consulting, a Ghana-based property advisory firm. Built using the BootstrapMade "Groovin" template with Bootstrap 5.3.3.

## Architecture & Structure

### Core Files

- `index.html` - Single-page application (1233 lines) with all content sections
- `assets/css/main.css` - Custom styles (1863 lines) with CSS variables for theming
- `assets/js/main.js` - Vanilla JavaScript for interactions (265 lines)
- `forms/contact.php` & `forms/newsletter.php` - PHP email form handlers (require pro version library)

### Section Structure (order matters for nav scrollspy)

Sections are ID-based anchors linked from navigation:

1. `#hero` - Carousel with 3 slides (property valuation messaging)
2. `#about` - Company info with tabbed content
3. `#stats` - Statistics counters (uses PureCounter)
4. `#portfolio` - Client logos/portfolio (actually named "clients section")
5. `#services` - Service cards grid
6. `#why-us` - Benefits section
7. `#team` - Team member cards
8. `#faq` - Accordion-style FAQ
9. `#contact` - Contact form with Google Maps embed

## Styling System

### CSS Variables (in `:root`)

```css
--default-font: "Roboto"
--heading-font: "Playfair Display"
--nav-font: "Merriweather"
--accent-color: #5c9f24 (brand green)
--background-color: #ffffff
--heading-color: #2a2a2a
```

### Background Modifiers

- `.light-background` - Light grey (#f9f9f9)
- `.dark-background` - Dark theme with white text
- Applied at section level to alternate visual rhythm

## JavaScript Patterns

### Mobile Navigation

- Toggle via `.mobile-nav-toggle` button
- Adds `.mobile-nav-active` class to body
- Icon switches between `bi-list` and `bi-x`

### Scroll Behaviors

- **Scrollspy**: Highlights active nav link based on scroll position (200px offset)
- **Sticky Header**: Adds `.scrolled` class to body after 100px scroll
- **Hash Navigation**: Handles URL hash links with smooth scroll and margin offset

### Third-Party Libraries

- **AOS** (Animate On Scroll) - `data-aos="fade-up"` attributes throughout
- **Isotope** - Portfolio filtering (`.isotope-layout` containers)
- **GLightbox** - Image lightbox galleries
- **Swiper** - Carousels with `.init-swiper` class
- **imagesLoaded** - Ensures Isotope initializes after images load

## Key Conventions

### Image Paths

**ISSUE**: Double slashes in hero carousel paths:

```html
src="assets/assets/img//template/Groovin/hero-carousel/..."
```

Should be: `assets/img/template/Groovin/hero-carousel/...`

### WhatsApp Integration

Scroll-top button doubles as WhatsApp link:

```html
<a href="https://wa.me/qr/RLY3X3MONSJ2P1" id="scroll-top" class="scroll-top">
  <i class="bi bi-whatsapp"></i>
</a>
```

### Preloader

Custom preloader uses HQ logo (`assets/img/HQ.png`), auto-removes on page load

### Form Handling

PHP forms require BootstrapMade pro library (`vendor/php-email-form/php-email-form.php`).
Default receiving email: `contact@example.com` (needs configuration).

## Development Workflow

### No Build Process

Static site - direct file editing. Refresh browser to see changes.

### Vendor Libraries (all minified)

Located in `assets/vendor/`:

- Bootstrap 5.3.3 (CSS + JS)
- Bootstrap Icons (CSS + fonts)
- AOS, GLightbox, Swiper, Isotope, PureCounter
- Do NOT modify vendor files

### Testing Locally

Use any static server:

```powershell
# Python
python -m http.server 8000

# PHP
php -S localhost:8000

# VS Code Live Server extension
```

## Content Update Patterns

### Adding Portfolio Items

Use Isotope filter classes on `.portfolio-item`:

```html
<div
  class="col-lg-4 col-md-6 portfolio-item isotope-item filter-[category]"
></div>
```

Available filters: `filter-app`, `filter-product`, `filter-branding`, `filter-books`

### Adding Team Members

Clone `.team-member` card structure with `.img-fluid` images and social links

### Service Cards

Use `.service-item` with icon (Bootstrap Icons or custom), title, and description

### FAQ Items

Structure: `.faq-item > h3 + .faq-content`, auto-toggles `.faq-active` on click

## Known Issues to Fix

1. **Image path redundancy**: `assets/assets/img//` in hero carousel
2. **Scroll-top button**: Event listener has empty string `scrollTop.addEventListener("", ...)` (line ~83 in main.js)
3. **Contact form**: Requires pro library or custom PHP implementation
4. **Placeholder content**: About section tabs contain lorem ipsum (lines 189-280 in index.html)

## AI Agent Best Practices

- **Respect section order**: Changes affect scrollspy navigation
- **Test scroll behaviors**: Modifications to sections need scroll offset verification
- **Maintain CSS variable consistency**: Use existing theme colors, don't hardcode
- **AOS delays**: Use increments of 100-200ms for staggered animations
- **Preserve vendor code**: Never edit files in `assets/vendor/`
- **Bootstrap classes**: Leverage existing Bootstrap utilities before custom CSS
