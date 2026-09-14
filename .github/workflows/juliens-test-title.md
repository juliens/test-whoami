---
on:
  slash_command:
    name: title
permissions:
      contents: read
      issues: read
      pull-requests: read
      id-token: write
      
checkout: false

# Cache the pre-fetched diff/metadata/comments on the PR head SHA so a
# re-review of the same commit skips the GitHub API calls.
cache:
  key: pr-prefetch-${{ github.event.pull_request.head.sha }}
  path: /tmp/gh-aw/agent
  restore-keys:
    - pr-prefetch-${{ github.event.pull_request.number }}-

engine: 
  id: claude
  auth:
    type: github-oidc
    provider: anthropic
    federation-rule-id: fdrl_013Yw3g9LVvJzRJgQoP5zFnR
    organization-id: 797e3cc2-9e62-4091-a6e2-9bd04249babc
    service-account-id: svac_015rSKKoTmnBF2WbzqpemYW5
    workspace-id: wrkspc_01EZUP6bV8tj87UdRfaC3zKR
    
network:
  allowed:
    - defaults
    - go
tools:
  github:
    toolsets: [default]
safe-outputs:
  update-pull-request:
---

# juliens-test-title

Analyse the title of the PR and the content of the change, and verify that the title make sense for a changelog line.

Change the title to fit this.