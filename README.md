```mermaid
graph TD
    %% Phase 1
    Designer[Designer] --> SoA[Digital Schedule of Activities];

    %% Phase 2
    SoA --> FSP[Financial Scenario Planning];
    SoA --> GMP[Grants Manager Planning];
    SoA --> IT[Intelligent Trials / Feasibility];
    SoA --> RBQM_Plan[RBQM];
    FSP --> StudyBudget[Study Budget];
    GMP --> SiteTemplate[Site Budget Template];
    IT --> SiteList[Potential Site List];
    RBQM_Plan --> RiskPlan[Risk Monitoring Plan];

    %% Phase 3
    SiteTemplate --> GCLM[Grants and Contracts Lifecycle Manager];
    SiteList --> CTMS_Startup[CTMS];
    SoA --> EDC_Build[EDC Build Rave];
    GCLM --> ExecutedContracts[Executed Budgets and CTAs];
    EDC_Build --> LiveEDC[Live Clinical Database];

    %% Phase 4
    LiveEDC --> EDC_Exec[EDC Rave Execution];
    ExecutedContracts --> Payments[Patient and Site Payments];
    EDC_Exec --> Payments;
    EDC_Exec --> CTMS_Exec[CTMS Execution];
    EDC_Exec --> RBQM_Exec[RBQM Execution];

    %% Oversight
    FSP --> Dashboard[Operational and Financial Dashboard];
    Payments --> Dashboard;
    CTMS_Exec --> Dashboard;
    RBQM_Exec --> Dashboard;

    %% Amendment Loop
    EDC_Exec --> Amendment[Protocol Amendment Approved];
    Amendment --> Designer_v2[Designer v2.0];
    Designer_v2 --> Planning_v2[Re-Planning];
    Planning_v2 --> Startup_v2[Re-Startup];
    Startup_v2 --> EDC_Exec;
