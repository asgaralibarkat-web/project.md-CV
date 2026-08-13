# ARCHITECTURE.md: System Architecture & Data Flow

## Point 1: System Architecture Diagram

```mermaid
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

    U -- "1. Executes 'python main.py'" --> CLI
    CLI -- "2. Reads local input files" --> FS
    FS -- "Reads candidate details" --> CV
    FS -- "Reads job posting text" --> JOB
    FS -- "3. Returns raw text contents" --> VAL
    VAL -- "4. Constructs bounded prompt" --> CLI
    
    CLI == "TB1: GEMINI_API_KEY Check" ==> LLM
    
    LLM -- "5. Returns generated Markdown response" --> CLI
    CLI -- "6. Saves structured scorecard & cover letter" --> FS
    FS -- "Writes output file" --> OUT
    OUT -- "7. Reviews final draft" --> U
Point 2: Component Responsibility TableComponentResponsibilityInputsOutputsFailure BehaviorFile EvidenceCLI RuntimeReads environment keys and initiates workflow execution.GEMINI_API_KEY, terminal commandConsole logs, process return codeHalts if API key is missing.main.pyFile System HandlerLoads input text and saves the final result.cv.txt, job.txtFile contents, application_draft.mdHalts with error if files don't exist.main.pyPrompt BuilderFormats CV and job posting into an anti-hallucination prompt.Raw CV & job text stringsFormatted prompt stringStops if inputs are empty.main.pyGoogle Gemini API ClientSends prompt to Google AI Studio and receives response.Formatted prompt, API keyMarkdown text responseHandles API timeout or auth error.main.py, requirements.txtPoint 3: Numbered Request and Data FlowUser Execution: User runs python main.py in the terminal.Read Inputs: main.py reads candidate text from cv.txt and job posting text from job.txt.Build Prompt: main.py combines the text into a structured prompt with anti-hallucination instructions.Send to Gemini: main.py sends an HTTPS request to Google AI Studio (gemini-2.5-flash) using GEMINI_API_KEY.Receive Draft: Google AI Studio returns the generated Match Scorecard and Cover Letter.Save Result: main.py writes the output to application_draft.md.Human Review: User opens application_draft.md to review the generated application materials.Point 4: Trust Boundaries & ChecksTB1 (Local Environment -> Google AI Studio): Validates that GEMINI_API_KEY exists in environment variables before sending network requests. Ensures no secret keys are committed to Git.TB2 (Output -> File System): Checks that the returned text payload is non-empty before writing to application_draft.md.
