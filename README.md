# fs-cursor

This repository defines cursor rules for using the Flipside MCP tools as a data analyst. It provides a comprehensive framework for blockchain analytics workflows and is designed to help analysts transition from SQL-based dashboards to MCP-driven workflows and artifacts. It is in early stages and constantly evolving. I hope that these rules make it a bit easier to use the Flipside MCP tools to derive insights and build great work!

## Target Audience

This repository is aimed at analysts who previously had SQL-based dashboards deployed to Flipside's Data Studio and are looking to evolve their analytical workflows using modern MCP (Model Context Protocol) tools.

## Integration with dashboard-dl

This repository is designed to work alongside the [dashboard-dl tool](https://github.com/forgxyz/dashboard-dl), which helps analysts:
- Extract existing SQL dashboards from Data Studio
- Convert them into MCP-driven workflows
- Create modern analytical artifacts

## Repository Structure

### .cursor/rules/

The `.cursor/rules/` directory contains the core rule definitions:

- **analytics_workflow.mdc** - Meta prompt for blockchain analytics questions (always applied)
- **flipside_mcp_tools_public.mdc** - Instructions for using Flipside MCP tools
- **generate_dashboard.mdc** - Guidelines for dashboard creation
- **log_methodology.mdc** - Process tracking and methodology guidelines
- **run_commands_autonomously.mdc** - Autonomous command execution rules
- **style_guide.mdc** - Formatting and presentation standards

## Getting Started

1. **Prerequisites**: Ensure you have the dashboard-dl tool installed and configured
2. **Rule Setup**: Copy the `.cursor/rules/` directory to your project
3. **Workflow**: Use the analytics_workflow.mdc rule as your entry point for blockchain analytics questions

## Workflow Overview

The analytics workflow follows these key steps:

1. **Process Guidelines**: Read methodology rules for tracking your analytical process
2. **Autonomous Execution**: Execute commands and queries without manual approval
3. **Question Assessment**: Identify and scope the primary analytical question
4. **Data Sources**: Leverage Flipside MCP tools to access blockchain data
5. **Query Execution**: Run queries against the data warehouse autonomously
6. **Dashboard Building**: Create dashboards concurrently with analysis
7. **Validation**: Use external sources (especially DeFiLlama) for result validation

## Key Features

- **Data-Driven Analysis**: Always query the warehouse first for metrics
- **Autonomous Operations**: Execute queries without manual intervention
- **Iterative Development**: Build analysis and dashboards incrementally
- **External Validation**: Cross-reference results with trusted sources
- **Documented Process**: Track methodology and decision-making

## Contributing

This repository is part of the Flipside analytics ecosystem. For issues or contributions, please coordinate with the Flipside team.

