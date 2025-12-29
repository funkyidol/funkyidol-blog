---
title: "Design system rebuild with Tailwind"
date: 2025-11-30
summary: "Rebuilt a component library with tokens, theming, and accessibility baked in, backed by visual regression tests."
draft: false
tags: ["design-system", "tailwind", "storybook"]
---

## Problem

Legacy UI components were inconsistent across products, lacked accessibility guarantees, and slowed delivery of new features.

## Approach

- Established design tokens (color, typography, spacing) synchronized with Tailwind config and Figma styles.
- Authored composable components with ARIA patterns, keyboard support, and dark-mode theming.
- Documented usage in Storybook with controls, MDX examples, and embedded accessibility checks.
- Added Chromatic visual regression tests and lint rules to enforce token usage.

## Outcome

- Reduced net-new feature UI build time by ~30% through reusable components.
- Consistent WCAG AA compliance verified in CI for every component story.
- Teams ship dark/light themes with zero runtime toggles and minimal CSS churn.
