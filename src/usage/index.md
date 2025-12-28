# Usage guide

## Events

Bamboo does not have explicit event system, the closest equivalent
are [triggers](https://confluence.atlassian.com/bamboo/configuring-triggers-289277087.html) that can start a build plan
based on certain conditions.

So, `actoo` has an event system that is inspired by GitHub Actions events. It supports:

- `push` - simulates a code push to the repository
- `pull_request` - simulates a pull request creation or update
- `schedule` - simulates a scheduled run of the workflow
- `workflow_dispatch` - simulates a manually triggered workflow run

---

### `push` event

Command: `actoo push`

Properties set:

TBD

### `pull_request` event

Command: `actoo pull_request`

Properties set:

TBD

### `schedule` event

Command: `actoo schedule`

Properties set:

TBD

### `workflow_dispatch` event

Command: `actoo workflow_dispatch`

Properties set:

- No additional properties are set by default for this event.

---

To list all workflows for a given event, use `-l`/`--list`:

```shell=sh
actoo -l pull_request
```
