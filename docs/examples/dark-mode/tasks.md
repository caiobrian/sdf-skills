# Tasks: Dark Mode

## Wave 1 — Foundation (parallel)

### T-01: ThemeProvider and useTheme hook

**Requirements:** RF-02, RF-03, EC-01, EC-02
**Files:** `src/context/ThemeContext.tsx`, `src/hooks/useTheme.ts`

Implement `ThemeProvider` that:
- Reads `localStorage.getItem("theme")` on mount
- Falls back to `window.matchMedia("(prefers-color-scheme: dark)").matches` (EC-01)
- Sets `document.documentElement.dataset.theme` whenever theme changes
- Does NOT listen for OS preference changes after user has set an explicit choice (EC-02)
- Persists choice to `localStorage` on every change (RF-02)

Implement `useTheme()` that throws a descriptive error if used outside `ThemeProvider`.

### T-02: Tailwind dark mode config

**Requirements:** RF-04, RNF-03
**Files:** `tailwind.config.ts`

Update `darkMode` to `["attribute", "[data-theme=dark]"]`.
Run `pnpm build` to confirm no compilation errors.

---

## Wave 2 — UI (depends on T-01)

### T-03: ThemeToggle component

**Requirements:** RF-01, CA-01
**Files:** `src/components/ThemeToggle.tsx`

Button that:
- Calls `setTheme("dark")` / `setTheme("light")` based on current value
- Shows a sun icon in dark mode, moon icon in light mode (use existing icon set)
- Has `aria-label` that reflects current action ("Switch to dark mode" / "Switch to light mode")

---

## Wave 3 — Integration (depends on T-01, T-02, T-03)

### T-04: Mount provider and FOUC prevention script

**Requirements:** RNF-02, EC-03
**Files:** `src/app/layout.tsx`

1. Wrap children with `<ThemeProvider>`
2. Add inline `<script>` in `<head>` (before any stylesheets) that reads `localStorage.theme` and sets `document.documentElement.dataset.theme` synchronously. Script must be self-contained (no imports).

### T-05: Add ThemeToggle to Settings page

**Requirements:** RF-01, CA-01
**Files:** `src/app/settings/page.tsx`

Import and render `<ThemeToggle />` in the Appearance section of the settings page. Add a visible label: "Theme".

---

## Completed

- [x] T-01
- [x] T-02
- [ ] T-03
- [ ] T-04
- [ ] T-05
