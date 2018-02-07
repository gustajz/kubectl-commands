# kubectl-commands


### Update revision history for all deployments in a namespace
```shell
NS=my-namespace; kubectl -n $NS get deploy -o=jsonpath='{range .items[*]}{.metadata.name}{"\n"}{end}' | while read LINE; do kubectl -n $NS patch deployment $LINE -p '{"spec":{"revisionHistoryLimit":10}}'; done
```

### Patch resource limits and requests
```shell
export NS=my-namespace
export DEPLOY_NAME=my-deploy

kubectl -n $NS patch deployment $DEPLOY_NAME -p '{"spec":{"template":{"spec":{"containers":[{"name": "'$DEPLOY_NAME'", "resources":{"limits":{"cpu":"2000m","memory":"512Mi"}, "requests":{"cpu":"300m","memory":"256Mi"}}}]}}}}' 
```