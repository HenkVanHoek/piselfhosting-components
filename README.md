# PiSelfhosting Components Repository

This repository serves as the central directory for all Docker Compose templates and metadata definitions used by the PiSelfhosting platform.

## Architecture & Workflow

The PiSelfhosting ecosystem operates on a two-way synchronization model:

```mermaid
graph TD
    A[Remote Repository] -->|1. Fetch/Sync All| B[Local PiSelfhosting Application]
    B -->|2. Edit / Add Component| C[PiSelfhosting Component Editor]
    C -->|3. Validate & Upload| A
```

### 1. Developer Role (Write Access)
- The developer uses the **PiSelfhosting Component Editor** to create or modify components.
- The editor has a built-in **Git Authorization Check** to verify push permissions. Only authorized developers with write permissions (either via SSH keys or Personal Access Tokens) can push updates.
- If additional contributors are added, they must be granted write access to this repository on GitHub.
- When an authorized developer triggers the upload action, the editor performs a pre-flight metadata validation check on the template header before pushing changes.

### 2. End-User Role (Read Access / Sync)
- Regular users run the PiSelfhosting application locally.
- Regular users fetch and import the latest component metadata and templates from this repository directly into their local environment.
- End-users do not need write permissions; they only read the public definitions.

## Component File Standards

All template files (e.g., `docker-compose.template.yml`) must start with the following uniform metadata header:

```yaml
# status: "untested"
# last_tested_version: "none"
# platform_notes: "None"
# breaking_changes: "None"
```

- **status**: Can be `untested`, `testing`, `tested`, or `deprecated`.
- **platform_notes**: Specifically notes platform details (for example, "Targeted for ARM architecture." if the container runs on Raspberry Pi architecture).

## Contributing

1. Clone this repository or edit via the **PiSelfhosting Component Editor**.
2. Add your component and write standard docker compose templates.
3. Validate templates using the linter within the Component Editor before pushing.
