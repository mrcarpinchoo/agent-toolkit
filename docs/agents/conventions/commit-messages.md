# Commit Messages

Conventional commits, with a few refinements.

## Format

```
<type>(<scope>): <subject>

<body>
```

## Type

Common types: `feat`, `fix`, `refactor`, `chore`, `docs`, `test`, `perf`, `style`, `build`, `ci`. Use whichever genuinely fits the change; don't force one that doesn't apply.

## Scope

Freeform, not a fixed list, a lowercase word for the domain or module most affected (e.g. `auth`, `billing`, `search`). Pick one consistent name per domain and stick with it across commits (don't alternate between a singular domain name and a plural/route-based one, e.g. `user` vs `users` vs `api`, pick one and use it everywhere).

Include a scope whenever a commit is clearly about one domain. Omit it only when a change is genuinely cross-cutting and naming one scope would be misleading (e.g. `chore: update dev tooling config`).

## Subject

- Imperative mood: "add", "allow", "return", not "added"/"allows"/"returns"
- No trailing period
- One line, concise enough to stand alone

## Body

Only include a body if the change needs more explanation than the subject line gives, a multi-part feature, a non-obvious fix rationale, a behavior or business rule worth calling out. Skip it for small, self-explanatory changes; a good `type(scope): subject` line is enough on its own.

When a body is included:

- Use bullet points (`-`), one point per line (wrap long ones, indented).
- Each bullet explains the _why_ or the resulting behavior, not a mechanical list of which files or functions changed. The diff already shows what changed; the commit message should carry what the diff can't.

## Standing rules

- Never add a `Co-Authored-By` trailer.
- Never use em dashes, in the subject or the body.
- Never include non-English text in commit messages, even quoted UI copy. Describe it generically in English instead (e.g. "the saved-items card" rather than quoting a localized label).
- Always show the composed commit message and wait for explicit approval before running `git commit`. This applies every time, even immediately after being told to "commit" or "let's commit now", showing the message is not itself permission to proceed.

## Examples

### Good: body warranted, bullets carry the why

```
feat(billing): allow editing invoice due date via PATCH /invoices/:id

- Add dueDate to UpdateInvoiceRequest/UpdateInvoiceResult and wire
  it through updateInvoice, following the same optional-field,
  empty-string-clears pattern as description
- Validate dueDate as an optional ISO 8601 date, must be in the future
- Closes the gap where dueDate was already readable everywhere but
  had no way to be set
```

```
fix(auth): return 422 with errors[] for signup validation failures

- Registration previously returned 400 with { error, details } while
  every other endpoint uses 422 with { success: false, errors: string[] }
- Update the route JSDoc to match
```

### Good: subject alone is enough, no body

```
docs(spec-kit): add spec, plan, and tasks for invoice due dates
```

### Avoid: prose paragraph plus a redundant file-by-file "Changes:" list

This restates the diff instead of explaining the reasoning, and duplicates itself (a paragraph, then a bulleted list saying the same thing again):

```
feat(catalog): add category management endpoints

Allows sellers to add and remove categories from their profile via
POST and DELETE /api/v1/sellers/me/categories/:categoryId. Enforces
a maximum of 5 categories, prevents duplicates, and validates that
the category exists. Both endpoints return the updated category list.

Changes:
- Add SellerCategoryEntry DTO and categories field to SellerProfileData.
- Add SellerService.addCategory and removeCategory methods.
- Update SellerService.getMyProfile to include categories.
- Add SellerController.addCategory and removeCategory handlers.
- Register POST and DELETE /me/categories/:categoryId routes.
```

A version following the convention above would instead be:

```
feat(catalog): add category management endpoints

- Add and remove categories via POST/DELETE /me/categories/:categoryId
- Cap at 5 categories per seller, reject duplicates and unknown category IDs
- GET /me now includes the categories array
```

### Avoid: inconsistent scope naming

Alternating between a domain scope and a route/plural form makes history harder to scan:

```
fix(sellers): expose account ID in seller list response
feat(api): add /api/v1/sellers route
```

Pick one consistent scope (`seller`) and use it everywhere.
