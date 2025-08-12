---
layout: default
title: Building Global Apps - An Internationalization (i18n) Guide
description: "Best practices for building multilingual web applications."
---

# 🌐 Building Global AI Apps: An Internationalization (i18n) Guide

## 📋 Table of Contents

1. [Infrastructure](#infrastructure)
2. [Best Practices](#best-practices)
3. [Code Review](#code-review)
4. [Checklist](#checklist)

---

## Infrastructure

### 1. i18n Setup
- Check if an i18n framework is already integrated. If not, add i18n capabilities by integrating i18next.

### 2. String Files Structure
- Manage each language in a single string file `/public/locales/{language}/translation.json`

### 3. Sitemap
- Maintain a sitemap with the domain and routing to support separate language URLs, such as `/{language}/{page}`. For example: `/en/about`, `/es/about`, `/ar/about`, `/fr/about`

### 4. Pre-rendering Translation Check
- Translations must be loaded and ready before the first rendering.

### 5. Language Selector
- A dropdown language selector with: Display languages in their native names, avoid using flags as language indicators, disable the currently active language, update URL and user preferences on change and navigate other pages.


## Best Practices

### 1. Avoid String Concatenation
- **Bad:** `"Hello " + userName`.
- **Good:** Keep sentences intact and use placeholders: `t('greeting', { name: userName })`.

### 2. Pluralization and Count Handling
- Provide `_one`, `_other` (and language‑specific `_zero`, `_two`, `_few`, `_many`) keys.
- Pass `count` into your translation call: `t('item', { count })`.

### 3. Locale‑Specific Formatting
- Use Intl-based formatting (dates, numbers, currency) via placeholders: `{{ value, date }}`, `{{ value, number }}`.
- Rely on the user’s locale settings to format correctly (e.g., `31/12/2025` vs. `12/31/2025`).

### 4. Fallback Languages
- Auto‑detect user locale, but allow manual override via a language switcher.
- Always configure a real fallback language (e.g., English) so missing keys never display raw identifiers.

### 5. Right‑to‑Left (RTL) Language Support
- For proper RTL layout, ensure your CSS applies `direction: rtl;` when the page’s language attribute is one of the following languages: ks, yi, uz, he, fa, sd, lrc, ckb, ar, ur, ug, mzn, ps.

### 6. Placeholder Naming
- Use consistent, descriptive placeholder names (e.g., `{{userName}}` rather than `{{x}}`).

### 7. ICU Message Format
- Adopt ICU syntax when needing complex logic (select, plurals) in a single string.

### 8. Encoding
- Always serve content in UTF‑8.

### 9. Language Selector
- Don’t include a flag in the language selector, because a flag represent a region but not a language

---

## Code Review

Only fix i18n-related code, do not change anything else.

### 1. Hard‑coded Strings
- Scan the project for any hard‑coded UI strings not passed through your i18n function.

### 2. Pluralization Check
- Identify manual plural logic and suggest replacing with library plural forms (`_one`, `_other`).

### 3. Formatting Audit
- Review number, date, and currency formatting. Are locale‑aware formats used?

### 4. RTL Verification
- Detect pages displaying in LTR when the language attribute is set to an RTL language. Ensure CSS `direction: rtl` is applied.

### 5. Placeholder Consistency Check
- Verify that placeholder names in translation strings match those used in code, and flag any mismatches.

### 6. Missing Translation Keys
- Scan for missing translation keys in resource files and suggest adding them to the appropriate locale files.

---

## Checklist
Respond with a summary and a checklist indicating which tasks above are completed.
