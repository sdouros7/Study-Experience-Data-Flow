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

    Phase 1 --> Phase 2;
