```mermaid
graph TD
    subgraph "Phase 0: Long-Range Planning (2-5 Years Pre-Protocol)"
        FSP_LR[Financial Scenario Planning] -- Creates --> HighLevelBudget(High-Level Estimated Budget);
    end

    subgraph "Phase 1: Study Design (Iterative Loop)"
        Designer[Designer <br> Protocol & SOA Authoring];
        HighLevelBudget -- Informs --> Designer;
        
        Designer -- Iteration 1..n --> FSP_Design[FSP for Design Impact];
        Designer -- Iteration 1..n --> IT_Design[Intelligent Trials for Feasibility];
        Designer -- Iteration 1..n --> RBQM_Design[RBQM for Risk Assessment];
        
        FSP_Design -- Financial Feedback --> Designer;
        IT_Design -- Operational Feedback --> Designer;
        RBQM_Design -- Risk Feedback --> Designer;
    end

    subgraph "Phase 2: Protocol Finalization & Digitization"
        Designer -- Final Version --> ApprovedProtocol[Approved Protocol/SOA];
        ApprovedProtocol --> DigitalTeam[Digital Protocol Team];
        DigitalTeam -- Digitizes --> DigitalProtocol((Digital Protocol <br> Single Source of Truth));
    end

    subgraph "Phase 3: Study Startup"
        direction LR;
        GM[Grants Manager];
        EDC_Build[EDC Build];
        CTMS_Setup[CTMS Setup];
        ContractingApp{New Contracting App <br> Budget Negotiation & CTA Execution};
        
        DigitalProtocol -- Populates --> GM;
        DigitalProtocol -- Populates --> EDC_Build;
        DigitalProtocol -- Populates --> CTMS_Setup;
        DigitalProtocol -- Populates --> FSP_Detailed[FSP for Baseline Budget];

        GM -- Site Budget Template --> ContractingApp;
        ContractingApp -- Align Payment Schedule <--> EDC_Build;
        ContractingApp -- Creates --> ExecutedCTA[Executed CTA];
        ExecutedCTA --> CTARepo[CTA Repository];
        CTARepo -. Alerts: Payment Rules .-> SitePayments_Setup[Site Payments Setup];
        CTARepo -. Alerts: Final Terms .-> GM;
        CTARepo -. Alerts: Final Visit Schedule .-> EDC_Build;
    end

    subgraph "Phase 4: Study Execution"
        EDC_Exec[EDC Data Capture];
        RBQM_Exec[RBQM Monitoring];
        CTMS_Exec[CTMS Management];
        
        EDC_Exec -- Feeds Live Data --> RBQM_Exec;
        EDC_Exec -- Feeds Live Data --> CTMS_Exec;

        subgraph "Payment Sub-Process"
            direction LR
            ReceiveTrigger(1. Receive EDC Trigger);
            MatchToCTA(2. Match Data to CTA);
            Calculate(3. Calculate Payment);
            Generate(4. Generate Invoice/Instruction);
            Disburse(5. Disburse Funds);
        end

        EDC_Exec -- Subject Visit/Procedure Data --> ReceiveTrigger;
    end

    subgraph "Phase 5: Unified Oversight"
        Dashboard[Operational & Financial Dashboard];
        FSP_Detailed -- Financial Plan --> Dashboard;
        Disburse -- Financial Actuals --> Dashboard;
        CTMS_Exec -- Operational Data --> Dashboard;
        RBQM_Exec -- Risk/Quality Data --> Dashboard;
        EDC_Exec -- Enrollment Data --> Dashboard;
    end
