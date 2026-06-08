```mermaid
graph TB
    %% Ορισμός Στυλ
    classDef sor fill:#f9f,stroke:#333,stroke-width:4px;
    classDef apps fill:#fff,stroke:#333,stroke-width:2px;
    classDef finance fill:#dfd,stroke:#333,stroke-width:2px;

    subgraph Core_System [<b>System of Record (SoR)</b>]
        SOR[<b>Κεντρικό SoR</b><br/>Master Data & Logic]:::sor
    end

    subgraph Inputs [Πηγές Δεδομένων]
        Registry[Μητρώο Συνεργατών]:::apps
        Public Pro[Παρακολούθηση Συμβάσεων]:::apps
    end

    subgraph Ops [Επιχειρησιακά Υποσυστήματα]
        TS[Timesheet App]:::apps
        Travel[Travel Expenses]:::apps
        Procure[Procurement App]:::apps
    end

    subgraph Financials [Οικονομική Διαχείριση]
        Pay[Paybrain]:::finance
        ERP[ERP System]:::finance
    end

    %% Ροές και Διασυνδέσεις
    Registry -->|Στοιχεία Συνεργατών| SOR
    Contracts -->|Όροι Συμβάσεων & Budget| SOR
    
    SOR <-->|API: Verification & Data Sync| TS
    SOR <-->|API: Expense Validation| Travel
    SOR <-->|API: Purchase Orders| Procure

    TS -.->|Approved Hours| Pay
```
    Travel -.->|Approved Expenses| Pay
    
    Pay -->|Payroll Data| ERP
    SOR -->|Accounting Entries| ERP
    Procure -->|Invoices| ERP
