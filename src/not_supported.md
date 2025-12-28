# Unsupported functionality

While we try to implement all features of Bamboo Runners, due to design choices and manpower available it's not possible
to make `actoo` completely compatible.  

Here is a list of features that is (yet) to be implemented or is decided as not going to be worked on
by `actoo` maintainers.

## Planned

- **CLI surface**
  - `bambact validate <path>` (syntax + schema validation; exit codes)
  - `bambact run plan <path> --plan <key> [--stage <name>] [--job <name>]`
  - `bambact run deploy <path> --project <key> --env <name> [--release <id>]`
  - `bambact list` (enumerate detected plans/deployments, stages, jobs, environments)
  - `bambact doctor` (runtime checks: docker availability, git, filesystem permissions)
  - Machine-readable output (`--json`) and quiet/verbose modes

- **Input formats and discovery**
  - Parse **Bamboo Specs YAML** (multiple files; repository layout discovery)
  - Parse **Bamboo Java Specs** (compile/load and read specs from compiled sources)
  - Support Specs version handling (e.g., `version: 2` style configs)
  - Deterministic merge/precedence rules when multiple specs define overlapping entities
  - Clear diagnostics with file/line pointers (YAML) and class/method pointers (Java Specs)

- **Validation**
  - YAML parse + structural validation for:
    - Plan definitions (project/plan keys, naming constraints, uniqueness)
    - Stage/job graph (ordering, parallelism constraints)
    - Task schemas (required fields, mutually exclusive options)
    - Variables (name rules, scope rules, reserved names)
    - Artifact definitions and references
  - **Java Specs validation**
    - Compile-time checks surfaced as CLI diagnostics (compile errors, missing deps)
    - Reflection/introspection validation for supported constructs only (plans, deployments, tasks)
    - Fail with clear mapping to Java class + line where possible (via compiler diagnostics)
  - Semantic validation:
    - Referenced jobs/stages/environments exist
    - Artifact producers/consumers are consistent
    - Requirements/capabilities are satisfiable by the selected runner
    - Docker runner settings are coherent (image, volumes, working dir)

- **Java Specs parse/validation pipeline (required for “Java Specs support”)**
  - Discover Java Specs entry points (convention + configurable package/class patterns)
  - Resolve dependencies (local Maven repo, Gradle cache, or explicit `--classpath`)
  - Build strategies:
    - Use Gradle/Maven wrapper if present (preferred)
    - Fallback: `javac` with provided classpath
  - Execute/instantiate spec classes in a sandboxed JVM:
    - Limit filesystem access to workspace (best-effort)
    - Pass variables into JVM via env/system properties
  - Extract model:
    - Plans, stages, jobs, tasks
    - Deployment projects, environments, tasks/final tasks
    - Variables and artifact definitions
  - Convert extracted model into the **same internal IR** as YAML for unified execution/validation

- **Execution model**
  - Plan execution model aligned to Bamboo concepts:
    - Plan → stages (sequential) → jobs (parallel within stage) → tasks (sequential within job)
  - Deployment execution model:
    - Deployment project → environments → tasks + final tasks
    - Include default deployment environment steps where expected (e.g., clean working directory + artifact download)
  - Cancellation and timeouts:
    - Global timeout, per-task timeout, graceful termination, hard kill

- **Runner environments**
  - Run in:
    - Host process mode (optional)
    - **Docker-only mode** (primary): per-job container or per-plan container
  - Container concerns:
    - Workspace mount + isolated working directories
    - UID/GID mapping, file permission normalization
    - Network control (default bridge; optional offline mode)
    - Volume cache support (e.g., dependency caches)

- **Core task support (must-have parity)**
  - **Checkout**
    - Git checkout (branch, tag, commit; shallow; submodules optional)
    - Credentials injection (SSH key, HTTPS token) via env/secret providers
  - **Clean working directory**
    - Exact clean semantics per step (job-level, stage-level)
  - **Script**
    - Inline script and script file execution
    - Shell selection (`sh`, `bash`, `pwsh` where applicable)
    - Working directory control
    - Environment variables injection
    - Return-code handling (fail/continue options)
  - **Artifacts**
    - Produce/publish artifacts (patterns, required vs optional behavior)
    - Consume/download artifacts between stages (shared artifacts behavior)
  - **Variables / Inject variables**
    - Read variables from `key=value` file
    - Export variables for later tasks/stages and for deployment handoff
  - **Final tasks**
    - Ensure “final tasks” always run (even on failure) for both plans and deployments

- **Additional tasks commonly needed for “complete” coverage**
  - Test result parsing hooks (at least pluggable interface)
  - Docker task primitives (build/push/login) or documented patterns via `script`
  - Dependency download/cache primitives (or first-class cache API)
  - Notification stubs (no-op locally, but validate configuration)
  - Manual gates/approvals (simulate via prompt/flag; validate presence)

- **Variables, parameters, and scope**
  - Support variable sources:
    - Spec-defined variables
    - CLI `--var KEY=VAL`
    - Environment variables passthrough/allowlist
    - Injected-from-file variables
  - Variable precedence rules (documented and deterministic)
  - Scope handling:
    - Global → plan → stage → job → task
    - Plan-to-deployment variable passing

- **Artifacts and workspace semantics**
  - Artifact store abstraction:
    - Local filesystem backend
    - Optional OCI/object-store backend interface (future)
  - Artifact integrity:
    - Missing required artifact should fail builds where required
    - Checksums/manifest support
  - Cross-stage automatic downloads consistent with Bamboo Specs expectations

- **Concurrency and scheduling**
  - Parallel jobs with configurable max concurrency
  - Resource locks (workspace locks; named locks for shared resources)
  - Deterministic ordering and reproducibility (seeded temp paths, stable log ordering)

- **Logging and observability**
  - Structured logs + human logs
  - Per-task log sections with timing, exit code, stdout/stderr capture
  - Artifacts of execution:
    - Run summary (JSON)
    - Console log file
    - Metadata manifest (variables, produced artifacts, task outcomes)

- **Exit codes and failure policy**
  - Clear exit codes:
    - Validation error vs execution failure vs internal error
  - Failure behaviors:
    - Fail-fast vs continue-on-error per task
    - Final tasks always run
    - Mark unstable vs failed (optional)

- **Security and secrets**
  - Secret inputs via:
    - Env vars
    - Mounted files
    - External secret provider interface (stub initially)
  - Redaction in logs (pattern-based + explicit “secret” variables)
  - Safe command echoing (no leaking secrets)

- **Extensibility**
  - Plugin/task interface:
    - Register new tasks with schema + executor
    - Versioned task APIs
  - Compatibility layer for Bamboo task identifiers (mapping YAML/Java task types → executors)

- **Compatibility targets**
  - Support both:
    - Build plans (stages/jobs/tasks)
    - Deployment projects/environments/tasks)
  - Handle Bamboo Specs repository patterns (multiple plans/deployments in one repo)


## Functionality that is not going to be worked on

TBD
