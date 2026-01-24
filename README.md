# Flutter • Clean Architecture + GetX (Feature-first)

This repository is a **learning project** focused on applying **Clean Architecture** in Flutter using **GetX** for:

- State management (Controllers)
- Dependency injection (Bindings)
- Navigation (Routes)

The project follows a **feature-first** organization, aiming for scalability, clear boundaries, and testability.

---

## ✅ Goals

- Practice Clean Architecture separation:
  - **Domain** = business rules (pure Dart)
  - **Data** = implementations and external access
  - **Presenter** = UI + GetX (Controllers/Bindings/Views)
- Keep **GetX isolated** from domain rules
- Make features easy to add without breaking others
- Build code that looks and behaves like production code

---

## 🗂️ Current Structure

lib/
├── core/
│ ├── app/
│ │ └── app.dart
│ ├── config/
│ │ └── service/
│ │ ├── utils_service.dart
│ │ └── validator.dart
│ ├── constants/
│ │ ├── colors/
│ │ │ └── app_colors.dart
│ │ └── endpoints/
│ │ ├── auth_endpoints/
│ │ │ └── auth_endpoints.dart
│ │ └── user_endpoints/
│ │ └── user_endpoints.dart
│
├── features/
│ ├── data/
│ │ ├── datasource/
│ │ ├── model/
│ │ └── repository/
│ │
│ ├── domain/
│ │ ├── datasource/
│ │ ├── entities/
│ │ ├── infra/adapter/
│ │ ├── repository/
│ │ └── usecase/
│ │
│ ├── infra/
│ │ └── (shared infra implementations / adapters)
│ │
│ ├── presenter/
│ │ ├── entity/
│ │ ├── interfaces/
│ │ ├── auth/
│ │ │ ├── binding/
│ │ │ ├── controller/
│ │ │ └── view/
│ │ ├── home/
│ │ └── splash/
│ │ └── view/
│ │
│ └── shareds/
│ └── common_widgets/
│ ├── animations/
│ └── atom/
│
├── shareds/
│ ├── common_widgets/
│ │ ├── animations/
│ │ └── atom/
│ └── routes/
│
├── main.dart
└── generated_plugin_registrant.dart


---

## 🧠 Layer Responsibilities

### Domain (pure Dart)
- Entities (business objects)
- Usecases (application rules)
- Repository contracts (interfaces)

✅ **Must not depend on Flutter or GetX**.

### Data
- Models (DTOs)
- Datasources (API/local)
- Repository implementations

✅ Depends on Domain contracts.

### Presenter (GetX lives here)
- Views (pages/widgets)
- Controllers (state + orchestration)
- Bindings (dependency injection)
- Routes navigation integration

✅ Can depend on Domain usecases.

---

## 🔁 Typical Flow (UI → Domain → Data)

1. **View** triggers an action (button, init, etc.)
2. **Controller** calls a **Usecase**
3. Usecase calls a **Repository contract**
4. **Repository implementation** (Data) hits datasource (API/local)
5. Result returns back up to Controller → updates UI

---

## 🧩 GetX Usage Guidelines (what I’m practicing here)

- Controllers should be **thin**
  - orchestration + state only
  - no DTO parsing, no API calling directly
- Bindings define dependencies per feature
- Navigation is centralized (routes folder)

---

## ▶️ Running the project

```bash
flutter pub get
flutter run
