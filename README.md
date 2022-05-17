# takehome_devops

Repositorio para aplicacao feed com autenticacao no servico auth.

Serviços ja virtualizados. Para checar os containers, baixe o repositorio, execute o comando de docker build 
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


