# kubectl-commands


### Update revision history for all deployments in a namespace
```shell
NS=my-namespace; kubectl -n $NS get deploy -o=jsonpath='{range .items[*]}{.metadata.name}{"\n"}{end}' | while read LINE; do kubectl -n $NS patch deployment $LINE -p '{"spec":{"revisionHistoryLimit":10}}'; done
```