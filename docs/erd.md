```mermaid
erDiagram
  TENANTS ||--o{ STORES : has
  TENANTS ||--o{ USERS : has
  TENANTS ||--o{ TABLES : has
  TENANTS ||--o{ MENU_CATEGORIES : has
  TENANTS ||--o{ MENU_ITEMS : has
  TENANTS ||--o{ RESERVATIONS : has
  TENANTS ||--o{ ORDERS : has
  TENANTS ||--o{ PAYMENTS : has
  TENANTS ||--o{ REVIEWS : has

  STORES ||--o{ TABLES : has
  STORES ||--o{ RESERVATIONS : has
  STORES ||--o{ ORDERS : has
  STORES ||--o{ REVIEWS : has

  USERS ||--o{ RESERVATIONS : makes
  USERS ||--o{ REVIEWS : writes
  USERS ||--o{ PAYMENTS : pays

  RESERVATIONS ||--o{ ORDERS : may_generate
  RESERVATIONS }o--|| TABLES : assigned_to

  ORDERS ||--o{ ORDER_ITEMS : contains
  ORDERS ||--o{ PAYMENTS : paid_by

  MENU_CATEGORIES ||--o{ MENU_ITEMS : includes

  TENANTS {
    bigint id
    string name
    string slug
    string plan
    string status
  }

  USERS {
    bigint id
    bigint tenant_id
    string name
    string email
    string password
    string role
  }

  STORES {
    bigint id
    bigint tenant_id
    string name
    string phone
    string address
  }

  TABLES {
    bigint id
    bigint tenant_id
    bigint store_id
    string name
    int capacity
  }

  MENU_CATEGORIES {
    bigint id
    bigint tenant_id
    bigint store_id
    string name
  }

  MENU_ITEMS {
    bigint id
    bigint tenant_id
    bigint store_id
    bigint menu_category_id
    string name
    bigint price
  }

  RESERVATIONS {
    bigint id
    bigint tenant_id
    bigint store_id
    bigint table_id
    bigint customer_id
    datetime reserved_at
    int people_count
    string status
  }

  ORDERS {
    bigint id
    bigint tenant_id
    bigint store_id
    bigint table_id
    bigint reservation_id
    bigint customer_id
    string status
  }

  ORDER_ITEMS {
    bigint id
    bigint order_id
    bigint menu_item_id
    int quantity
    bigint unit_price
    bigint total_price
  }

  PAYMENTS {
    bigint id
    bigint tenant_id
    bigint order_id
    bigint user_id
    bigint amount
    string method
    datetime paid_at
  }

  REVIEWS {
    bigint id
    bigint tenant_id
    bigint store_id
    bigint user_id
    bigint reservation_id
    tinyint rating
    string comment
  }
```