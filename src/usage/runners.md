# Runners and Capabilities

Bamboo does not offer managed virtual environments like GitHub Actions. Instead, it relies on
[agents](https://confluence.atlassian.com/bamboo/configuring-agents-289277283.html) to run build plans.
By default, `actoo` uses `alpinelinux/docker-cli:latest` Docker image to run the workflows with docker-only support.
However, if you need something more specific, like sumulating a particular OS or pre-installed tools, you can specify
a custom Dockerfile to use as the runner for your workflows.

In order to specify a custom agent image, you can create a "actoo-runners.json" file in the root of your repository or
specify it via the `--runners` command line option. See below for details.

## `actoo-runners.json` specification

This file allows you to define custom runners for your workflows. It allows to specify either a Docker image
or a Dockerfile path for each runner and, if needed, additional capabilities that the runner provides.

When `actoo` runs a workflow, it checks the `requirements` required by the jobs in the workflow and matches them
against the capabilities defined for each runner in the `actoo-runners.json` file. If a runner satisfies all
the required capabilities, it is selected to run the job. If no runner matches the required capabilities,
an error is raised. If multiple runners match, the first one defined in the file is selected.

The structure of the file is as follows:

```json
{
    "runners": {
        "<runner-key>": {
            "image": "<docker-image-or-dockerfile-path>",
            "dockerfile": "<optional-dockerfile-path>",
            "capabilities": {
                "<capability-name>": "<capability-value>"
            }
        }
    }
}
```

`image` and `dockerfile` fields are mutually exclusive. If both are specified, an error is raised.

### Example `actoo-runners.json`

```json
{
    "runners": {
        "ubuntu-latest": {
            "image": "ubuntu:latest",
            "capabilities": {
                "os": "linux",
                "arch": "x86_64"
            }
        },
        "custom-agent": {
            "dockerfile": "./Dockerfile.custom-agent",
            "capabilities": {
                "os": "linux",
                "arch": "x86_64",
                "docker": "20.10.7"
            }
        }
    }
}
```
