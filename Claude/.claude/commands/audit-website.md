# 🌐 Website Audit — Nuxt 4 + Nuxt UI + NuxtHub

You are a Senior Frontend Engineer specializing in Nuxt 4, Vue 3, Nuxt UI, and NuxtHub.
Your task is to perform a **comprehensive and detailed audit** of this project and produce a full report in Arabic.

---

## 🧠 Project Context — Read This First

- **Framework:** Nuxt 4 (new `app/` directory structure)
- **UI Library:** Nuxt UI (use its components and theme system in all recommendations)
- **Backend/Hosting:** NuxtHub (Cloudflare Workers, D1, KV, Blob, Cache)
- **Language:** JavaScript as the primary language — TypeScript is used **only** in:
  - `nuxt.config.ts`
  - `app.config.ts`
  - `utils/` files that are written once and rarely changed
  - Other static config files
- **Components, Composables, Pages:** Pure JavaScript (`<script setup>`)
- **Project Type:** Public-facing website — SEO is the highest priority

---

## 📂 Step 1 — Map the Project Structure

Before any analysis, do the following:

1. Read the full directory structure
2. Read `nuxt.config.ts`, `app.config.ts`, and `package.json`
3. Read `CLAUDE.md` if it exists
4. Identify all modules, plugins, and middleware in use
5. Understand the nature of the site (number of pages, content type, whether auth exists)

---

## 🔍 Audit Dimensions

### 1. 🔐 Security

Scan every file in the project and look for:

**A. Sensitive Data Exposure**
- Any `API_KEY`, `SECRET`, `TOKEN`, or `PASSWORD` hardcoded in source files
- Sensitive variables placed in `runtimeConfig.public` instead of the private `runtimeConfig`
- `.env` file committed to the repo (not in `.gitignore`)
- Missing `.env.example` file for documentation

**B. NuxtHub Security**
- Server routes in `server/api/` with no input validation
- `hubDatabase()`, `hubKV()`, or `hubBlob()` used without permission checks
- CORS open to all origins in server routes

**C. XSS and Injection**
- Any usage of `v-html` — where does the content come from? Is it sanitized?
- `innerHTML` anywhere in the codebase
- User-supplied data rendered directly without sanitization

**D. HTTP Security Headers**
- Is `Content-Security-Policy` configured in `nuxt.config.ts`?
- Is `X-Frame-Options` set?
- Is `X-Content-Type-Options` set?
- Is `Referrer-Policy` set?

**E. NuxtHub Specific**
- Are `NUXT_HUB_PROJECT_KEY` and `NUXT_HUB_PROJECT_SECRET` stored only in `.env`?
- Is remote storage properly restricted?

---

### 2. ⚡ Performance & Core Web Vitals

**A. LCP (Largest Contentful Paint)**
- Does the hero image use `<NuxtImg>` with `priority` or `preload`?
- Are fonts loaded with `font-display: swap`?
- Is `@nuxt/fonts` used or are fonts manually optimized?

**B. CLS (Cumulative Layout Shift)**
- Do all `<img>` and `<NuxtImg>` elements have explicit `width` and `height`?
- Do dynamic components cause layout shift on load?
- Do fonts cause FOUT/FOIT?

**C. INP (Interaction to Next Paint)**
- Are there heavy event listeners attached to many elements?
- Do animations use only `transform` and `opacity` (GPU-accelerated)?

**D. Bundle Size**
- What is the total bundle size? Check `nuxt build` output or `.nuxt/analyze`
- Are large third-party libraries imported in full instead of tree-shaken?
- Is all of `lodash` imported instead of individual functions?

**E. Lazy Loading**
- Are large or below-the-fold components using `defineAsyncComponent` or `<LazyComponent>`?
- Are only the used Nuxt UI components being loaded?

**F. Images**
- Do all images go through `<NuxtImg>` or `<NuxtPicture>`?
- Is `@nuxt/image` listed in modules?
- For NuxtHub Blob images — are image transformations being used?

---

### 3. 📦 Build & Bundle

- Check `nuxt.config.ts` for `vite.build` settings
- Unused imports in any file
- Packages in `dependencies` that belong in `devDependencies` or vice versa
- Duplicate or conflicting modules
- Is `nuxt analyze` configured for bundle inspection?
- Does `build.transpile` contain unnecessary packages?

