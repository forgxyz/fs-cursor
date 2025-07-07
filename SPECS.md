# fs-cursor

## running thoughts / plan of action
the goal of this is to explore a workflow of doing flipside analytics within cursor with the following tools:
 - cursor pro
 - flipside mcp
 - snowflake login (optional)

inspiration:
 - https://x.com/Steve8708/status/1937657624138514766
    - 
 - https://github.com/sandeshsk12/Flipside_dashboard_porter
    - 

### needs
 - cursorrules (publish and maintain cursorrules)
    - inspo: http://github.com/elizaos/.cursor/
    - potential rules
        - always log generated sql
            - include a comment ? context as to what led to the sql generation ?
        - style guide

### features
 - migrate dashboard
 - maintain custom rules
 - publish artifact (use existing mcp tool publish_html for now, but keep notes on how this could/should change)
    - thoughts on artifacts - any chart that is generated should include the sql that generated the numbers. include a dropdown of some sort on methodology. ENFORCE TRANSPARENCY AND METHODOLOGY
        - https://flipsidecrypto.slack.com/archives/C08HR3W100Y/p1751386703510519?thread_ts=1751379475.069369&cid=C08HR3W100Y
 - snowflake extension showcasing how to continue to access the data directly
    - and maybe how to use YOUR queries as inspiration for the MCP to really steer it

maybe all of this distills into an analytics-starter repository
 - that way the migration tool is less a tool and a set of prompts or rules
 - dependent on what sandesh built
 - review query export csv
    - categorize by blockchain ? assess sql? idk 
    - there's only id, name, sql text. there's no dates or anything. that would have been very helpful...

### workflow
 1. enabling the flipside mcp server in cursor
    - general settings -> cursor settings -> mcp tools
    - add new mcp tool
    - json configuration w url and api key
    - have cursor test the tools! (remember to approve toolcall)
        - "Please test the flipside mcp tools with just a few tool calls. Concisely exmplain the capabilities they provide."

## resources
**tool documentation**  
 - https://docs.flipsidecrypto.xyz/welcome-to-flipside/flipside-growth-mcp#tools-you-can-call-for-advanced-users

**dashboard exporter**  
community built tool to export dashboards into an html artifact for preservation. This will be the starting point for our migration to mcp-led analytics.  
 - https://github.com/sandeshsk12/Flipside_dashboard_porter

**query csv cleaner**  
flipside's query export is not formatted well. tlm wrote a script to clean that up.
 - https://github.com/0xthelaughingman/csv-handler-temp
