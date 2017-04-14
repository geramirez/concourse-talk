---
# Concourse CI
---
## What we are going to learn.
- What is Concourse CI?
- Why use it?
- Concourse Elements
    - Tasks
    - Jobs
    - Resources
    - Pipelines
- Some examples
---
## Background
- Started by a CF engineer
- Created CF team was having difficulties with existing CI systems
- Maintained by Pivotal
---
## What is Concourse CI?
It's a continuous integration tool which creates environments and runs scripts.
What makes Concourse CI unique is that it forces users to declare configuration upfront.
---
## What does that mean?
- CI pipeline configurations and tasks can be checked into version control
- Workers will always have the same configurations and will be reconfigured before each task
- CI pipelines are completely reproducible
---
## Why use it?
1. No more snowflake server configurations  
2. Allows development teams to have more control of configurations  
3. Less ceremony around creating new tasks  
---
## Concourse Elements
- Tasks
- Jobs
- Resources
- Pipelines
---
## Tasks
The smallest configurable unit in a Concourse pipeline is a single task.
Ideally tasks are pure functions.
```yml
  - task: annoy
    config:
      run:
        path: echo
        args: ["Hey! Listen!"]
```
---
## Jobs
Determine the actions of your pipeline, how resources progress through it, and how everything is visualized. 
Jobs are composed of one or more tasks.
```yml
jobs:
- name: Notify
  plan:
  - task: annoy
    config:
      run:
        path: echo
        args: ["Hey! Listen!"]
```
---
## Resources
Resources are the inputs and outputs of jobs
```
resources:
- name: git-repo
  type: git
  source:
    uri: https://github.com/some-org/some-repo.git
    branch: master
```
---
## Pipelines
Combination of resources and jobs
![pipeline-image](https://concourse.ci/pipes.svg)
---
### Setup
```bash
docker-compose up
fly -t local login -c http://127.0.0.1:8080
# concourse/changeme
fly -t local set-pipeline -p demo -c 1-task-only.yml
```
---
### Resources types
[Link to resources](https://concourse.ci/resource-types.html)