---

### 4. 🎯 Nuxt 4 Best Practices

**A. File Structure (app/ directory)**
- Is the project using the new `app/` directory?
- Are `pages/`, `components/`, `composables/`, `layouts/`, `middleware/` all inside `app/`?
- Are any files placed in the wrong location?

**B. Auto-imports**
- Are there manual imports for things Nuxt auto-imports automatically?
- Are composables prefixed with `use` so auto-import can detect them?

**C. Pages and Routing**
- Is `definePageMeta()` used correctly?
- Are dynamic route params validated?
- Is `<NuxtLink>` used instead of `<a>` everywhere?
- Are page transitions configured on `<NuxtPage>`?

**D. Data Fetching**
- Is the choice between `useFetch`, `useAsyncData`, and `$fetch` appropriate for each case?
- Do all fetch calls handle both `error` and `pending` states?
- Are `key` values in `useAsyncData` unique to avoid conflicts?
- Is `lazy: true` used where SSR does not need to wait for the data?

**E. Composables**
- Is each composable in `app/composables/` actually reused, or can it be simplified?
- Do composables handle lifecycle correctly (`onMounted`, `onUnmounted`)?
- Are there memory leaks (event listeners not removed, intervals not cleared)?

**F. Server Routes (NuxtHub)**
- Does every route in `server/api/` validate its input?
- Are `hubDatabase().prepare()` queries safe from SQL injection?
- Are error responses consistent and structured?
- Is caching configured for static or rarely-changing responses?

---

### 5. 🔷 Code Quality — JavaScript Focus

- Is ESLint configured with `@nuxt/eslint`?
- Does the ESLint config include Vue-specific rules?
- Is there duplicated logic that should be extracted into a composable?
- Are there leftover `console.log` or `console.error` calls?
- Are there magic numbers without named constants?
- Are there functions longer than 50 lines that should be split?
- Are variable names unclear (`data`, `res`, `temp`, `x`)?
- Is there commented-out code left behind?

**Vue-Specific:**
- Are props missing default values for non-required props?
- Are events undocumented (missing `defineEmits`)?
- Are watchers used where computed properties would be more appropriate?
- Is `v-for` used without a proper `:key`?
- Are props being mutated directly instead of emitting?

---

### 6. 🔍 SEO — Highest Priority

**A. Meta Tags**
- Does every page use `useSeoMeta()` correctly?
- Are `title` and `description` present and unique per page?
- Is the description between 150–160 characters?
- Are `ogTitle`, `ogDescription`, and `ogImage` set per page?
- Are `twitterCard`, `twitterTitle`, and `twitterImage` set?

**B. Structured Data**
- Is JSON-LD present with the appropriate schema (WebSite, Article, Organization, etc.)?
- Is `useSchemaOrg` used, or is JSON-LD written manually?

**C. Technical SEO**
- Is `@nuxtjs/sitemap` or equivalent configured for Nuxt 4?
- Is `robots.txt` present in `public/`?
- Are canonical URLs defined?
- Do dynamic routes generate correct pages for SSG or SSR?
- Is `error.vue` configured?

---

### 7. 🎨 Nuxt UI — Usage Review

- Is the theme in `app.config.ts` correctly and consistently configured?
- Are custom colors properly added to the theme?
- Are Nuxt UI components used correctly (`<UButton>`, `<UCard>`, etc.)?
- Are there unnecessary style overrides that break the design system?
- Is `darkMode` working correctly across all components?
- Is the `ui` prop used correctly for customization?
- Are there custom components that duplicate what Nuxt UI already provides?

---

### 8. ♿ Accessibility

- Does every image have a descriptive and appropriate `alt`?
- Do interactive elements (buttons, links) have `aria-label` when needed?
- Is there only one `<h1>` per page?
- Is the heading order logical (h1 → h2 → h3)?
- Is every `<input>` associated with a `<label>`?
- Can the site be navigated using only the keyboard?
- Are focus states clearly visible?

---

### 9. ❌ Error Handling

- Is `error.vue` present in `app/`?
- Does `error.vue` handle both 404 and 500 errors?
- Do all `useFetch` and `useAsyncData` calls handle the `error` state?
- Do server routes have try/catch and return consistent error responses?
- Is there a global error handling plugin?
- Does the user see a clear error message instead of a blank screen or crash?

