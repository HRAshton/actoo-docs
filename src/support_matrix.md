# Supported options in `bamboo.yaml` (Build & Deployment Specs)

## **This document is work in progress**

This checklist enumerates **all known Bamboo YAML Specs attributes** for **Build Plans** and **Deployment Projects**.
Unchecked items indicate not yet supported / partially supported in BambAct.

---

## Global / Repository-level

- [ ] `version`
- [ ] `bamboo-specs` (implicit root)
- [ ] `triggers`
- [ ] `notifications`
- [ ] `variables`
- [ ] `permissions`
- [ ] `labels`
- [ ] `dependencies`
- [ ] `requirements`
- [ ] `repositories`

---

## Build Plans

### Plan Definition

- [ ] `project`
    - [ ] `key`
    - [ ] `name`
- [ ] `plan`
    - [ ] `key`
    - [ ] `name`
    - [ ] `description`
    - [ ] `enabled`
    - [ ] `linked-repositories`
    - [ ] `variables`
    - [ ] `triggers`
    - [ ] `notifications`
    - [ ] `labels`
    - [ ] `dependencies`
    - [ ] `branch-management`
    - [ ] `branches`
    - [ ] `permissions`

---

### Stages

- [ ] `stages`
    - [ ] `<stage>`
        - [ ] `name`
        - [ ] `description`
        - [ ] `manual`
        - [ ] `final`
        - [ ] `jobs`

---

### Jobs

- [ ] `<job>`
    - [ ] `key`
    - [ ] `name`
    - [ ] `description`
    - [ ] `enabled`
    - [ ] `requirements`
    - [ ] `other-tasks`
    - [ ] `artifacts`
    - [ ] `variables`
    - [ ] `clean-working-directory`
    - [ ] `checkout`
    - [ ] `tasks`
    - [ ] `final-tasks`
    - [ ] `docker`
        - [ ] `image`
        - [ ] `volumes`
        - [ ] `environment`
        - [ ] `network`
    - [ ] `timeout`
    - [ ] `conditions`

---

### Tasks (Build)

#### Common Task Attributes

- [ ] `task`
    - [ ] `type`
    - [ ] `description`
    - [ ] `enabled`
    - [ ] `conditions`
    - [ ] `final`
    - [ ] `timeout`
    - [ ] `environment`

---

#### Script Task

- [ ] `script`
    - [ ] `interpreter`
    - [ ] `inline`
    - [ ] `file`
    - [ ] `working-dir`
    - [ ] `arguments`
    - [ ] `environment`
    - [ ] `fail-on-error`

---

#### Checkout Task

- [ ] `checkout`
    - [ ] `repository`
    - [ ] `path`
    - [ ] `force-clean-build`

---

#### Artifact Tasks

- [ ] `artifacts`
    - [ ] `definitions`
        - [ ] `name`
        - [ ] `location`
        - [ ] `pattern`
        - [ ] `shared`
        - [ ] `required`
    - [ ] `subscriptions`
        - [ ] `artifact`
        - [ ] `destination`
        - [ ] `required`

---

#### Inject Variables Task

- [ ] `inject-variables`
    - [ ] `file`
    - [ ] `scope`
    - [ ] `namespace`

---

#### Test Parser Task

- [ ] `test-parser`
    - [ ] `type`
    - [ ] `result-path`
    - [ ] `fail-on-error`

---

---

## Deployment Projects

### Deployment Definition

- [ ] `deployment`
    - [ ] `project`
        - [ ] `key`
        - [ ] `name`
        - [ ] `description`
    - [ ] `variables`
    - [ ] `permissions`
    - [ ] `notifications`

---

### Environments

- [ ] `environments`
    - [ ] `<environment>`
        - [ ] `name`
        - [ ] `description`
        - [ ] `requirements`
        - [ ] `variables`
        - [ ] `triggers`
        - [ ] `notifications`
        - [ ] `tasks`
        - [ ] `final-tasks`

---

### Tasks (Deployment)

#### Common Deployment Task Attributes

- [ ] `task`
    - [ ] `type`
    - [ ] `description`
    - [ ] `enabled`
    - [ ] `conditions`
    - [ ] `final`
    - [ ] `timeout`
    - [ ] `environment`

---

#### Script Task (Deployment)

- [ ] `script`
    - [ ] `interpreter`
    - [ ] `inline`
    - [ ] `file`
    - [ ] `working-dir`
    - [ ] `arguments`
    - [ ] `environment`
    - [ ] `fail-on-error`

---

#### Artifact Download Task

- [ ] `download-artifacts`
    - [ ] `artifacts`
        - [ ] `name`
        - [ ] `destination`
        - [ ] `required`

---

#### Manual Approval Task

- [ ] `manual`
    - [ ] `message`
    - [ ] `timeout`

---

## Branch & Advanced Features

- [ ] `plan-branches`
    - [ ] `create`
    - [ ] `delete`
    - [ ] `merge-strategy`
- [ ] `dependencies`
- [ ] `custom-tasks`
- [ ] `capabilities`
- [ ] `agent-requirements`
- [ ] `conditions`
- [ ] `expressions`

---

## Java Specs Parity (for reference)

- [ ] `Plan`
- [ ] `Stage`
- [ ] `Job`
- [ ] `Task`
- [ ] `Artifact`
- [ ] `DeploymentProject`
- [ ] `Environment`
- [ ] `Variable`
- [ ] `Requirement`
- [ ] `Trigger`
- [ ] `Notification`
