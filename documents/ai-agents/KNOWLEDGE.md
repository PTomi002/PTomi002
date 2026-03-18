### Gas Town

Create ***Town*** an existing dir:
```
gt install . --git
```

Start all daemon services:
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
```

Attach ***Crew Members*** to the ***Rigs***:
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

Start a feature development:
```
gt convoy create "Release prep" gt-abc --notify           # defaults to mayor
```
