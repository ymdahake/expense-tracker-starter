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

This is a minimal React + Vite single-page app. The `transactions` array is the only shared state and lives in `App`. It flows down as props; nothing is lifted back up except via callbacks.

### Component tree

```
App                          — holds transactions state, passes it down
├── Summary                  — receives transactions, computes totals internally
├── TransactionForm          — owns its own form state, calls onAdd(transaction) to add
└── TransactionList          — receives transactions, owns filter state internally
```

### Known bug (intentional, part of the course)

- "Freelance Work" in the seed data is marked `type: "expense"` but categorized as `"salary"` — it should be `type: "income"`.

### State shape

```js
transactions: [{ id, description, amount, type, category, date }]
// type: "income" | "expense"
// category: "food" | "housing" | "utilities" | "transport" | "entertainment" | "salary" | "other"
// amount: number
```

All state is in-memory only — there is no persistence layer.
