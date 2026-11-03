# devops-labs-gitops

GitOps-репозиторій конфігурації LogiFlow для Argo CD.

```
bootstrap/root.yaml          кореневий Application, застосовується вручну один раз
argocd-apps/logiflow.yaml    Application застосунку (керується root)
charts/logiflow/             Helm-чарт з ЛР-4 і values-minikube.yaml
```

## Розгортання

```
kubectl create namespace logiflow-argo
kubectl -n logiflow-argo create secret generic logiflow-secret --from-literal=DB_PASSWORD=<...> --from-literal=SECRET_KEY=<...> --from-literal=S3_ACCESS_KEY=<...> --from-literal=S3_SECRET_KEY=<...>
kubectl apply -f bootstrap/root.yaml
```

Секрет створюється вручну й у Git не зберігається (параметр чарта `existingSecret`).
Оновлення: змінити тег образу в `charts/logiflow/values-minikube.yaml`, commit, push.
