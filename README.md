# mermaid

##  Jira OAuth 2.0 Flow

```mermaid
sequenceDiagram
    participant User
    participant Your_App
    participant Jira_Auth_Server
    participant Jira_API

    User->>Your_App: Click "Login with Jira"
    Your_App->>Jira_Auth_Server: Redirect with client_id, scope, redirect_uri
    Jira_Auth_Server->>User: Show Login + Consent Screen
    User-->>Jira_Auth_Server: Authenticate + Approve
    Jira_Auth_Server-->>Your_App: Redirect with authorization code
    Your_App->>Jira_Auth_Server: Exchange code for access token
    Jira_Auth_Server-->>Your_App: access_token (+ optional refresh_token)
    Your_App->>Jira_API: Call API with Bearer access_token
    Jira_API-->>Your_App: JSON response with Jira data
