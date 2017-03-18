---
# Concourse CI
---
## What we are going to learn.
- What is it?
- Why use it?
- Concourse Primitives
    - Jobs
    - tasks
    - resources
- How to test and deploy and web app using Concourse.
---
## What is Councourse CI?
Is a continious integration tool, which allows/forces users to declare all their CI pipelines configurations in yaml a dsl, script, or container. 
---
### What does that mean?
- CI pipeline configurations and tasks can be checked into version control
- CI pipeline configurations are not dependent on the state of the servers running the pipeline
- CI pipelines are completely reproducable
---
### Why use it?
1. No more snowflake server configurations. 
2. Allows development teams to have more control of configurations.
3. Less ceremony around creating new tasks.
---
### Example

```
docker-compose up
fly -t lite login -c http://127.0.0.1:8080
fly -t lite set-pipeline -p tasks -c tasks-only.yml
```

```
resources:
- name: every-1m
  type: time
  source: {interval: 1m}

jobs:
- name: navi
  plan:
  - get: every-1m
    trigger: true
  - task: annoy
    config:
      platform: linux
      image_resource:
        type: docker-image
        source: {repository: ubuntu}
      run:
        path: echo
        args: ["Hey! Listen!"]
```
