# ✅ Загальний підхід до іменування

### Формат файлу:
```
<feature>.<role>.ts
```

- **feature** — що описує файл (наприклад: `email`, `user`, `auth`)
- **role (або suffix)** — яка роль цього файлу (`service`, `adapter`, `types`, `guard` тощо)

---

## 📂 Категорії і приклади

### 1. Adapter

- `email.adapter.ts`
- ✅ Коли: адаптуєш зовнішній API/SDK/бібліотеку під внутрішній інтерфейс  
- 🧠 Реалізує патерн Adapter (Wrapper над SendGrid, EmailJS тощо)

---

### 2. Abstract клас

- `auth.abstract.ts`, `base.abstract.ts`
- ✅ Коли: базовий клас, який буде наслідуватися  
- 🔍 Альтернатива: `base-*.ts` (наприклад: `base-http.service.ts`)
- 🔑 Має містити `abstract` у класі

```ts
export abstract class AuthStrategy {
  abstract login(...): void;
}
```

---

### 3. Типи / Інтерфейси / DTO

| Роль         | Назва файлу         | Коментар                                         |
|--------------|---------------------|--------------------------------------------------|
| Типи         | `user.types.ts`     | Кілька типів або об'єднань типів                 |
| Інтерфейси   | `user.interfaces.ts`| Якщо хочеш розділити інтерфейси окремо          |
| DTO          | `user.dto.ts`       | Для структур даних у транспорті                  |
| Моделі       | `user.model.ts`     | Класи з методами                                 |

🔹 **Рекомендація:** використовуй `types.ts` у більшості випадків. Якщо дуже багато — окремо `interfaces.ts`.

---

### 4. Utils / Helpers

- `date.utils.ts`, `form.helpers.ts`
- ✅ Для чистих функцій (`formatDate`, `debounce`, `calculateAge`)
- ❗ Уникай бізнес-логіки

---

### 5. Service

- `auth.service.ts`, `user.service.ts`
- ✅ Інкапсуляція бізнес-логіки або роботи з API
- 🔸 Якщо звертається до бекенду → `*.api.ts` (див. нижче)

---

### 6. API / Client

- `user.api.ts`, `payment.client.ts`
- ✅ Для REST/gRPC/GraphQL/Firebase викликів
- 🔄 Можна зберігати у `/api/`

---

### 7. Component (React або Angular)

| Роль     | React                  | Angular                       |
|----------|------------------------|-------------------------------|
| Компонент | `UserCard.tsx`         | `user-card.component.ts`      |
| Тести    | `UserCard.test.tsx`    | `user-card.component.spec.ts` |
| Стилі    | `UserCard.module.scss` | `user-card.component.scss`    |

🔹 У React — PascalCase, в Angular — kebab-case.

---

### 8. Hooks (React)

- `useForm.hook.ts` або `useForm.ts`
- ✅ Починається з `use*`
- 🔍 Для некомпонентної логіки

---

### 9. Store / State

- `user.store.ts`, `user.slice.ts`, `user.state.ts`
- ✅ Для управління локальним/глобальним станом (Redux, Zustand, NGXS тощо)

---

### 10. Mocks / Fixtures

- `user.mocks.ts`, `test-fixtures.ts`
- ✅ Для тестових даних

---

### 11. Factories

- `user.factory.ts`
- ✅ Генерація об’єктів (часто з `faker.js`, `test-data-bot`)

---

### 12. Constants

- `auth.constants.ts`, `validation.constants.ts`
- ✅ Стабільні значення: ролі, regex, enum-like обʼєкти

---

### 13. Guards / Middleware

- `auth.guard.ts`, `auth.middleware.ts`
- ✅ `Guard` — Angular / NestJS  
- ✅ `Middleware` — бекенд, Express тощо

---

### 14. Pipes

- `date.pipe.ts`, `capitalize.pipe.ts`
- ✅ Angular `@Pipe` або NestJS `ValidationPipe`

---

## 📦 Рекомендована структура (Feature-first)

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

## 🧨 Уникай

| Погана практика | Чому погано                             |
|-----------------|------------------------------------------|
| `utils.ts`       | Неочевидно, що всередині                |
| `index.ts`       | Якщо все в одному — буде роздутий файл |
| `data.ts`        | Непрозоре ім’я — незрозумілий вміст    |
| `common.ts`      | Те саме — що саме в ньому "common"?    |

---

## ✅ Підсумок

| Сутність     | Формат файлу                   |
|--------------|--------------------------------|
| Adapter      | `feature.adapter.ts`           |
| Abstract     | `feature.abstract.ts`          |
| Типи         | `feature.types.ts`             |
| Інтерфейси   | `feature.interfaces.ts`        |
| DTO          | `feature.dto.ts`               |
| Utils        | `feature.utils.ts`             |
| Helpers      | `feature.helpers.ts`           |
| Service      | `feature.service.ts`           |
| API Client   | `feature.api.ts`               |
| Store        | `feature.store.ts` / `state.ts`|
| Hook         | `useFeature.hook.ts`           |
| Guard        | `feature.guard.ts`             |
| Pipe         | `feature.pipe.ts`              |
| Constants    | `feature.constants.ts`         |
| Mocks        | `feature.mocks.ts`             |
| Component    | `FeatureComponent.tsx` / `feature.component.ts` |
