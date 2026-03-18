### Gas Town

#### Technologies

##### Beads

Beads CLI is an AI-native issue tracker and memory system, Jira for AI Agents to track their progress.

A Bead represents tasks in a Directed Acyclic Graph, as the AI Agent discovers tasks, it will create Beads, which will be versioned controlled in Dolt.

As you work on branches the memory of what we are doing on that branch stays there.

As we progress on the beads, we can sync it to share with other agents.

e.g.: Login System
```
Bead #1 User Table Schema
Description: XYZ

Bead #2 Password Hashing
Description: ABC
Requires #1

Bead #3 Login Logic
Description: GHJ
Requires #1 #2

...
```

##### Dolt

Dolt is essentially "Git for Data." 

It is a SQL database that you can fork, clone, branch, merge, and push/pull just like a Git repository, so the project memory became brancheable.

e.g.: on a branch feature/XYZ the AI Agents wont see tasks or bugs from the main branch, so their context wont be polluted, and it will see the branch specific beads.

#### Workflow

Create ***Town*** an existing / new dir:
```
gt install . --git
gt install mini-infra --git
```

Start / Stop all daemon services:
```
gt up
gt shutdown
```

Login to GitHub
```
gh auth login
```

Attach ***Rigs*** to the ***Town***:
```
gt rig add mini_devops_infra https://github.com/PTomi002/mini-devops-infra
gt rig add product_producer https://github.com/PTomi002/product-producer
gt rig add product_consumer https://github.com/PTomi002/product-consumer
```

(Optional) Attach ***Crew Members*** to the ***Rigs*** for long-running, exploratory tasks:
```
gt crew add crew_mini_infra_01 --rig mini_devops_infra
gt crew add crew_product_producer_01 --rig product_producer
```

Open dashboard:
```
gt dashboard --port 3000
gt dashboard --open
```

Attach ***Mayor*** to the current terminal:
```
gt mayor attach
```

Start a feature development in the ***Mayor*** session:
```
gt mayor attach
gt convoy create "Release prep" gt-abc --notify --base-branch feat/test
```

Check real-time progress of the tasks:
```
gt feed
```



