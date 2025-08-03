---
layout: default
title: i18n Best Practices
description: "Organized i18n best practices and i18next-specific guidelines for AI-powered code reviews"
---

# 🌐 Internationalization (i18n) Best Practices

Welcome to the **i18n Best Practices** guide, organized for GitHub Pages. This repository contains two main sections:

- [General i18n Best Practices](#general-i18n-best-practices)
- [i18next-Specific Best Practices](#i18next-specific-best-practices)

---

## 📋 Table of Contents

1. [General i18n Best Practices](#general-i18n-best-practices)
2. [i18next-Specific Best Practices](#i18next-specific-best-practices)
3. [Example AI Prompts for Code Review](#example-ai-prompts-for-code-review)

---

## General i18n Best Practices

### 1. Avoid String Concatenation
- **Bad:** `"Hello " + userName`
- **Good:** Use full sentences with placeholders: `t('greeting', { name: userName })`.

### 2. Pluralization and Count Handling
- Provide `_one` and `_other` keys.
- Pass `count` to `t()` to select the right form.

### 3. Locale-Specific Formatting
- Use Intl formatting via i18next: `{{value, formatName}}`.
- Rely on locale-aware date, number, and currency formats.

### 4. Fallback Languages
- Set `fallbackLng` to a real language (e.g., `'en'`).
- Configure `fallbackNS` for shared namespaces.

### 5. Provide Context
- Use distinct keys or i18next `context` feature for gender, formality.

### 6. UI/UX Considerations
- Auto-detect and allow users to override locale.
- Design for text expansion and RTL support.
- Use Unicode fonts and avoid in-string HTML.

---

## i18next-Specific Best Practices

### 1. Configuration
```js
i18next.init({
  lng: userLang,
  supportedLngs: ['en', 'es', 'de'],
  fallbackLng: ['en'],
  ns: ['common', 'featureA'],
  defaultNS: 'common',
  fallbackNS: 'common',
  keySeparator: '.',
  nsSeparator: ':'
});
```

### 2. Organizing Resources
- Use **namespaces** (e.g., `common.json`, `validation.json`).
- Lazy-load per feature or page to reduce bundle size.

### 3. Interpolation & Escaping
- Default: `escapeValue: true` to prevent XSS.
- Only disable (`{{- var}}` or `escapeValue:false`) for trusted HTML.

### 4. Missing Translations
- Enable `saveMissing: true` in dev to collect keys.
- Use `cimode` or custom handlers to spot missing strings.
- Set `returnEmptyString: false` to treat `""` as missing.

### 5. Advanced Features
- **Nesting:** `"welcome": "Welcome to $t(terms.appName)!"`
- **Context + Plural:** Combine `context` and `count` for gendered plurals.
- **Backends & Caching:** Chain backends and cache translations for performance.

---

## Example AI Prompts for Code Review

- **Hard-coded Strings:**  
  > "Scan my project for any hard-coded UI strings not passed through i18next."

- **Configuration Review:**  
  > "Analyze this i18next.init config. Are `fallbackLng`, `supportedLngs`, and `escapeValue` set correctly?"

- **Pluralization Check:**  
  > "Review pluralization usage. Are there manual count checks instead of `_one`/`_other` keys?"

- **Concatenation Issues:**  
  > "Find instances of string concatenation for UI text and suggest using translation placeholders."

- **XSS Safety:**  
  > "Verify no unescaped interpolation (`escapeValue:false`) with user input to prevent XSS."

---

*This page is auto-generated and maintained for AI-powered i18n code reviews.*
