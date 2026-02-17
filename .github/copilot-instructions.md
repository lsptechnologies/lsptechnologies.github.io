# LSP Technologies Website — Copilot Instructions

## Project Overview
This is a **static GitHub Pages marketing website** for LSP Technologies Inc., a Canadian technology venture studio. The entire site is a single `index.html` file with inline Tailwind CSS and vanilla JavaScript — no build process, no frameworks, no complex dependencies.

**Key understanding:** This is a minimal, intentional design. Keep it that way. Updates should respect the single-file architecture and the carefully curated design system.

## Architecture & File Structure
```
.
├── index.html          # Complete site (422 lines) — hero, about, platforms, contact sections
├── assets/
│   ├── logo.png       # LSP Technologies logo (used in nav and footer)
│   └── oncall.png     # OnCallNow product image (displayed in platform card 01)
├── README.md          # Brief project description
└── .github/copilot-instructions.md
```

**No separate CSS, no JS bundles, no config files.** All styling and scripts are inline in the HTML `<head>` and end of `<body>`.

## Design System & Styling Conventions

### Color Palette (defined in Tailwind config)
- **navy** — Primary background (`#0D1B3E`), `mid: #1E3A8A`, `light: #2D4FAA`
- **brand-red** — Action buttons, accents (`#C8102E`)
- **brand-teal** — Call-to-action, hover states, borders (`#14B8A6`)
- **brand-gold** — Accent color (`#C9A84C`)

### Typography
- **Display font** — Cormorant Garamond (serif) for headers and brand identity
- **Body font** — DM Sans (sans-serif) for all other text
- Both loaded from Google Fonts CDN

### Consistent Patterns
- **Section structure** — Each section (`hero`, `about`, `platforms`, `contact`) starts with aligned teal leader line + uppercase label
- **Buttons** — Use `brand-red` with uppercase tracking, hover transitions include `-translate-y-0.5` for lift effect
- **Input styling** — Backdrop blur with border-teal on focus (lines 135–142)
- **Animations** — Custom keyframes defined in `<style>` block: `gridShift`, `fadeUp`, `fadeIn`, `scrollLine`

## How to Make Common Changes

### Add/Update Section Content
1. Find the section by ID comment (`<!-- ── SECTION_NAME ── -->`)
2. Preserve the section header structure (teal leader, label, heading with `font-display`)
3. Keep Tailwind utilities consistent with existing sections
4. Example: The platforms section (lines 314–371) has 3 grid cards — add new cards by duplicating structure

### Update Brand Assets
- Replace `./assets/logo.png` or `./assets/oncall.png` in place
- Update `alt` text appropriately
- No need to rebuild or process — just swap files

### Modify Colors or Animations
- Colors: Edit `theme.extend.colors` in the Tailwind config (lines 12–15)
- Animations: Add/modify keyframes in the `<style>` block (lines 42–102) or the Tailwind config (lines 16–21)

### Form Handling
The contact form (lines 375–409) has no backend wired up — inputs are static HTML. To connect to a service:
- Use `form id="contactForm"` wrapper
- Add `type="submit"` to the button
- Implement a fetch() handler in the JavaScript section (currently only has scroll reveal logic)

## Javascript Behavior
The site has minimal, vanilla JS (lines 413–422):
- **Scroll reveal** — IntersectionObserver watches `.scroll-reveal` elements
- **Nav shrinking** — Detects scroll position to adjust navbar styling

**Note:** No `.scroll-reveal` elements currently exist in the HTML, so the observer runs but doesn't affect anything. This is likely a placeholder for future use.

## Git Workflow
- Current branch: `dev`
- Default branch: `main`
- This is a **GitHub Pages site** — deployment happens on push to `main`

## Key Constraints & Decisions
- **Single file by design** — Keep HTML, CSS, and JS together. No separate stylesheets or script bundles.
- **Tailwind inline** — Loaded from CDN (`cdn.tailwindcss.com`), config defined in `<script>` tag
- **No TypeScript, no bundler, no CI/CD** — Extremely simple. Changes deploy directly on commit.
- **Cloudflare email obfuscation** — Contact email is protected; see line 407 for encoded format
- **Responsive via Tailwind** — Use `clamp()` for fluid typography, grid breakpoints defined with Tailwind
- **Canadian identity** — References to Canada, CBCA incorporation, Ontario location are intentional brand markers

## Testing & Validation
- **No automated tests** — Manually verify in browser
- **Check responsive** — Test navbar, hero, platforms grid on mobile/tablet/desktop
- **Verify animations** — Grid shift, fade-up, scroll line should run smoothly on scroll
- **Test form inputs** — Ensure focus states (teal border) work and placeholder text is visible

## Common Pitfalls to Avoid
1. ❌ Adding external dependencies or frameworks — this defeats the simplicity
2. ❌ Separating CSS into a stylesheet — breaks the intentional single-file architecture
3. ❌ Changing the navbar structure — it's tightly integrated with the logo and navigation UX
4. ❌ Using color hex values directly instead of the defined color system
5. ❌ Forgetting `font-display` class for headers — consistency matters for brand

## Quick Links to Important Sections
- **Design system config** — Lines 11–21 (Tailwind theme extension)
- **Custom CSS** — Lines 31–102 (animations, interactive styles)
- **Navigation** — Lines 104–115
- **Hero section** — Lines 117–177
- **About section** — Lines 179–258
- **Platforms section** — Lines 260–371
- **Contact & form** — Lines 373–410
- **Footer** — Lines 412–428
- **JavaScript** — Lines 413–422 (scroll reveal, nav behavior)
