```
kustom-two-way/
├── apps/
│   ├── api/
│   │   ├── base/
│   │   │   ├── deployment.yaml
│   │   │   ├── service.yaml
│   │   │   └── kustomization.yaml
│   │   └── overlays/
│   │       ├── dev/kustomization.yaml
│   │       ├── staging/kustomization.yaml
│   │       └── prod/kustomization.yaml
│   └── web/
│       ├── base/
│       │   ├── deployment.yaml
│       │   ├── service.yaml
│       │   └── kustomization.yaml
│       └── overlays/
│           ├── dev/kustomization.yaml
│           ├── staging/kustomization.yaml
│           └── prod/kustomization.yaml
└── envs/
    ├── dev/kustomization.yaml
    ├── staging/kustomization.yaml
    └── prod/kustomization.yaml
```

```bash
# Deploy ONLY api to prod
kubectl apply -k apps/api/overlays/prod

# Deploy the entire dev environment (api + web)
kubectl apply -k envs/dev

# See what would change in prod
kubectl diff -k envs/prod

# Remove staging environment
kubectl delete -k envs/staging
```

- By setting up a two-axis Kustomize structure, now able to deploy every application to every environment with a single command and copyless YAML.
- structure can scale to n in the application dimension and n in the environment dimension.