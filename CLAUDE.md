# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm install      # Install dependencies
npm run dev      # Start dev server at http://localhost:5173
npm run build    # Production build
npm run preview  # Preview production build
npm run lint     # Run ESLint
```

No test framework is configured in this project.

## Architecture

This is a minimal React + Vite single-page app. All application logic lives in a single file:

- **`src/App.jsx`** — the entire app: state management, filtering logic, form handling, and rendering. No components are extracted; everything is in one monolithic `App` component.

### Known bugs (intentional, part of the course)

- Transaction `amount` values are stored as strings (not numbers), causing the income/expense totals to concatenate instead of sum correctly.
- "Freelance Work" in the seed data is marked `type: "expense"` but categorized as `"salary"` — it should be `type: "income"`.

### State shape

```js
transactions: [{ id, description, amount, type, category, date }]
// type: "income" | "expense"
// category: "food" | "housing" | "utilities" | "transport" | "entertainment" | "salary" | "other"
// amount: stored as string (bug)
```

All state is in-memory only — there is no persistence layer.
