flowchart LR
  %% Frontend
  subgraph Frontend
    UA[Usuário] -->|Acessa via HTTP| WebApp[Web App]
  end

  %% API Gateway
  subgraph API
    WebApp --> APIGW[API Gateway]
  end

  %% Serviços de Autenticação e Usuário
  subgraph Autenticação & Usuário
    APIGW --> AuthSvc[Auth Service]
    AuthSvc --> UserSvc[User Service]
    UserSvc --> DBUser[(User DB)]
  end

  %% Serviços de Pedido e Pagamento
  subgraph Pedidos & Pagamentos
    APIGW --> OrderSvc[Order Service]
    OrderSvc --> DBOrder[(Orders DB)]
    OrderSvc --> PaymentSvc[Payment Service]
    PaymentSvc --> ThirdParty[Gateway Externo]
  end

  %% Serviços de Estoque
  subgraph Estoque
    APIGW --> InventorySvc[Inventory Service]
    InventorySvc --> DBInventory[(Inventory DB)]
  end

  %% Notificações
  subgraph Notificações
    OrderSvc --> NotifySvc[Notification Service]
    NotifySvc -->|Email/SMS| UA
  end
