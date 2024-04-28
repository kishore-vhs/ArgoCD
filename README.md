# ArgoCD

github webhook: https://<loadbalancer>/api/webook

kubectl create secret tls wc-tls --cert=tls.crt --key=tls.key -n default
kubectl create secret tls wc-tls --cert=tls.crt --key=tls.key -n ingress-nginx

argocd app create test-deploy --path deploy \
--repo https://github.com/kishore-vhs/ArgoCD.git \
--dest-server https://api.hskglobaltech.shop \
--dest-namespace default

argocd app create voting-deploy --path voting_app \
--repo https://github.com/kishore-vhs/ArgoCD.git \
--dest-server https://api.hskglobaltech.shop \
--dest-namespace default

argocd app set test-deploy --sync-policy automated --auto-prune --allow-empty --self-heal
argocd app set voting --sync-policy automated --auto-prune --allow-empty --self-heal


 argocd login $ARGOCD_SERVER --username admin --password iU2VGW6yzCGWrNDU --insecure