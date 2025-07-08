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

The analytics workflow follows these key steps:

1. **Process Guidelines**: Read methodology rules for tracking your analytical process
2. **Autonomous Execution**: Execute commands and queries without manual approval
3. **Question Assessment**: Identify and scope the primary analytical question
4. **Data Sources**: Leverage Flipside MCP tools to access blockchain data
5. **Query Execution**: Run queries against the data warehouse autonomously
6. **Dashboard Building**: Create dashboards concurrently with analysis
7. **Validation**: Use external sources (especially DeFiLlama) for result validation
8. **Data Transparency and Validation**: Guidelines for citing data sources for external validation
