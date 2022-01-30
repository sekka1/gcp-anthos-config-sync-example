
https://cloud.google.com/anthos-config-management/docs/tutorials/config-sync-helm#configure_your_repository


## namos cli

https://cloud.google.com/anthos-config-management/docs/how-to/nomos-command


```
nomos hydrate \
    --source-format=unstructured \
    --output=./nomos-output
```



## Another example of the kustomize route:

https://github.com/GoogleCloudPlatform/anthos-config-management-samples/tree/main/namespace-specific-policy

Doesnt seem to work

## Debug inside of the importers container:
Error in the `importers` container:
```
I0130 16:41:42.647368       1 reconcile.go:203] Resolved config dir: {/repo/root/ef52826ea86c644ac5d7e6c1e7a6da1ca57b8a7c/example2}. Polling config dir: /repo/root/rev/example2
W0130 16:41:42.662158       1 client.go:166] ResourceVersion for "configmanagement.gke.io/v1, Kind=Repo", "/repo" did not change during update (noop), updateFn should have indicated no update needed
I0130 16:41:42.666683       1 reconcile.go:241] listing policy files in /repo/root/ef52826ea86c644ac5d7e6c1e7a6da1ca57b8a7c/example2
W0130 16:41:42.696335       1 reconcile.go:267] Failed to parse: 3 error(s) 
[1] KNV2001: unmarshalerDecoder: Object 'Kind' is missing in '{"namespace":"team-a","resources":["../base"]}', error found in #10 byte of ...|../base"]}|..., bigger context ...|{"namespace":"team-a","resources":["../base"]}|...  path: /repo/root/ef52826ea86c644ac5d7e6c1e7a6da1ca57b8a7c/example2/team-a/kustomization.yaml  For more information, see https://g.co/cloud/acm-errors#knv2001 
[2] KNV2001: unmarshalerDecoder: Object 'Kind' is missing in '{"resources":["namespace.yaml"]}', error found in #10 byte of ...|ce.yaml"]}|..., bigger context ...|{"resources":["namespace.yaml"]}|...  path: /repo/root/ef52826ea86c644ac5d7e6c1e7a6da1ca57b8a7c/example2/base/kustomization.yaml  For more information, see https://g.co/cloud/acm-errors#knv2001 
[3] KNV2001: unmarshalerDecoder: Object 'Kind' is missing in '{"resources":["team-a"]}', error found in #10 byte of ...|"team-a"]}|..., bigger context ...|{"resources":["team-a"]}|...  path: /repo/root/ef52826ea86c644ac5d7e6c1e7a6da1ca57b8a7c/example2/kustomization.yaml  For more information, see https://g.co/cloud/acm-errors#knv2001 
I0130 16:41:42.707880       1 repostatus.go:186] No unreconciled commits but there are source/import errors. RepoStatus sync token will remain at "".
I0130 16:41:42.708305       1 client.go:168] Updated "configmanagement.gke.io/v1, Kind=Repo", "/repo" from ResourceVersion 3308409 to 3308446
```

Running the namose command inside of:
```
kubectl -n config-management-system exec -it  git-importer-667bdfbdb6-bq4cb -c importer bash
```

Getting this:
```
I have no name!@git-importer-667bdfbdb6-bq4cb:/repo/root/ef52826ea86c644ac5d7e6c1e7a6da1ca57b8a7c/example2$ nomos hydrate \
>     --source-format=unstructured \
>     --output=./nomos-output
Error: Kustomization file is detected, but Kustomize is not installed: exec: "kustomize": executable file not found in $PATH. Please install Kustomize and re-run the command.
```

Is this ran inside of this container?  Why isnt the `kustomize` binary there?

Maybe not...b/c im not really getting the same error as the logs.  Something more is going on here.

