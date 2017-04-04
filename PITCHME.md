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
## What is Concourse CI?
Is a continuous integration tool, which allows/forces users to declare all their CI pipelines configurations in yaml a dsl, script, or container. 
---
## What does that mean?
- CI pipeline configurations and tasks can be checked into version control
- CI pipeline configurations are not dependent on the state of the servers running the pipeline
- CI pipelines are completely reproducible
---
## Why use it?
1. No more snowflake server configurations  
2. Allows development teams to have more control of configurations  
3. Less ceremony around creating new tasks  
---
## Concourse Primitives
Concourse Elements
- Tasks
- Jobs
- Resources
- Pipelines
---
## Tasks
The smallest configurable unit in a Concourse pipeline is a single task.
Ideally tasks are pure functions: given the same set of inputs, it should either always succeed with the same outputs or always fail.
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
Resources are objects serve as inputs and outputs for the pipeline
```
resources:
- name: concourse
  type: git
  source:
    uri: https://github.com/concourse/concourse.git
    branch: master
```
---
## Pipelines
Combination of resources and jobs
---
### Example
```bash
docker-compose up
fly -t local login -c http://127.0.0.1:8080
fly -t local set-pipeline -p demo -c tasks-only.yml
```
---
### Resources types
[Link to resources](https://concourse.ci/resource-types.html)
