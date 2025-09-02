```mermaid
graph TD
    subgraph Legend
        direction LR
        L1(Product) -.-> L2(Data Object);
    end

    subgraph Phase 1: Study Design
        Designer[Designer] -- Creates --> SoA(Digital Schedule <br> of Activities);
    end

    subgraph Phase 2: Study Planning
        direction LR
        FSP[Financial Scenario Planning];
        GMP[Grants Manager Planning];
        IT[Intelligent Trials / Feasibility];
        RBQM_Plan[RBQM];
        SoA -- Feeds --> FSP;
        SoA -- Feeds --> GMP;
        SoA -- Feeds --> IT;
        SoA -- Feeds --> RBQM_Plan;
        FSP -- Creates --> StudyBudget(Study Budget);
        GMP -- Creates --> SiteTemplate(Site Budget Template);
        IT -- Creates --> SiteList(Potential Site List);
        RBQM_Plan -- Creates --> RiskPlan(Risk Monitoring Plan);
    end

    subgraph Phase 3: Study Startup
        GCLM[Grants & Contracts <br> Lifecycle Manager]
        CTMS_Startup[CTMS];
        EDC_Build[EDC Build (Rave)];
        SiteTemplate -- Feeds --> GCLM;
        SiteList -- Feeds --> CTMS_Startup;
        SoA -- Feeds --> EDC_Build;
        GCLM -- Creates --> ExecutedContracts(Executed Budgets & CTAs);
        EDC_Build -- Creates --> LiveEDC(Live Clinical Database);
    end

    subgraph Phase 4: Study Execution
        direction LR
        EDC_Exec[EDC (Rave)];
        Payments[Patient & Site Payments];
        CTMS_Exec[CTMS];
        RBQM_Exec[RBQM];
        LiveEDC -- Captures Data In --> EDC_Exec;
        ExecutedContracts -- Informs --> Payments;
        EDC_Exec -- Triggers --> Payments;
        EDC_Exec -- Sends Data to --> CTMS_Exec;
        EDC_Exec -- Sends Data to --> RBQM_Exec;
    end

    subgraph Continuous Oversight
        Dashboard[Unified Operational & <br> Financial Dashboard];
        FSP & Payments -- Financial Data --> Dashboard;
        CTMS_Exec & EDC_Exec -- Operational Data --> Dashboard;
        RBQM_Exec -- Risk Data --> Dashboard;
    end

    subgraph Amendment Loop
        direction BT
        Amendment(Protocol Amendment Approved);
        Designer_v2[Designer v2.0];
        Planning_v2[Re-Planning];
        Startup_v2[Re-Startup];
        Amendment --> Designer_v2;
        Designer_v2 --> Planning_v2;
        Planning_v2 --> Startup_v2;
        Startup_v2 --> EDC_Exec;
    end

    Phase 1 --> Phase 2 --> Phase 3 --> Phase 4 --> Dashboard;
    Phase 4 -.-> Amendment;
