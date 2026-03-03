## GitHub 101

### Self GitHub Runners

TODO

### Workflows

#### Event Types

TODO

#### ChatOps Approach

 TODO
 
### Rate Limited Docker Pull

#### Issue

Sometimes running the CI pipeline the following issue comes:

```
/usr/bin/docker pull snyk/snyk:docker
Error response from daemon: error from registry: You have reached your unauthenticated pull rate limit. https://www.docker.com/increase-rate-limit
```

The Azure infra looks like this for the management cluster:
```
Load balancers ➡️[Load balancer name] ➡️ Settings ➡️Backend pools

aksOutboundBAckendPool(4)
kubernetes(4)
```

Checking the outbound rules:
```
Load balancers ➡️[Load balancer name] ➡️ Settings ➡️Outbound rules

aksOutboundRule ➡️aksOutboundBAckendPool
```

So this means that the egress traffic goes via a Load balancer which has 1 IPv4 address.

On the GitHub Workflow side the code looks like this:
```
- name: Run Snyk Container Scan
  uses: snyk/actions/docker@master
```

Which uses the following repo code (downloaded before any defined step):
https://github.com/snyk/actions/blob/master/docker/action.yml

Which uses an unauthenticated user, so the rate limiting may happen at Docker side.

#### Solution A

Use a non-docker provided script which runs directly in the runner and provide the corresponding parametrisation:
```
snyk/actions/node
snyk/actions/setup
```

#### Solution B

Fork the existing action https://github.com/snyk/actions/blob/master/docker/action.yml and
create our own script.

First we manually mirror the docker image to our image registry.

Secondly in the forked repository we override the image to use our image registry instead of docker hub.

