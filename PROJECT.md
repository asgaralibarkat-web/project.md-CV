# PROJECT.md: Project Brief

## Project Title
Targeted Job Application Drafter (CV-to-Listing Matcher)

## Coding Tool
Claude Code (or OpenAI Codex)

## Primary User
An active job seeker targeting real estate and operations roles on Luxembourg job portals (e.g., ADEM, LinkedIn).

## Problem Today
Manually reviewing long job descriptions, cross-referencing CV qualifications, and writing custom cover letters for every application causes fatigue, copy-paste errors, and significant time loss.

## Useful Outcome
A generated local file containing a CV Match Scorecard (3 aligned skills, 1 gap) and a single-page tailored cover letter draft ready for human review.

## Smallest Live Demonstration
1. Place candidate background in cv.txt and job description in job.txt.
2. Run python main.py in the terminal.
3. System reads both files, runs the analysis, and outputs application_draft.md.

## Data Needed
* cv.txt (Candidate resume text)
* job.txt (Pasted job description text)
* Prompts configured in main.py

## Success Definition (Pass/Fail Checks)
* [ ] Pass: Generates output within 15 seconds.
* [ ] Pass: Scorecard correctly lists 3 matching skills and 1 identified gap.
* [ ] Pass: Cover letter accurately references candidate facts without hallucinating credentials.
* [ ] Fail: Output includes generic placeholders or unverified facts.

## Scope Exclusions (V1 Non-Goals)
1. No web scraping or auto-browsing.
2. No automatic submission to job portals.
3. No PDF export or custom layout engines.
