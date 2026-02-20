# Task 1

## What I implemented

- Created branch `feature/lab3` from the current `origin/main`.
- Added `.github/workflows/github-actions-demo.yml` using the GitHub Actions quickstart template.
- Pushed the workflow and monitored execution logs.

## Successful workflow run (push trigger)

- Run URL: https://github.com/Corbonat/DevOps-Intro/actions/runs/22241895572
- Trigger: `push` event on branch `feature/lab3`.
- Result: `success`.

## Key concepts learned

- **Workflow**: YAML file in `.github/workflows/`.
- **Trigger (`on`)**: event that starts the workflow (`push`).
- **Job**: a group of steps executed on one runner.
- **Step**: one command or one reusable action.
- **Runner**: GitHub-hosted VM (`ubuntu-latest`) that executes the job.

## Short execution analysis

The push event started one job (`Explore-GitHub-Actions`).  
The job executed step-by-step: event info output, runner/repository info output, `actions/checkout@v5`, file listing, and final status output.  
The run finished successfully, confirming that the workflow is discovered and executed correctly by GitHub Actions.

# Task 2

## Workflow changes made

- Added `workflow_dispatch` under `on:` for manual starts.
- Added step `Gather runner system information` with runner, OS, CPU, memory, and disk commands.

```yaml
on:
  push:
  workflow_dispatch:

jobs:
  Explore-GitHub-Actions:
    steps:
      - name: Gather runner system information
        run: |
          echo "Runner OS: $RUNNER_OS"
          lscpu
          free -h
          df -h /
```

## Successful runs for Task 2

- Push run URL: https://github.com/Corbonat/DevOps-Intro/actions/runs/22242141290
- Manual run URL (`workflow_dispatch`): https://github.com/Corbonat/DevOps-Intro/actions/runs/22242153683
- Both runs finished with `success`.

## Gathered system information (from logs)

```text
Runner OS: Linux
Runner architecture: X64
Kernel: Linux 6.11.0-1018-azure
CPU(s): 4
Model name: AMD EPYC 7763 64-Core Processor
Mem: 15Gi total
Disk (/dev/root): 145G total, 53G used, 92G available
```

## Manual vs automatic trigger

- `push`: starts automatically when a commit is pushed.
- `workflow_dispatch`: starts only when manually triggered by a user.
- In my runs, both trigger modes executed the same job and both succeeded.

## Runner environment analysis

The workflow used a GitHub-hosted Linux runner (`ubuntu-latest`) with predictable CI resources (4 vCPU, ~15 GiB RAM).  
This environment is suitable for repeatable build/test tasks and is recreated for each run, which improves isolation and consistency.
