** Trocar tab por espaços no VIM
  - Criar arquivo ~/.vimrc e incluir o conteudo abaixo
  set expandtab
  set tabstop=2
  set softtabstop=2
  set shiftwidth=2

** Criar pod através de arquivo YML
kubectl create -f arquivo.yml

** Obter detalhes do Pod
kubectl get pod

** Obter mais detalhes do Pod
kubectl get pod -o wide

** Obter descrição do Pod
kubectl describe pod pod-name

** Entrar no bash do pod
kubectl exec -ti pod-name sh

** Shell para testar load balance
for X in $(seq 1 100); do minikube ssh curl 10.106.178.226:8080; sleep 1; done

** Scaffold para criar arquivo de deployment
kubectl create deploy cgi --image hectorvido/sh-cgi --dry-run -o yaml > cgi.yml

** Scaffold para criar arquivo de deployment
kubectl expose deploy cgi
- cgi é o nome do deploy criado anteriormente

** Atualizar imagem sem downtime gravando as alterações
kubectl patch deploy cgi --patch '{"spec" : {"template" : {"spec" : {"containers": [{"name": "sh-cgi", "image" : "hectorvido/sh-cgi:v3"}]}}}}' --record

** Ver o rollout das alterações do arquivo yml de deploy
kubectl rollout history deploy cgi

** Remover serviços e deploy pela label
kubectl delete all -l app=<label deploy|serviço>

** Criar arquivo .conf do redis
echo -n '<senha>' | sha256sum > redis.conf

** Reiniciar container sem delete
kubectl scale deploy redis --replicas=0
kubectl scale deploy redis --replicas=1

** Criar arquivo yml a partir do deploy
kubectl get deploy <deploy-name> -o yaml > <file-name>.yml

** Criar certificado x509 para criar usuários no kubernetes
openssl req -x509 -nodes -keyout key.pem -out cert.pem

** Ver dados do certificado criado
openssl x509 -in cert.pem -noout -text

** Criar secret 
kubectl create secret tls perl --key key.pem --cert cert.pem

