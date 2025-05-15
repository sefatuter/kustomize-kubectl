#

```
kubectl kustomize overlays/dev

Dev deploy: kubectl apply -k overlays/dev
Prod deploy: kubectl apply -k overlays/prod
```

## Run Kustomize commands sequentially

- Preview what will be applied
```bash
kubectl kustomize overlays/dev
```

- Apply to the cluster
```bash
kubectl apply -k overlays/dev
```

- Apply to the cluster
```bash
kubectl get all -l app=hello
```

- View differences after you edit something
```bash
kubectl diff -k overlays/dev
```

- Delete everything you just created
```bash
kubectl delete -k overlays/dev
```
```bash
kubectl apply --dry-run=client -o yaml -k overlays/dev
```

| Goal                                | Command                                          |
| ----------------------------------- | ------------------------------------------------ |
| **See what you’ll apply**           | `kubectl kustomize overlays/dev`                 |
| **Apply everything**                | `kubectl apply -k overlays/dev`                  |
| **Show a diff against the cluster** | `kubectl diff -k overlays/dev` *(kubectl 1.18+)* |
| **Delete everything you deployed**  | `kubectl delete -k overlays/dev`                 |
| **Dry-run server-side**             | `kubectl apply -k overlays/dev --server-dry-run` |

```
app/
└── base/
    ├── deployment.yaml
    ├── service.yaml
    └── kustomization.yaml         # lists the two files above
└── overlays/
    ├── dev/
    │   ├── kustomization.yaml     # sets replica 1, ClusterIP svc
    │   └── deployment-replica.yaml
    ├── staging/
    │   └── kustomization.yaml     # patches Service -> NodePort
    └── prod/
        └── kustomization.yaml     # replica 4, Service -> LoadBalancer
```

- Kustomize is just the “sticky notes” system:
keep one original YAML file and add tiny overlay notes to change it for dev, test, prod, or any other variant—no copy-pasting entire files.