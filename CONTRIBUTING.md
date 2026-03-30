# Nestera Contributing Guide

Welcome! Thank you for your interest in contributing to Nestera. We appreciate all contributions, from code fixes to documentation improvements.

Follow this guide to ensure your contributions are effective and aligned with project standards.

## 🚀 Getting Started

1. **Read the [README.md](README.md)** for setup (Rust, Soroban CLI, Node.js, contracts/backend/frontend).
2. **Fork the repository** and clone your fork.
3. **Install dependencies** and run `cargo check` / `npm install` as per README.
4. **Create a feature branch** (see Git Workflow).

## 📏 Coding Standards

### Rust / Soroban Contracts (`contracts/`)
- **Formatting:** `cargo fmt` (always run before commit).
- **Linting:** `cargo clippy -- -D warnings`.
- **Style:**
  - Use `no_std`, Soroban SDK patterns.
  - `Check-effects-interact`: Validate first, mutate storage, emit events.
  - Math: `checked_add/sub/mul` for i128 to prevent overflow.
  - Invariants: Use `invariants::assert_non_negative`, fee bounds.
  - Storage: Extend TTL after writes (see [SOROBAN_STORAGE.md](contracts/docs/SOROBAN_STORAGE.md)).
  - Errors: `SavingsError` enum, `panic_with_error!`.
- **Testing:** `cargo test` – unit/integration, cover edge cases (TTL, fees, maturity).
- **Build:** `cargo build --target wasm32-unknown-unknown --release`.

### TypeScript / NestJS (`backend/`) & Next.js (`frontend/`)
- **Formatting:** ESLint + Prettier (configs provided).
- **Linting:** `eslint . --fix`, `prettier --write .`.
- **Standards:** Async/await, type-safe (DTOs, guards), filters (HTTP exceptions).

### General
- **Conventional Commits:** `feat: add group save`, `fix: ttl overflow`, `docs: update guide`, `chore: fmt`.
- **Tests:** 100% coverage for new features/fixes.

## 🗂️ Naming Conventions

| Language | Variables/Params | Functions/Methods | Structs/Types | Constants |
|----------|------------------|-------------------|---------------|-----------|
| **Rust** | `snake_case` | `snake_case` | `PascalCase` | `SCREAMING_SNAKE_CASE` |
| **TS** | `camelCase` | `camelCase` | `PascalCase` | `UPPER_SNAKE_CASE` |
| **Symbols** (Soroban) | Short: `user`, `dep`, `rate` | - | - | - |
| **Keys** (DataKey) | Descriptive enums: `UserGroupSaves(Address)` | - | - | - |
| **Branches/PRs** | `feat/group-ui`, `fix/ttl-bug` | - | - | - |

**Examples:**
```rust
// Good
pub fn deposit_to_goal_save(env: Env, user: Address, goal_id: u64, amount: i128)

// Avoid
pub fn Deposit(user, id, amt)  // Wrong case, short names
```

## 🔀 Git Workflow

1. **Branch from `main`:** `git checkout -b feat/your-feature`.
2. **Keep history clean:** Small, focused commits.
3. **Rebase before PR:** `git rebase main`.
4. **Push:** `git push origin feat/your-feature`.

**Branch Naming:** `feat/`, `fix/`, `docs/`, `refactor/`, `test/`, `chore/`.

## 🔄 Pull Request Process

1. **Push branch** and open PR against `main`.
2. **PR Template Requirements:**
   ```
   **Description:** What/why.
   **Related Issue:** #123
   **Changes:** - List
   **Tests:** Added/updated
   **Screenshots:** (UI)
   ```
3. **Checks:**
   - [ ] `cargo fmt --check` / `prettier --check`.
   - [ ] `cargo test` / `npm test` pass.
   - [ ] No merge conflicts.
   - [ ] CI green (if setup).
4. **Review Process:**
   - Assign reviewers (or `@maintainer`).
   - Address feedback in new commits.
   - Squash/rebase on approval.
5. **Merge:** Squash & merge with conventional commit title.

**Labels:** `status/ready`, `type/feat`, `area/contracts`.

## 📚 Additional Resources

- [Soroban Storage Design](contracts/docs/SOROBAN_STORAGE.md)
- [Governance Docs](contracts/GOVERNANCE.md)
- [Rust Soroban Docs](https://soroban.stellar.org/docs)
- Issues: [Good first issue](https://github.com/issues?q=is:issue+is:open+label:"good+first+issue")

## 🤝 Code of Conduct

Follow the [Contributor Covenant](https://www.contributor-covenant.org/version/2/1/code_of_conduct/).

Happy contributing! 🎉

