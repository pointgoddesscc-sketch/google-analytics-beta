# Deployment guidance

This project is a Python-based Model Context Protocol (MCP) server for Google
Analytics APIs. It is not a Next.js or static web application, so it should not
be deployed to Vercel as a one-link website in the same way as an `apps/docs` or
`apps/web` frontend project.

## Recommended usage

Run the server from a local MCP-compatible client, such as Gemini CLI or Gemini
Code Assist, using the package entry point documented in the main README.

```json
{
  "mcpServers": {
    "analytics-mcp": {
      "command": "pipx",
      "args": ["run", "analytics-mcp"],
      "env": {
        "GOOGLE_APPLICATION_CREDENTIALS": "PATH_TO_CREDENTIALS_JSON",
        "GOOGLE_PROJECT_ID": "YOUR_PROJECT_ID"
      }
    }
  }
}
```

## Why Vercel is not the right target

Vercel is optimized for web frontends and serverless functions. This repository
provides an MCP server that communicates over the protocol expected by MCP
clients and requires Google Analytics credentials at runtime. Deploying it as a
public web link would not provide a useful browser-facing application and could
risk exposing an interface that should remain tied to trusted clients and
credentials.

## If you need a public web application

Create a separate frontend application that calls a backend you control. Keep the
Google Analytics credentials on the backend, and never expose credential files or
OAuth secrets to browser code. The frontend can then be deployed to a platform
such as Vercel, while the backend runs on an environment designed for long-lived
services or authenticated API endpoints.
