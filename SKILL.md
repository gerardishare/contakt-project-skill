---
name: contakt-project-setup
description: set up a client or internal project workspace that should use sharepoint as its document source and chatgpt projects as its working context. use when chatgpt needs to check whether a sharepoint app/connection is available, ask for the project root folder, propose or create a standard folder structure, and run an interactive intake that produces a reusable project context for all chats in the project.
---

# SharePoint project setup

Run this workflow in order. Be explicit about what you verified, what you inferred, and what still needs the user to do manually.

## Setup workflow

1. **Check SharePoint availability first.**
2. **Ask for the SharePoint project root folder.**
3. **Propose or create the folder structure.**
4. **Run an intake interview one question at a time.**
5. **Write the final project context and setup summary.**

Do not skip step 1. Do not pretend a SharePoint app, connector, or write capability exists unless you actually verified it with available tools.

## 1) Check SharePoint availability

Start by determining whether SharePoint is available in the current ChatGPT environment.

- If the environment exposes connected apps, connectors, or sources, inspect them first.
- If SharePoint is clearly available and authenticated, say so.
- If SharePoint exists but is not authenticated, tell the user they need to sign in.
- If SharePoint is not available, stop the automation part and explain the manual next step: enable or connect SharePoint in **Settings > Apps** or ask their workspace admin to enable it.

If SharePoint is unavailable, you may still continue with:
- the recommended folder structure
- the intake interview
- the generated project context

But clearly label the setup as **not yet connected to SharePoint**.

## 2) Ask for the project root folder

Ask for the root folder on SharePoint that should contain the project workspace.

Accept any of these:
- a SharePoint URL
- a folder path
- a site plus library and folder name

Also confirm or infer:
- client name
- project name

If the user has already provided one of these in the conversation, do not ask again.

## 3) Folder structure

Use this default structure unless the user asks for a variation:

```text
/[client] - [project]
  /00_Projectcontext
  /01_Bronbestanden
  /02_Werkbestanden
  /03_Definitief
  /04_Admin
```

Purpose of each folder:
- `00_Projectcontext`: project brief, customer profile, scope, planning, standards, prompts, working agreements
- `01_Bronbestanden`: source documents and input material that count as the primary knowledge base
- `02_Werkbestanden`: drafts, analyses, notes, intermediate outputs, experiments
- `03_Definitief`: approved deliverables and final versions
- `04_Admin`: operational or administrative material that should usually not drive substantive analysis

### Creation rule

If there is a verified write-capable SharePoint action available, create the folders there.

If there is no verified write-capable action, do **not** claim they were created. Instead:
- show the exact folder tree
- tell the user to create it manually in SharePoint
- continue with the project-context setup anyway

## 4) Intake interview

Run the intake interactively, one question at a time. Keep questions short. Reuse information already given. Do not ask for information that is already known.

Collect at least:
- client name
- project name
- project goal
- scope
- out of scope
- key stakeholders or audiences
- expected deliverables
- preferred language
- preferred tone or style
- confidentiality or sensitivity considerations

Optional if useful:
- success criteria
- deadlines or milestone cadence
- terminology to use or avoid
- preferred structure for outputs

### Questioning behavior

- Ask exactly one main question per turn.
- If the user gives multiple answers at once, update the intake state and move to the next missing field.
- Summarize briefly after every 3-4 answers so the user can correct misunderstandings.
- Default to Dutch if the user does not specify a language.
- Default to a professional consultancy style if the user does not specify tone.

## 5) Final outputs

When enough information is collected, always produce **all** of the following sections.

### A. Setup status

Report:
- whether SharePoint availability was verified
- whether authentication appears complete
- whether folder creation was executed or still needs manual action
- what root folder was used

### B. Recommended or created folder structure

Show the final tree in a fenced text block.

### C. Project context

Write a polished project-context block that is ready to paste into ChatGPT Project instructions or a dedicated project-context document.

Always include a section that explains how ChatGPT should use the SharePoint folder structure. This section does **not** require user input and should be inserted automatically.

Use this exact section title and meaning:

```text
Gebruik van de SharePoint mappenstructuur:
- Gebruik 00_Projectcontext voor vaste projectinformatie, afspraken en context die in alle chats geldt.
- Gebruik 01_Bronbestanden als primaire bron van waarheid voor analyse, samenvattingen en adviezen.
- Gebruik 02_Werkbestanden voor concepten, tussenversies, analyses en werkdocumenten.
- Gebruik 03_Definitief voor gevalideerde eindversies en goedgekeurde deliverables.
- Gebruik 04_Admin alleen voor operationele of administratieve informatie en niet als primaire inhoudelijke bron, tenzij expliciet gevraagd.
- Benoem onzekerheid wanneer informatie ontbreekt of wanneer bronnen elkaar tegenspreken.
- Maak onderscheid tussen feiten uit bronbestanden, interpretaties en aanbevelingen.
```

### D. Suggested starter prompts

Give 3 short starter prompts tailored to the project, for example:
- analyze source material
- draft a deliverable
- review a draft against project context

## Output template

Use this final structure unless the user requests another format.

```markdown
## Setup status
- SharePoint app/connector:
- Authentication status:
- Root folder:
- Folder creation status:

## Folder structure
```text
[paste final tree]
```

## Project context
[paste the final context block in the user's preferred language]

## Starter prompts
1. ...
2. ...
3. ...
```

## Project-context writing rules

When writing the project context:
- write in the user's preferred language
- keep it concise but complete
- prefer clear headings over long paragraphs
- avoid generic ai phrasing
- treat `00_Projectcontext` and `01_Bronbestanden` as the default source of truth
- explicitly instruct ChatGPT to mention uncertainty instead of guessing
- separate facts, interpretations, and recommendations whenever relevant

## Reference files

Consult these files when useful:
- `references/folder-structure.md` for the default SharePoint layout and folder meanings
- `references/project-context-template.md` for the project-context scaffold
