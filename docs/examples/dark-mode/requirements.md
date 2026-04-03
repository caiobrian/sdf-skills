# Requirements: Dark Mode

## Functional Requirements

| ID | Requirement |
|----|-------------|
| RF-01 | The app must offer a toggle to switch between light and dark mode |
| RF-02 | The selected theme must persist across page reloads |
| RF-03 | System preference (`prefers-color-scheme`) must be used as the default when no preference is saved |
| RF-04 | All existing UI components must render correctly in both themes |

## Non-Functional Requirements

| ID | Requirement |
|----|-------------|
| RNF-01 | Theme switch must apply without a full page reload |
| RNF-02 | No flash of unstyled content (FOUC) on initial load |
| RNF-03 | Color contrast must meet WCAG AA (4.5:1 for text) in both themes |

## Edge Cases

| ID | Case |
|----|------|
| EC-01 | User clears localStorage — falls back to system preference |
| EC-02 | System preference changes while app is open — does not override user's explicit choice |
| EC-03 | Component renders before JS hydration — must not flash wrong theme |

## Acceptance Criteria

| ID | Criterion |
|----|-----------|
| CA-01 | Toggle in settings page switches theme immediately (RF-01, RNF-01) |
| CA-02 | Reloading the page preserves last selected theme (RF-02) |
| CA-03 | First visit with no saved preference matches OS theme (RF-03) |
| CA-04 | All components in Storybook pass visual regression in dark mode (RF-04) |
| CA-05 | No FOUC visible in Lighthouse trace (RNF-02) |
