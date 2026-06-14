# Component Usage

This skill explains how the UI component architecture is structured in this Next.js template and how to use the existing components.

## Component Architecture

Components are grouped into two primary folders within `src/layouts/`:
1. **`src/layouts/components/`**: Smaller, reusable UI elements.
2. **`src/layouts/partials/`**: Larger page sections or layout wrappers.

> [!IMPORTANT]
> **Component Verification Required:** Because this skill is used across multiple templates, the components listed below are **JUST EXAMPLES**. Components may be missing, renamed, or structured differently depending on the specific template you are working with. **You MUST ALWAYS verify component existence and read their actual implementation by checking `src/layouts/components/` and `src/layouts/partials/` before attempting to use or modify them.**

## Example Components (Verify Before Use)

The following are common examples you *might* find in the template:

### `<BlogCard />`
Located in `src/layouts/components/BlogCard.tsx`.
- **Purpose**: Displays a single blog post preview.
- **Props**: Receives a `data` object containing the parsed markdown content and frontmatter.
- **Usage**: Commonly mapped over an array of posts in `src/app/blog/page.tsx` and `src/app/page.tsx`.

### `<SeoMeta />`
Located in `src/layouts/partials/SeoMeta.tsx`.
- **Purpose**: Injects SEO tags into the `<head>` of the document.
- **Props**: `title`, `meta_title`, `description`, `image`.
- **Usage**: Automatically used by the `layout.tsx` files or page components to set metadata. It falls back to `config.json` if props are omitted.

### `<ThemeSwitcher />`
Located in `src/layouts/components/ThemeSwitcher.tsx`.
- **Purpose**: Toggles between light and dark mode.
- **Usage**: Utilizes the `useTheme` hook from `next-themes`. Embedded inside the `<Header />` component.

### `<Logo />`
Located in `src/layouts/components/Logo.tsx`.
- **Purpose**: Renders the site logo using `next/image` with fallback to text if no image is provided.
- **Usage**: Pulls source URLs directly from `config.json` (`logo`, `logo_darkmode`).

## Modifying Components

When extending components:
- **Styling**: Components generally use Tailwind utility classes directly in the `className` prop. If a component requires complex CSS, it may rely on classes defined in `src/styles/components.css`.
- **Data Fetching**: Components in `src/layouts/components/` should ideally remain stateless or rely on props. Data fetching (like reading markdown files) should happen in the page-level components (`src/app/**/page.tsx`), passing the data down as props.

## Common Mistakes / What NOT to do

- **DO NOT** embed heavy data fetching logic directly inside atomic components (like `BlogCard`). Pass data down from Server Components (pages) to keep the UI components pure.
- **DO NOT** hardcode generic values like the site name into components. They should always pull from `config.json` or props.
- **DO NOT** assume a component exists just because it is listed in this document. Always verify its existence in the codebase before using it.
