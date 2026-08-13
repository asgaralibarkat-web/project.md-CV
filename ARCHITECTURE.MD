flowchart LR
    subgraph Client Boundary [User Local Environment]
        U[Primary User / Job Seeker]
    end

    subgraph Application Boundary [Local Python CLI Runtime]
        CLI[Interface: main.py CLI Handler]
        VAL[Validation & Prompt Builder]
        FS[File System Handler]
    end

    subgraph Data Store Boundary [Local Storage]
        CV[(cv.txt)]
        JOB[(job.txt)]
        OUT[(application_draft.md)]
    end

    subgraph External Provider Boundary [Google Cloud / AI Studio]
        LLM[External Model Provider: Gemini 2.5 Flash]
    end

    %% Flow Connections
    U -- "1. Executes 'python main.py'" --> CLI
    CLI -- "2. Reads local input files" --> FS
    FS -- "Reads candidate details" --> CV
    FS -- "Reads job posting text" --> JOB
    FS -- "3. Returns raw text contents" --> VAL
    VAL -- "4. Constructs bounded prompt & validates inputs" --> CLI
    
    %% Trust Boundary 1
    CLI == "TB1: API Key & SSL/TLS" ==> LLM
    
    LLM -- "5. Returns generated Markdown response" --> CLI
    CLI -- "6. Saves structured scorecard & cover letter" --> FS
    FS -- "Writes output file" --> OUT
    OUT -- "7. Reviews final draft" --> U

    %% Trust Boundaries Annotations
    classDef boundary fill:#f9f9f9,stroke:#333,stroke-width:1px;
    class Client Boundary,Application Boundary,Data Store Boundary,External Provider Boundary boundary;
