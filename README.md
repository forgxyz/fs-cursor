# fs-cursor

This repository defines cursor rules for using the Flipside MCP tools as a data analyst. It provides a comprehensive framework for blockchain analytics workflows and is designed to help analysts transition from SQL-based dashboards to MCP-driven workflows and artifacts. It is in early stages and constantly evolving. I hope that these rules make it a bit easier to use the Flipside MCP tools to derive insights and build great work!

## Target Audience

This repository is aimed at analysts who previously had SQL-based dashboards deployed to Flipside's Data Studio and are looking to evolve their analytical workflows using modern MCP (Model Context Protocol) tools.

## Integration with dashboard-dl

This repository is designed to work alongside the [dashboard-dl tool](https://github.com/forgxyz/dashboard-dl), which helps analysts:
- Extract existing SQL dashboards from Data Studio
- Convert them into MCP-driven workflows
- Create modern analytical artifacts

## Getting Started

1. **Prerequisites**: Ensure you have the dashboard-dl tool installed and configured
2. **Rule Setup**: Copy the `.cursor/rules/` directory to your project
3. **Workflow**: Use the analytics_workflow.mdc rule as your entry point for blockchain analytics questions

## Best Practices
1. Ask Cursor to generate a `CONTEXT.md` file, provide the `*-description.md` file as input context. This new markdown file will serve as the base context for your work going forward. The `interpret_dashboard` rule was written to guide generation of this file.
2. Start your analysis by tagging or adding `CONTEXT.md` as the input to your workflow. Cursor should follow the `analytics_workflow` rule as the guiding principles of your work. This can be edited and adjusted to best fit your needs. You may need to tag this rule, even though it is set to always apply. This rule should require the workflow to follow the `log_methodology` rule, which will be a running log of the LLM client's process. It is helpful to add this as context to the chat as well, alongside `CONTEXT.md`
3. Work with intention! Well constructed artifacts are rarely, if ever, one shot prompts. If the LLM is interrupting and asking for feedback too much, adjust the prompts in the rules, otherwise work with the client to build the artifact iteratively.
    - `dashboard-dl` creates `.csv` files with the last cached query results. This has proven to be a problem, at times, as the LLM client will stray away from querying fresh data to using the archive. A simple nudge in the chat like, `"Do NOT use the saved CSVs. Run the queries to get fresh data then update the document"` should be sufficient to guide the LLM back to using the execute sql tools. I have removed the reference to the resultset location from the `*-description.md` which should help.
4. Install the Live Preview extension (`ms-vscode.live-server`) to see a fully rendered HTML document within Cursor
5. Just like with SQL-based analytics, it is up to the human in the loop to quality check answers! A compiled query is not necessarily a correct query. This is where moving slowly will help. Build in pieces, check the pieces, continue onwards.
6. **Remember:** The LLM client is your co-analyst. Treat it as a collaborator, not a code monkey. Rules are simply prompts and the client may need guidance back to a rule if you find its behavior straying from the intended workflow. As with above, a simple message like `"Yes, looks great! Let's move on to the last tab and do not forget the @log_methodology.mdc rule"` will keep you on target.
7. Pay attention to what the chat outputs - often the LLM client will ask for confirmation about the next steps. Read these! Make sure the workflow is in line with what you want, and intervene as needed.
8. Customize and take ownership of the rules! If you find yourself repeating an instruction, add a new rule or change an existing one.

## Workflow Overview

This guide walks you through migrating and modernizing your Flipside Data Studio dashboards using Cursor AI with these specialized rules. The process transforms static dashboards into dynamic, current analytics with fresh data and modern presentation.

### One-Shot Automated Migration (Experimental)

**NEW**: For the fastest dashboard migration, try the experimental one-shot workflow:

```
@one_shot_migration.mdc https://flipsidecrypto.xyz/your-dashboard-url
```

This single command attempts to:
- ✅ Automatically install dashboard-dl if needed (clones repo, runs `uv sync`)
- ✅ Download and archive your dashboard to `outputs/` folder
- ✅ Generate context and execute fresh queries autonomously
- ✅ Build a complete HTML dashboard with cyber gaming aesthetic
- ✅ Create full audit trail and methodology documentation

**Note**: This is experimental and may not work perfectly in all cases. If it does stop for user input, try just telling the LLM client to Continue. If that fails or you need more control over the process, use the step-by-step workflow below to take control.

---

### Step-by-Step Manual Workflow

If the one-shot approach doesn't work or you prefer more control over the process:

### Prerequisites

- **Cursor IDE** with these rules properly loaded
- **Flipside MCP tools** configured in your environment  
- **dashboard-dl** tool: [forgxyz/dashboard-dl](https://github.com/forgxyz/dashboard-dl)

### Phase 1: Archive Your Dashboard

**Extract your existing Flipside dashboard:**
Follow the installation instructions in `dashboard-dl` and run the command from this directory
```bash
# Download dashboard archive from Flipside Data Studio
`dashboard-dl [your-dashboard-url]`
```

**What you get:** Complete dashboard archive with SQL queries, descriptions, and metadata files.

### Phase 2: Generate Context

**Let Cursor create the analysis context:**
- Open a new Cursor chat with the `*-description.md` tagged as context and ask Cursor to create a context file.
- Cursor automatically triggers context generation based on the defined rule
- Review the generated `CONTEXT.md` for completeness
- If needed, prompt: *"Please review and enhance the CONTEXT.md based on the dashboard description, follow the rule @interpret_dashboard"*

**What you get:** Structured `CONTEXT.md` that captures original dashboard intent and requirements.

### Phase 3: Migrate & Analyze

**Work with Cursor to execute fresh analysis:**
- Prompt: *"Analyze the original SQL queries and execute fresh versions using Flipside MCP tools"*
- Review `methodology.md` as Cursor builds the analysis audit trail
- **Critical instruction:** *"Use only fresh warehouse data, never cached CSV files"* Cursor should default to executing queries, but the presence of the csv files does sometimes confuse the workflow.

### Phase 4: Rebuild Dashboard

**Collaborate with Cursor to create modern visualization:**
- Prompt: *"Create a modern HTML dashboard with the query results. Build data visualizations per the requirements in the context file"*
- Cursor applies responsive design and visual style standards
- Verify ascending time axes and mandatory data source dropdowns
- Request adjustments: *"Modify the [chart type] to better highlight [specific insight]"*

### Phase 5: Validate & Publish

**Ensure accuracy and deploy:**
- Prompt: *"Cross-validate key metrics with DeFiLlama data"*
- Work with the Flipside Workflow and Skills tools to add new elements, review the existing elements, or take the analysis in a whole new direction. At this point, it is entirely up to you and your needs.
- Review final dashboard for completeness and accuracy
- Deploy: *"Publish this dashboard using the MCP publish html tools"*
- The style guide is something that I like. You can modify or delete the rule if it is creating an artifact that does not feel authentic to you.

### Best Practices

**Let Cursor work autonomously** - The rules are designed for minimal intervention
**Review CONTEXT.md** - This file guides the entire workflow  
**Use specific prompts** for modifications rather than micromanaging
**Check methodology.md** - Understand how Cursor approached the analysis
