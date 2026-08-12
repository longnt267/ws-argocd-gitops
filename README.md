# ws-argocd-gitops

Repo GitOps cho ArgoCD — chỉ chứa Helm chart + Application manifest, tách riêng khỏi repo source code (`ws-argocd-app`).

## Apply vào ArgoCD (local)

Sau khi đã push repo này lên GitHub:

```bash
kubectl apply -f argocd/application-dev.yaml
kubectl apply -f argocd/application-stage.yaml
```

ArgoCD sẽ tự tạo namespace `nestjs-dev` / `nestjs-stage`, sync chart, và tự động sync lại mỗi khi có commit mới (do `syncPolicy.automated`).

## Cách image được cập nhật

`image.repository`/`tag` trong `values-dev.yaml` / `values-stage.yaml` được CI ở repo `ws-argocd-app` cập nhật tự động (build → push image lên `ghcr.io/longnt267/nestjs-demo` → commit sửa tag vào repo này). Có thể sửa tay để test trước khi setup CI.
