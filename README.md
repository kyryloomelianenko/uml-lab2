# UML Lab Work 2  
## DishGuide

---

## Опис проєкту

DishGuide — це система рекомендацій страв у ресторанах на основі відгуків користувачів.

---

## Functional Requirements

| ID | Опис |
|----|------|
| FR-01 | Користувач може шукати ресторани |
| FR-02 | Користувач може шукати ресторани за місцем розташування |
| FR-03 | Користувач може переглядати рекомендовані страви |
| FR-04 | Користувач може переглядати рейтинг ресторану |
| FR-05 | Користувач може фільтрувати ресторани за кухнею |
| FR-06 | Користувач може переглядати профіль ресторану |
| FR-07 | Система надає рекомендації страв на основі відгуків |

---

## Use Case Diagram

```mermaid
flowchart LR

User((User))
Admin((Admin))

subgraph System[DishGuide System]

UC1[Пошук ресторану]
UC2[Пошук за локацією]
UC3[Перегляд рекомендацій]
UC4[Перегляд рейтингу]
UC5[Фільтрація за кухнею]
UC6[Перегляд профілю ресторану]
UC7[Аналіз відгуків]

end

User --> UC1
User --> UC2
User --> UC3
User --> UC4
User --> UC5
User --> UC6

Admin --> UC7

UC3 -->|<<include>>| UC7
```

---

## Class Diagram

```mermaid
classDiagram

class User {
  -id : int
  -name : String
  +searchRestaurant()
}

class Restaurant {
  -id : int
  -name : String
  -location : String
  -rating : float
  +getDetails()
}

class Dish {
  -id : int
  -name : String
  -price : double
}

class Review {
  -text : String
  -rating : int
}

class RecommendationService {
  +getRecommendations()
}

class Filter {
  +filterByCuisine()
}

User --> Restaurant
Restaurant --> Dish
Restaurant --> Review
RecommendationService --> Dish
RecommendationService --> Review
User --> Filter
```

---

## Sequence Diagram

```mermaid
sequenceDiagram

participant User
participant System
participant RecommendationService
participant Restaurant
participant Review

User ->> System: selectRestaurant()
System ->> Restaurant: getDetails()

System ->> RecommendationService: getRecommendations()

RecommendationService ->> Review: analyzeReviews()
Review -->> RecommendationService: reviewsData

RecommendationService -->> System: dishList
System -->> User: recommendations
```

---

## Traceability Matrix

| Functional Requirement | Use Case | Classes | Sequence Diagram |
|----------------------|----------|--------|------------------|
| FR-01 | Пошук ресторану | User, Restaurant | ✔ |
| FR-02 | Пошук за локацією | User, Restaurant | — |
| FR-03 | Перегляд рекомендацій | User, RecommendationService | ✔ |
| FR-04 | Перегляд рейтингу | User, Review | — |
| FR-05 | Фільтрація за кухнею | User, Filter | — |
| FR-06 | Перегляд профілю ресторану | User, Restaurant | — |
| FR-07 | Аналіз відгуків | RecommendationService, Review | ✔ |
