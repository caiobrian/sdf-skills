# Plan: Dark Mode

## Types and Interfaces

```typescript
type Theme = "light" | "dark";

interface ThemeContextValue {
  theme: Theme;
  setTheme: (theme: Theme) => void;
}
```

## Storage

- Key: `"theme"` in `localStorage`
- Values: `"light"` | `"dark"`
- Fallback: `window.matchMedia("(prefers-color-scheme: dark)").matches`

## Strategy

1. **ThemeProvider** — wraps the app, reads from localStorage on mount, exposes context
2. **useTheme()** — hook that consumes ThemeContextValue; throws if used outside provider
3. **CSS approach** — `data-theme` attribute on `<html>`; Tailwind `darkMode: ["attribute", "[data-theme=dark]"]`
4. **FOUC prevention** — inline script in `<head>` reads localStorage and sets `data-theme` before React hydrates (no module bundler dependency)

## File Map

| File | Role |
|------|------|
| `src/context/ThemeContext.tsx` | Provider + context definition |
| `src/hooks/useTheme.ts` | Consumer hook |
| `src/components/ThemeToggle.tsx` | Toggle button UI |
| `src/app/layout.tsx` | Mount provider, inject FOUC script |
| `tailwind.config.ts` | Update `darkMode` strategy |

## Constraints

- No new dependencies — Tailwind already in project
- No server-side rendering for theme value (hydration mismatch risk)