---

### 10. 📊 Dependency Analysis

Inspect `package.json` and look for:
- Packages that are many major versions behind
- Unused packages
- Conflicting packages or duplicates solving the same problem
- Packages that should be in `devDependencies` but are in `dependencies`
- Nuxt modules that are incompatible with Nuxt 4

---

### 11. 🌍 Environment & NuxtHub Config

- Does `nuxt.config.ts` use the `hub: {}` configuration correctly?
- Are `hubDatabase`, `hubKV`, `hubBlob`, `hubCache` enabled only when used?
- Is `runtimeConfig` properly structured (secrets private, public only for frontend)?
- Does `.env.example` document every required variable?

---

## 📋 Issue Report Format

For every issue found, report it using this exact structure:

```
### [CATEGORY] — [SEVERITY] — [Short Issue Name]

**📍 Location:** `path/to/file.vue` line X

**❓ Problem:**
Clear and detailed description in Arabic.

**💥 Impact:**
What happens because of this issue? What is the effect on the user or project?

**🔬 How to verify manually:**
Step-by-step instructions the developer can follow to see the issue themselves:
1. Open ...
2. Click on ...
3. Notice that ...

**✅ Available Solutions:**

Solution 1 — [Name]:
[code or steps]

Solution 2 — [Name]:
[code or steps]

**⭐ Recommended solution for this project:**
Explain why this solution is the best fit, considering the project uses JavaScript (not TypeScript), Nuxt UI, and NuxtHub.

**🔗 References:**
- [Source Name](URL)
- [Source Name](URL)
```

**Severity Levels:**
- 🔴 **Critical** — Security vulnerability or issue that blocks functionality
- 🟠 **High** — Major impact on security or performance
- 🟡 **Medium** — Moderate impact on experience or code quality
- 🟢 **Low** — Minor improvement
- 💡 **Suggestion** — Optional enhancement

---

## 📊 Final Report

After completing all dimensions, write:

### Executive Summary
- **Overall Project Health Score:** X/100
- **Critical Issues 🔴:** X
- **High Issues 🟠:** X
- **Medium Issues 🟡:** X
- **Low Issues 🟢:** X
- **Suggestions 💡:** X

### Score Per Dimension
| Dimension | Score | Status |
|-----------|-------|--------|
| Security | X/10 | 🔴/🟠/🟡/🟢 |
| Performance | X/10 | |
| Build & Bundle | X/10 | |
| Nuxt 4 Practices | X/10 | |
| Code Quality | X/10 | |
| SEO | X/10 | |
| Nuxt UI | X/10 | |
| Accessibility | X/10 | |
| Error Handling | X/10 | |
| Dependencies | X/10 | |

### 🚨 Top 5 Issues to Fix Immediately
Ordered by priority with reason for urgency.

### ⚡ Quick Wins — Under 30 Minutes
Simple fixes with high impact.

### 🏗️ Long-Term Architecture Recommendations
Structural improvements for scalability and maintainability.

### ✅ Strengths
What is already working well in the project.

---

## 💾 Saving the Report

**Important — after completing the full report:**

Save the report as a Markdown file at:
```
audit/website-audit-[YYYY-MM-DD]-[HH-MM].md
```

Example: `audit/website-audit-2025-01-15-14-30.md`

- Create the `audit/` folder if it does not exist
- Use today's actual date and current time
- **Write the entire report in Arabic** — technical terms (useFetch, composables, hubDatabase, etc.) stay in English as-is
- Include all issues, recommendations, code examples, and references

---

## ⚙️ Hard Constraints — Always Follow These

1. **Never suggest TypeScript** for JavaScript files (composables, pages, components) — only for config files and utils
2. **Always use Nuxt UI components** in any solution that involves UI — do not suggest other UI libraries
3. **Always consider NuxtHub** for anything related to database, storage, and caching
4. **Nuxt 4 only** — do not suggest patterns that belong to Nuxt 3
5. **Prefer first-party solutions** using Nuxt built-ins before suggesting new packages
6. **Be specific** — every recommendation must reference a specific file and line number, not a general pattern
7. **Primary references:** Nuxt docs, Vue docs, Nuxt UI docs, NuxtHub docs

Start now by reading the project structure, then go through each dimension one by one.