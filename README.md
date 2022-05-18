# takehome_devops

Repositorio para aplicacao feed com autenticacao no servico auth.

Necessario instalar o docker, minikube e kubectl para executar a aplicacao;

Instalacao docker;
https://docs.docker.com/engine/install/

instalacao minikube;
https://minikube.sigs.k8s.io/docs/start/

instalacao kubectl;
https://minikube.sigs.k8s.io/docs/handbook/kubectl/


As aplicaçoes ja virtualizados. Para checar os containers, baixe o repositorio, execute o comando de docker build 
na pasta de cada aplicacao. como no exemplo abaixo;

cd services/feed;
docker build -t feed:1.0 .

cd services/auth
docker build -t auth:1.0 .

Para o kubernetes baixar as imagens, será preciso tagear as imagens e colocar dentro do docker hub de sua preferencia;
exemplo abaixo;

docker build -t <DOCKER_LOGIN>/feed:1.0 .
Será requisitado seu usuario e senha do docker hub para a finalização do comando. 


Para iniciar um cluster no minikube execute o seguinte comando;

minikube start --vm=true --cpus 4 --memory 4098

Para verificar de modo grafico suas aplicacoes, execute;

minikube dashboard

Após habilitar o minikube, verifique se os pods responsaveis pelo funcionamento do k8s, estao no ar;

kubectl get pods -A

Para executar a aplicacao, entre na pasta do kubernetes e execute o comando de criacao dos objetos;

cd /services/k8s/
kubectl create -f .

Verifique se os elementos estao no ar;

kubectl get pods,svc,deploy;

O resultado será algo como abaixo;

NAME                                   READY   STATUS    RESTARTS      AGE
pod/auth-deployment-5854d6b87c-d287r   1/1     Running   2 (17h ago)   38h
pod/feed-deployment-6c9cbcf86c-d4jxs   1/1     Running   3 (17h ago)   18h

NAME                   TYPE           CLUSTER-IP      EXTERNAL-IP     PORT(S)        AGE
service/feed-service   LoadBalancer   10.99.103.253   10.99.103.253   80:30937/TCP   91s
service/kubernetes     ClusterIP      10.96.0.1       <none>          443/TCP        38h

NAME                              READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/auth-deployment   1/1     1            1           38h
deployment.apps/feed-deployment   1/1     1            1           18h 


Note que o service foi criado como loadbalance. Para ativar o load balance do minikube, execute;

minikube tunnel;

Agora realize os testes com o comando curl, exemplo abaixo;

curl -H "Authorization: Bearer 66ec51ac-72ea-479d-8b5f-d99eede929f0" -v 10.99.103.253/feed/premium

curl -H "Authorization: Bearer 66ec51ac-72ea-479d-8b5f-d99eede929f0" -v 10.99.103.253/feed/patriota


