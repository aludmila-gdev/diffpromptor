```mermaid
flowchart LR
  %% → Front-end
  subgraph Frontend
    UA(Usuário) -->|HTTP| WebApp(Web App)
  end

  %% → API Gateway
  subgraph API_Gateway
    WebApp --> APIGW(API Gateway)
  end

  %% → Serviços de Autenticação & Usuário
  subgraph Auth_User
    APIGW --> AuthSvc(Auth Service)
    AuthSvc --> UserSvc(User Service)
    UserSvc --> DBUser[(User DB)]
  end

  %% → Pedidos & Pagamentos
  subgraph Orders_Payments
    APIGW --> OrderSvc(Order Service)
    OrderSvc --> DBOrder[(Orders DB)]
    OrderSvc --> PaymentSvc(Payment Service)
    PaymentSvc --> ThirdParty[Gateway Externo]
  end

  %% → Estoque
  subgraph Inventory
    APIGW --> InventorySvc(Inventory Service)
    InventorySvc --> DBInventory[(Inventory DB)]
  end

  %% → Notificações
  subgraph Notifications
    OrderSvc --> NotifySvc(Notification Service)
    NotifySvc -->|Email/SMS| UA
  end
