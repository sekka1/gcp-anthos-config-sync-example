https://cloud.google.com/anthos-config-management/docs/tutorials/config-sync-helm

This should be the simplest dir structure



Still fails with:
```
I0130 17:39:15.102180       1 client.go:168] Updated "/, Kind=", "/repo" from ResourceVersion 3332076 to 3332077
I0130 17:39:15.106548       1 reconcile.go:241] listing policy files in /repo/root/93b73209388e0dfd2fede73daee38596b6bf8d46/example3
W0130 17:39:15.149017       1 reconcile.go:267] Failed to parse: 2 error(s) 
[1] KNV2001: unmarshalerDecoder: Object 'Kind' is missing in '{"helmCharts":[{"name":"cert-manager","namespace":"cert-manager","releaseName":"my-cert-manager","repo":"https://charts.jetstack.io","version":"v1.5.3"}]}', error found in #10 byte of ...|v1.5.3"}]}|..., bigger context ...|"https://charts.jetstack.io","version":"v1.5.3"}]}|...  path: /repo/root/93b73209388e0dfd2fede73daee38596b6bf8d46/example3/base/kustomization.yaml  For more information, see https://g.co/cloud/acm-errors#knv2001 
[2] KNV2001: unmarshalerDecoder: Object 'Kind' is missing in '{"patches":[{"path":"ignore-deployment-mutation-patch.yaml","target":{"kind":"Deployment"}}],"resources":["base"]}', error found in #10 byte of ...|:["base"]}|..., bigger context ...|get":{"kind":"Deployment"}}],"resources":["base"]}|...  path: /repo/root/93b73209388e0dfd2fede73daee38596b6bf8d46/example3/kustomization.yaml  For more information, see https://g.co/cloud/acm-errors#knv2001 
I0130 17:39:15.158880       1 repostatus.go:186] No unreconciled commits but there are source/import errors. RepoStatus sync token will remain at "".
I0130 17:39:15.159461       1 client.go:168] Updated "configmanagement.gke.io/v1, Kind=Repo", "/repo" from ResourceVersion 3332077 to 3332078
```

# Enable Root Sync

https://cloud.google.com/anthos-config-management/docs/how-to/migrate-multi-repo

