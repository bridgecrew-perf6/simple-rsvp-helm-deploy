## Login via Argocd

SECRET=$(kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d)
argocd login argocd.10.38.12.146.nip.io --grpc-web --insecure --username admin --password $SECRET

## Create the Helm App

argocd app create ntnx-rsvp-app --repo https://github.com/jesse-gonzalez/simple-rsvp-app.git --path . --dest-namespace ntnx-rsvp-app --dest-server https://kubernetes.default.svc --values-literal-file configs/kalm-main/values.yaml --grpc-web

--insecure

> Sync (Deploy) The Application

argocd app get ntnx-rsvp-app --grpc-web

argocd app sync ntnx-rsvp-app --grpc-web