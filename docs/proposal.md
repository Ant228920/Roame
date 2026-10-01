
ФІНАЛЬНА ПРОПОЗИЦІЯ (UA):

Roame — AI-керована вебплатформа автоматизованого планування подорожей та управління ресурсами на основі інтеграції LLM та комбінаторної оптимізації.
1. Проблематика
Індустрія TravelTech стикається з архітектурним розривом: ШІ-асистенти обробляють природномовні запити, але генерують логістично нереалізовні маршрути (AI hallucinations в плануванні). Платформи бронювання забезпечують транзакції ізольованих об'єктів, але не здійснюють маршрутизацію. Три класи проблем:
Узгодження стохастичної природи LLM із детермінованими просторово-часовими обмеженнями.
Висока обчислювальна складність оптимізації розкладів (NP-складна задача VRPTW).
Гетерогенність простору станів (уніфікація різнотипних послуг без структурного дублювання).
Складність полягає в ізоляції ресурсоємних математичних алгоритмів від транзакційного ядра при збереженні консистентності даних.
2. Ідея
Cloud-Native платформа на базі сервіс-орієнтованої архітектури (SOA). Система ізолює стохастичну обробку (векторний пошук через LLM) від детермінованих обчислень (CP-SAT solver). Взаємодія між веб'ядром та обчислювальними worker-ами відбувається асинхронно через брокери повідомлень.
3. Функціонал
Гібридний рекомендаційний рушій: Семантичний пошук кандидатів через PostgreSQL (pgvector) та векторні вбудовування.
Асинхронний математичний оптимізатор: Розв'язання задачі маршрутизації з часовими вікнами (VRPTW) фоновими worker-процесами для запобігання блокуванню Event Loop.
Універсальна підсистема управління ресурсами: Обробка транзакцій бронювання на базі моделі задоволення обмежень (CSP) з використанням компенсуючих транзакцій для складених маршрутів.
Геопросторова маршрутизація: Інтеграція Mapbox API для геокодування та розрахунку матриць відстаней.
RBAC та верифікація: JWT-авторизація для 3 ролей, транзакційна перевірка Proof-of-Visit для відгуків.
Асинхронні сповіщення (Chat Bot): Окремий мікросервіс для інформування про таймінги та статуси.
4. Архітектура
Service-Oriented Architecture (SOA) · Asynchronous Task Queue (Celery) · Vector Search (Embeddings) · Circuit Breaker (для зовнішніх API) · JWT Auth · Docs-as-Code.
5. Стек
Категорія
Технології
Мови
Python 3.11+, TypeScript
Backend
FastAPI, SQLAlchemy, Alembic
Frontend
React, Vite, TailwindCSS
Дані
PostgreSQL + pgvector, Redis
Оптимізація та AI
Google OR-Tools (CP-SAT), Google Gemini API
Інфраструктура
Docker, Docker Compose, GitHub Actions, Celery

6. Результати
Математична модель розподілу просторово-часових ресурсів.
CI/CD конвеєр із лінтерами та тестами.
Оптимізаційні метрики алгоритму порівняно з наївним підходом.
Документація OpenAPI та ADR (Architecture Decision Records).

FINAL PROPOSAL (EN):
Roame – An AI-Driven Web Platform for Automated Travel Planning and Resource Management Using Combinatorial Optimization.
1. Problem
The TravelTech industry faces an architectural gap: AI assistants handle natural language queries but generate logistically unfeasible itineraries (AI hallucinations in scheduling). Booking platforms ensure transactions for isolated objects but lack routing capabilities. Three problem classes:
Reconciling the stochastic nature of LLMs with deterministic spatio-temporal constraints.
High computational complexity of schedule optimization (the NP-hard VRPTW problem).
Heterogeneity of the state space (unifying various service types without structural duplication).
The complexity lies in isolating resource-intensive mathematical algorithms from the transactional core while maintaining data consistency.
2. Concept
A Cloud-Native platform based on Service-Oriented Architecture (SOA). The system isolates stochastic processing (vector search via LLM) from deterministic computations (CP-SAT solver). Communication between the web core and computational workers is asynchronous via message brokers.
3. Features
Hybrid Recommendation Engine: Semantic candidate search via PostgreSQL (pgvector) and embeddings.
Asynchronous Mathematical Optimizer: Solving the Vehicle Routing Problem with Time Windows (VRPTW) via background workers to prevent Event Loop blocking.
Universal Resource Management: Booking transaction processing based on the Constraint Satisfaction Problem (CSP) model, utilizing compensating transactions for composite itineraries.
Geospatial Routing: Mapbox API integration for geocoding and distance matrix calculations.
RBAC and Verification: JWT authorization for 3 roles; transactional Proof-of-Visit check for reviews.
Asynchronous Notifications (Telegram Bot): A decoupled microservice for timing and status alerts.
4. Architecture
Service-Oriented Architecture (SOA) · Asynchronous Task Queue (Celery) · Vector Search (Embeddings) · Circuit Breaker (for external APIs) · JWT Auth · Docs-as-Code.
5. Stack
Category
Technologies
Languages
Python 3.11+, TypeScript
Backend
FastAPI, SQLAlchemy, Alembic
Frontend
React, Vite, TailwindCSS
Data
PostgreSQL + pgvector, Redis
Optimization & AI
Google OR-Tools (CP-SAT), Google Gemini API
Infrastructure
Docker, Docker Compose, GitHub Actions, Celery

6. Deliverables
Mathematical model of spatio-temporal resource allocation.
CI/CD pipeline with linters and tests.
Optimization metrics of the algorithm compared to a naive approach.
OpenAPI documentation and ADR (Architecture Decision Records).
