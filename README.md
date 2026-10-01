# Data Legion for Claude

Enrich and search B2B person and company data from a conversation with Claude.

## What it does

This plugin connects Claude to the Data Legion MCP server and adds four skills that tell Claude how to use it well:

- **Enrich a list**: fill in titles, employers, contact details and firmographics for people or companies you share.
- **Find people**: build target lists with search over people and companies.
- **Research a company**: turn a company's size, growth and hiring data into a short brief.
- **Report a data issue**: flag a wrong or outdated record so Data Legion can fix it.

## Use it

Install the plugin, then connect the Data Legion connector from the plugin's Connectors tab and sign in with your Data Legion account. Signing in needs the admin or developer role. Then ask, for example: "Enrich jane.doe@acme.com", "Find product managers at fintech companies in New York", or "Give me a brief on stripe.com".

Each successful match uses a credit from your Data Legion account. Cleaning, validation and data-issue reports are free. Manage or disconnect the connection at https://www.datalegion.ai/dashboard/connected-apps.

## Data

The plugin sends the identifiers and search criteria you give Claude (for example an email address, a domain, or a job title and city) to Data Legion at https://api.datalegion.ai/mcp, and returns the matching records. It stores nothing itself. See https://www.datalegion.ai/legal/privacy-policy and https://www.datalegion.ai/docs/integrations/mcp-server.
