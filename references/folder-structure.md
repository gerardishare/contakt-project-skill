# Default SharePoint project structure

## Tree

```text
/[client] - [project]
  /00_Projectcontext
  /01_Bronbestanden
  /02_Werkbestanden
  /03_Definitief
  /04_Admin
```

## Folder intent

### 00_Projectcontext
Use for stable project instructions that should govern all chats and outputs.
Examples:
- project brief
- customer profile
- scope and exclusions
- definitions and terminology
- quality criteria
- writing conventions

### 01_Bronbestanden
Treat as the primary knowledge base.
Examples:
- customer documents
- interview notes
- policies
- source reports
- research inputs

### 02_Werkbestanden
Use for work in progress.
Examples:
- drafts
- analyses
- scratch notes
- interim deliverables
- comparison documents

### 03_Definitief
Use for approved outcomes.
Examples:
- final reports
- approved presentations
- signed-off recommendations

### 04_Admin
Use for project operations, not substantive analysis by default.
Examples:
- planning sheets
- budgets
- administration
- internal logistics

## Interpretation rule

When answering project questions, prefer sources in this order unless the user instructs otherwise:
1. 00_Projectcontext
2. 01_Bronbestanden
3. 03_Definitief
4. 02_Werkbestanden
5. 04_Admin
