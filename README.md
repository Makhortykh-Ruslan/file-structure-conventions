# ✅ Naming Convention Guide

### File format:
```
<feature>.<role>.ts
```

- **feature** — what the file describes (e.g., `email`, `user`, `auth`)
- **role** (or suffix) — the file's responsibility (e.g., `service`, `adapter`, `types`, `guard`)

---

## 📂 Categories & Examples

### 1. Adapter

- `email.adapter.ts`
- ✅ When: adapting an external API/SDK/library to an internal interface  
- 🧠 Follows the Adapter pattern (e.g., wrapper for SendGrid, EmailJS)

---

### 2. Abstract Classes

- `auth.abstract.ts`, `base.abstract.ts`
- ✅ When: it's a base class intended for inheritance  
- 🔍 Alternative: `base-*.ts` (e.g., `base-http.service.ts`)
- 🔑 Must include the `abstract` keyword

```ts
export abstract class AuthStrategy {
  abstract login(...): void;
}
```

---

### 3. Types / Interfaces / DTOs

| Role        | File name            | Notes                                             |
|-------------|----------------------|---------------------------------------------------|
| Types       | `user.types.ts`      | For multiple types or unions                     |
| Interfaces  | `user.interfaces.ts` | If you want to split interfaces separately        |
| DTOs        | `user.dto.ts`        | For transport-specific data structures            |
| Models      | `user.model.ts`      | For classes with logic/methods                   |

🔹 **Recommendation:** use `types.ts` in most cases. If it grows large — split into `interfaces.ts`.

---

### 4. Utils / Helpers

- `date.utils.ts`, `form.helpers.ts`
- ✅ For pure functions (`formatDate`, `debounce`, `calculateAge`)
- ❗ Avoid business logic here

---

### 5. Service

- `auth.service.ts`, `user.service.ts`
- ✅ Encapsulates business logic or interactions with APIs
- 🔸 If calling backend — use `*.api.ts` (see next)

---

### 6. API / Client

- `user.api.ts`, `payment.client.ts`
- ✅ For REST/gRPC/GraphQL/Firebase calls
- 🔄 Can live in a separate `/api` folder

---

### 7. Component (React or Angular)

| Role       | React                | Angular                         |
|------------|----------------------|----------------------------------|
| Component  | `UserCard.tsx`       | `user-card.component.ts`         |
| Test       | `UserCard.test.tsx`  | `user-card.component.spec.ts`    |
| Styles     | `UserCard.module.scss` | `user-card.component.scss`    |

🔹 React usually uses **PascalCase**, Angular uses **kebab-case**.

---

### 8. Hooks (React)

- `useForm.hook.ts` or `useForm.ts`
- ✅ Should start with `use*`
- 🔍 For reusable, non-component logic

---

### 9. Store / State

- `user.store.ts`, `user.slice.ts`, `user.state.ts`
- ✅ For managing local/global state (Redux, Zustand, NGXS, etc.)

---

### 10. Mocks / Fixtures

- `user.mocks.ts`, `test-fixtures.ts`
- ✅ For mock test data

---

### 11. Factories

- `user.factory.ts`
- ✅ For generating objects (often used with `faker`, `test-data-bot`)

---

### 12. Constants

- `auth.constants.ts`, `validation.constants.ts`
- ✅ For stable values: roles, regex, enums

---

### 13. Guards / Middleware

- `auth.guard.ts`, `auth.middleware.ts`
- ✅ Guard — used in Angular or NestJS  
- ✅ Middleware — used in backend / Express apps

---

### 14. Pipes

- `date.pipe.ts`, `capitalize.pipe.ts`
- ✅ Angular `@Pipe` or NestJS `ValidationPipe`

---

## 📦 Recommended Structure (Feature-first)

```
features/
└── user/
    ├── user.api.ts
    ├── user.service.ts
    ├── user.types.ts
    ├── user.adapter.ts
    ├── user.utils.ts
    ├── user.mocks.ts
    ├── UserProfile.component.tsx
    ├── useUser.hook.ts
    └── __tests__/
        └── user.service.test.ts
```

---

## 🧨 Avoid

| Bad practice  | Why it's bad                                |
|---------------|---------------------------------------------|
| `utils.ts`     | Too generic — unclear what's inside         |
| `index.ts`     | Easily bloated and hard to maintain         |
| `data.ts`      | Vague name — lacks clarity                  |
| `common.ts`    | Ambiguous — what exactly is “common”?       |

---

## ✅ Summary

| Entity       | File format                          |
|--------------|---------------------------------------|
| Adapter      | `feature.adapter.ts`                 |
| Abstract     | `feature.abstract.ts`                |
| Types        | `feature.types.ts`                   |
| Interfaces   | `feature.interfaces.ts`              |
| DTO          | `feature.dto.ts`                     |
| Utils        | `feature.utils.ts`                   |
| Helpers      | `feature.helpers.ts`                 |
| Service      | `feature.service.ts`                 |
| API Client   | `feature.api.ts`                     |
| Store        | `feature.store.ts` / `feature.state.ts` |
| Hook         | `useFeature.hook.ts`                 |
| Guard        | `feature.guard.ts`                   |
| Pipe         | `feature.pipe.ts`                    |
| Constants    | `feature.constants.ts`               |
| Mocks        | `feature.mocks.ts`                   |
| Component    | `FeatureComponent.tsx` / `feature.component.ts` |
