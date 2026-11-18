# 04 — Security architecture and trust boundaries

Standups raised object-level authorization (BOLA), token expiry, secure local storage, API security, untrusted code sandboxing, and a compromised local machine. Treat the desktop client as potentially hostile: client-side checks improve usability but cannot replace server authorization.

## Identity and authentication

Authentication establishes a principal; authorization evaluates allowed actions. OIDC is an identity layer on OAuth 2.0; OAuth itself is an authorization framework. JWT is a token format, not an authentication protocol or a substitute for validation. Learn access vs refresh tokens, expiry, revocation/rotation, session recovery, and safe native-app redirect handling. Use a maintained identity library and the current [OAuth Security BCP, RFC 9700](https://www.rfc-editor.org/rfc/rfc9700.html); consult [OpenID Connect Core](https://openid.net/specs/openid-connect-core-1_0.html) for OIDC semantics.

## Authorization

For every object request, check that the principal is allowed to perform that action on that exact candidate, assessment, answer, execution, or violation record. Check function-level roles, tenant boundaries, and object-level access; a guessed/changed object ID must not grant access. OWASP calls this Broken Object Level Authorization and recommends object-level checks for every endpoint that takes an object identifier ([OWASP API1:2023](https://api-security.owasp.org/editions/2023/en/0xa1-broken-object-level-authorization/)). Consider RBAC (roles) and ABAC (attributes/policy) according to access rules; follow least privilege. Minimize token scope/lifetime, store refresh credentials with OS-protected storage, redact logs, and recover queued work after reauthentication.

## Compromised client and network

Use TLS; validate payloads and enforce size/rate limits server-side. Assume local files can be read/modified if the device is compromised. Encrypt sensitive persisted data where appropriate, protect keys, and design server-side integrity checks. Bind uploaded execution outputs to authenticated session, code revision, and attempt.

For common web/API threats, study SQL injection, XSS, CSRF, SSRF, mass assignment, file-upload risks, secret management, encryption in transit/at rest, and resource exhaustion. Use allowlists and output encoding appropriate to the sink; avoid treating “input validation” as a universal SQL/XSS defense. The [OWASP API Security Top 10](https://devguide.owasp.org/en/07-training-education/07-api-top-ten/) is a threat checklist, not a complete security program.

For uploaded files, consider type/size validation, isolated parsing, malware scanning where appropriate, and storage outside executable/public paths. Apply rate limits and resource quotas to expensive endpoints and code execution.

## Sandboxing code execution

Untrusted candidate code belongs behind a strong isolation boundary with least privilege, resource/time limits, controlled network/filesystem access, and cleanup. The API/web process should not directly execute untrusted code with its own credentials. A sandbox reduces risk but needs defense in depth and monitoring.

Consider restricted file access, temporary-file cleanup, no arbitrary shell execution, safe IPC, limited outbound network, CPU/memory/process/time limits, and dependency/plugin risk. Test whether a candidate can reach another candidate's files or internal services. Protect secrets outside the sandbox and do not place general-purpose service credentials in the execution environment.

## Optional AI-agent threat model

Include this only if an AI agent reads untrusted candidate content or can call tools. Treat prompts/documents as untrusted input, constrain each tool to the minimum permission, validate tool arguments/results, bound loops/time/cost, log actions, and require human approval for high-impact actions. OWASP documents prompt injection and privilege minimization ([OWASP GenAI prompt injection](https://genai.owasp.org/llmrisk/llm01-prompt-injection/), [AI Agent Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html)). Prompt text alone is not an access-control boundary.

## Threat-model exercise

For each asset (answers, code, tokens, violations, results), identify attacker, entry point, impact, prevention, detection, and recovery. Test direct object-ID substitution between candidates, expired tokens mid-sync, malformed oversized uploads, and sandbox escape assumptions.

For tool-using agents, enforce tool allowlists/permissions server-side, validate arguments and outputs against schemas, use restricted credentials, require approval for consequential actions, bound loops/time/token/cost, and audit tool actions. Prompt instructions alone are not an access-control layer.
