## ProManage - Diagrama Arquitectura 

graph TB
%% Arquitectura General de ProManage
subgraph "🌐 Frontend Layer"
WEB[Web App<br/>React/Angular]
MOB[Mobile App<br/>React Native]
PWA[PWA<br/>Progressive Web App]
end

    subgraph "🚪 API Gateway Layer"
        GW[API Gateway<br/>Kong/AWS API Gateway]
        LB[Load Balancer<br/>Application LB]
        AUTH[Auth Middleware<br/>JWT Validation]
    end
    
    subgraph "🔧 Microservices Layer"
        AS[🔐 Auth Service<br/>Authentication & Authorization]
        US[👥 User Service<br/>User Profiles & Management]
        PS[📋 Project Service<br/>Project CRUD & Timeline]
        BS[💰 Budget Service<br/>Financial Management]
        FS[📁 File Service<br/>Document Management]
        NS[🔔 Notification Service<br/>Email & Push Notifications]
    end
    
    subgraph "💾 Data Layer"
        PG[(PostgreSQL<br/>Relational Data)]
        MG[(MongoDB<br/>Document Store)]
        RD[(Redis<br/>Cache & Sessions)]
        S3[(AWS S3<br/>File Storage)]
    end
    
    subgraph "🏗️ Infrastructure Layer"
        K8S[☸️ Kubernetes<br/>EKS Cluster]
        ECR[🏪 AWS ECR<br/>Container Registry]
        ELB[⚖️ Elastic Load Balancer]
        CF[☁️ CloudFront CDN]
    end
    
    subgraph "📊 Monitoring & Logging"
        PROM[📊 Prometheus<br/>Metrics Collection]
        GRAF[📈 Grafana<br/>Dashboards]
        ELK[📋 ELK Stack<br/>Logging]
    end
    
    %% Conexiones principales
    WEB --> GW
    MOB --> GW
    PWA --> GW
    
    GW --> AUTH
    AUTH --> LB
    LB --> AS
    LB --> US
    LB --> PS
    LB --> BS
    LB --> FS
    LB --> NS
    
    %% Conexiones a bases de datos
    AS --> PG
    AS --> RD
    US --> PG
    PS --> PG
    PS --> MG
    BS --> PG
    FS --> S3
    NS --> RD
    
    %% Infraestructura
    K8S --> ECR
    ELB --> K8S
    CF --> ELB
    
    %% Monitoreo
    PROM --> K8S
    GRAF --> PROM
    ELK --> K8S
    
    %% Estilos
    classDef frontend fill:#ff6b6b,stroke:#c92a2a,stroke-width:2px,color:#fff
    classDef gateway fill:#4ecdc4,stroke:#339af0,stroke-width:2px,color:#fff
    classDef service fill:#45b7d1,stroke:#1971c2,stroke-width:2px,color:#fff
    classDef database fill:#6c5ce7,stroke:#5f3dc4,stroke-width:2px,color:#fff
    classDef infra fill:#fd79a8,stroke:#e64980,stroke-width:2px,color:#fff
    classDef monitor fill:#51cf66,stroke:#37b24d,stroke-width:2px,color:#fff
    
    class WEB,MOB,PWA frontend
    class GW,LB,AUTH gateway
    class AS,US,PS,BS,FS,NS service
    class PG,MG,RD,S3 database
    class K8S,ECR,ELB,CF infra
    class PROM,GRAF,ELK monitor

## Diagrama 