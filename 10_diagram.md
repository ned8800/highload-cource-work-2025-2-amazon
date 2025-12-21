<a href="img/Amazon-10.svg">SVG схема</a>

<a href="https://www.mermaidchart.com/d/6798f124-5495-49bd-a40b-f81c14d99ee4">схема c кодом на www.mermaidchart.com</a>


```
mermaid
flowchart TD

subgraph clients["Clients"]
  mobile_client["Mobile Client"]
  web_client["Web Client"]
  seller_client["Seller Client"]
  logistics_client["Logistics Client"]
end

subgraph proxy["DNS / Proxy / Balance"]
  Cloudflare["BGP Anycast"]
  L4-balancer["L4-balancer"]
  nginx_L7["L7 баланчировка (Nginx)"]
  cdn["CDN"]
  api_gateway["Public API Gateway"]
end

subgraph backend["Backend Services"]
  AuthService["Auth Service"]
  UserService["User Service"]
  CartService["Cart Service"]
  OrderService["Order Service"]
  ReviewService["Review Service"]
  LogisticsService["Logistics Service"]
  SellerService["Seller Service"]
  SearchService["Search Service"]
  PaymentService["Payment Service"]
  ProductService["Product Service"]
end

subgraph storage["Storage"]
  RedisSessions["Redis (Sessions)"]
  PostgresUsers["PostgreSQL (Users)"]
  PostgresProducts["PostgreSQL (Products)"]
  RedisProductCache["Redis Cache (Products)"]
  RedisCart["Redis (Cart)"]
  PostgresOrders["PostgreSQL (Orders)"]
  PostgresReviews["PostgreSQL (Reviews)"]
  PostgresShipments["PostgreSQL (Shipments)"]
  PostgresSellers["PostgreSQL (Sellers)"]
  ElasticSearch["ElasticSearch"]
  PostgresPayments["PostgreSQL (Payments)"]
  PostgresRatings["PostgreSQL (Ratings)"]
  S3["Amazon S3"]
end

subgraph queues["Message Queues"]
  Kafka["Kafka"]
end

subgraph monitoring["Monitoring & analytics"]
  Prometheus["Prometheus"]
  Grafana["Grafana"]
  ClickHouse["ClickHouse"]
end

subgraph external["External APIs"]
  PaymentGatewayAPI["Payment Gateway API"]
  LogisticsExternalAPI["Logistics API"]
end

%% Clients
mobile_client --> Cloudflare
web_client --> Cloudflare
seller_client --> Cloudflare
logistics_client --> Cloudflare
Cloudflare --> L4-balancer
L4-balancer --> nginx_L7

nginx_L7 --> api_gateway
nginx_L7 --> cdn

cdn --> S3

%% Public API Gateway
api_gateway --> AuthService
api_gateway --> UserService
api_gateway --> ProductService
api_gateway --> CartService
api_gateway --> OrderService
api_gateway --> ReviewService
api_gateway --> SearchService

%% Seller API Gateway
api_gateway --> SellerService
api_gateway --> ProductService
api_gateway --> OrderService
api_gateway --> LogisticsService

%% Logistics API Gateway
api_gateway --> LogisticsService

%% Backend Services to Workers
AuthService --> RedisSessions & PostgresUsers
UserService --> RedisSessions & PostgresUsers
ProductService --> PostgresProducts --> RedisProductCache
ProductService --> S3
CartService --> RedisCart
OrderService --> PostgresOrders
ReviewService -->|async| PostgresReviews
ReviewService -->|async| PostgresRatings
LogisticsService --> PostgresShipments
SellerService --> PostgresSellers
SearchService --> ElasticSearch

PaymentService --> PostgresPayments


%% Workers to External APIs
PaymentService -->|async| PaymentGatewayAPI
LogisticsService -->|async| LogisticsExternalAPI

%% Kafka Events
AllServices -->|async| Kafka
Kafka --> Prometheus
Kafka --> ClickHouse

%% Monitoring
Prometheus --> Grafana



classDef db fill:#ccf,stroke:#333,stroke-width:1px
classDef backend fill:#cbd3f5,stroke:#333,stroke-width:1px
classDef services fill:#e0d1f5,stroke:#333,stroke-width:1px
classDef proxy fill:#cce5cc,stroke:#333,stroke-width:1px
classDef client fill:#f9f9f9,stroke:#333,stroke-width:1px
classDef broker fill:#eeeeee,stroke:#333,stroke-width:1px

class mobile_client,web_client,seller_client,logistics_client client
class Cloudflare,L4-balancer,nginx_L7,cdn proxy
class api_gateway backend
class AuthService,UserService,ProductService,CartService,OrderService,ReviewService,LogisticsService,SellerService,SearchService,PaymentService services

class RedisSessions,PostgresUsers,PostgresProducts,RedisProductCache,RedisCart,PostgresOrders,PostgresReviews,PostgresShipments,PostgresSellers,ElasticSearch,PostgresPayments,PostgresRatings,S3 db
class Kafka,ClickHouse broker

```

## **Описание микросервисов**

### **1. User Service**

- Управление профилями пользователей: обновление, настройки, предпочтения.
- СУБД: PostgreSQL (Users)

### **2. Auth Service**

- Регистрация, авторизация, сессии.
- СУБД: PostgreSQL (Users) + Redis (Sessions)

### **3. Product Service**

- Управление карточками товаров.
- СУБД: PostgreSQL (Products), ElasticSearch (Search), Redis (Cache)
- Хранение медиа: S3
### **4. Cart Service**

- Работа с корзиной пользователя.
- СУБД: Redis (Cart)

### **5. Order Service**

- Управление заказами.
- СУБД: PostgreSQL (Orders)

### **6. Review Service**

- Добавление отзывов.
- СУБД: PostgreSQL (Reviews)
- Публикация событий в Kafka.

### **7. Logistics Service**

- Отслеживание отправлений.
- СУБД: PostgreSQL (Shipments)
- Интеграция с внешним `Logistics API`
- Асинхронная публикация событий в Kafka.

### **8. Seller Service**

- Управление продавцами.
- СУБД: PostgreSQL (Sellers)

### **9. Search Service**

- Поиск по товарам и продавцам.
- СУБД: ElasticSearch

### **10. Payment Service**

- Интеграция с `Payment Gateway API`.
- СУБД: PostgreSQL (Payments)
- Асинхронная публикация в Kafka.
- Фолбэк: Payment Error Worker

### **11. Recommendation Service**

- Персональные рекомендации.
- СУБД: PostgreSQL (Recommendations), Redis (Base Feed)
- Фолбэк: Error Recommendation Worker

### **12. Moderation Service**

- Асинхронная модерация отзывов и товаров.
- События через Kafka (Moderation Queue)

### **13. Orchestrator Service**

- Управление сложными сагами и бизнес-процессами.
- Построен на Kafka Streams / Temporal.

### **14. User Activity Worker**

- Обработка действий пользователя.
- Запись в ElasticSearch и PostgreSQL (Recommendations).

---
