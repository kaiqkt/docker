<details><summary>Mais usados</summary>
<p>

Listar os container que estão sendo executados
```sh
docker ls
```
Exibir historico de execução de containers
```sh
docker ps -a
```
Remove imagens, containers e networks que não estão sendo utilizados
```sh
docker system prune
```
Copiar um arquivo para a maquina ou para o container
```sh
docker cp <container-id>:<dir>/<file-to-cp> <machine-dir>
docker cp <machine-dir> <container-id>:<dir>/<file-to-cp>
```
Informações sobre o container
```sh
docker top <container-id>
```
Verificar processos sendo executados pelo docker
```sh
docker stats
```

</p>
</details>
  
<details><summary>Container</summary>
<p>

Rodar um novo container com base em uma imagem
```sh
docker run <image-name>
```
Rodar um novo container de forma interativa
```sh
docker run -it <image-name>
```
Rodar um novo container em background sem ocupar uma aba do terminal
```sh
docker run -d <image-name>
```
Rodar um novo container exportando uma porta para conexão
```sh
docker run -p 80:80 <image-name>
```
Rodar um novo container inserindo variaveis de ambiente
```sh
docker run -e VAR_EXEMPLE=True <image-name>
```
Rodar um novo container definindo nome para o container
```sh
docker run --name container <image-name>
```
Rodar um novo container definindo que o mesmo sera removido após a execução
```sh
docker run --rm <image-name>
```
Parar um container que estiver sendo executado
```sh
docker stop <container-name>
```
Inicia o mesmo container já existente
```sh
docker start <container-name>
```
Verificar as ultimas ações de um container 
```sh
docker logs <container-id>
```
Remover um container da máquina
```sh
docker rm <container-id>
```
Remover um container da máquina mesmo se estiver sendo executado
```sh
docker rm -f <container-id>
```
  
</p>
</details>

<details><summary>Volume</summary>
<p>

Rodar um novo container definindo um volume anonimo
```sh
docker run -v <image-name>
```
Rodar um novo container definindo um volume nomeado, utilizando o mesmo dir que estiver na tag WORKDIR da Dockerfile
```sh
docker run -v <volume-name>:/<dir-name> <image-name>
```
Rodar um novo container definindo um volume nomeado da propria maquina que estiver executando, utilizando o mesmo dir que estiver na tag WORKDIR da Dockerfile
```sh
docker run -v "/$(pwd)<volume-name>":/<dir-name> <image-name>
Exemplo:
docker run -d -p 81:80 --name container-messages -v "/$(pwd)/volumes/messages":/var/www/html/messages --rm phpmessages
```
Listar todos os volumes
```sh
docker volume ls
```

 </p>
</details>
  
<details><summary>Imagem</summary>
<p>

Buildar uma imagem docker com base em uma Dockerfile
```sh
docker build <image-dir>
```
Listar as imagens
```sh
docker image ls
```
Nomear e inserir uma tag a uma imagem
```sh
docker tag <image-id> <image-name>:<image-tag>
```
Deletar imagem
```sh
docker rmi <image-id>
```
Deletar imagem mesmo que estiver sendo usada
```sh
docker rmi -f <image-id>
```
Subir imagem para o docker hub (repositorio deve ser criado previamente)
```sh
docker push <imagem-id>
```
  
</p>
</details>

<details><summary>Network</summary>
<p>

Listar as redes do nosso ambiente
```sh
docker network ls
```
Criar uma network com o driver de rede default: bridge
```sh
docker network create <network-name> 
```
Criar uma network com o driver de rede especifico
```sh
docker network create -d <driver-name> <network-name> 
```
Remover uma network
```sh
docker network rm <network-name>
```
Remover todas as redes que não estão sendo utilizadas
```sh
docker network prune
```
Roda container em uma rede(em uma conexão containerxcontainer não é necessario externalizar a porta)
```sh
docker run --network <network-name> <image-nae>
```
Insere o container em uma rede
```sh
docker network connect <network-name> <container-name>
```
Remove o container de uma rede
```sh
docker network disconnect <network-name> <container-name>
```
Lista detalhes de uma rede
```sh
docker network inspect <network-name>
```
  
</p>
</details>

<details><summary>Kubernetes</summary>
<p>

O que é kubernetes?

Uma ferramenta de orquestração de containers;
Permite a criação de múltiplos containers em diferentes máquinas (nodes);
Escalando projetos, formando um cluster;
Gerencia serviços, garantindo que as aplicações sejam executadas sempre da mesma forma;

Conceitos fundamentais?

Control Plane: Onde é gerenciado o controle dos processos dos Nodes.
Nodes: Máquinas que são gerenciadas pelo Control Plane.
Deployment: A execução de uma imagem/projeto em um Pod
Pod: um ou mais containers que estão em um Node.
Services: Serviços que expõe os Pods ao mundo externo.
kubectl: Cliente de linha de comando para o Kubernetes.

<details><summary>Minikube</summary>
<p>

O Kubernetes pode ser executado de uma maneira simples em nossa máquina.
Vamos precisar do client, kubectl, que é a maneira de executar o Kubernetes.
E também o Minikube, uma espécie de simulador de Kubernetes, para não precisarmos de vários computadores/servidores.

Para inicializar o Minikube vamos utilizar o comando:
```sh
minikube start --driver=<DRIVER>
```
Você pode tentar usar os drivers: virtualbox, hyperv e docker

O Minikube nos disponibiliza uma dashboard para ver  o detalhamento de nosso projeto: serviços, pods e etc:
```sh
minikube dashboard
```

Para obter a url da dashboard: 
```sh
minibuke dashboard --url
```

</p>
</details>

<details><summary>Kubernetes Cli</summary>
<p>

Podemos também verificar como o Kubernetes está configurado:
```sh
kubectl config view
```

O Deployment é uma parte fundamental do Kubernetes;
Com ele criamos nosso serviço que vai rodar nos Pods;
Definimos uma imagem e um nome, para posteriormente ser replicado entre os servidores;
A partir da criação do deployment teremos containers rodando;
Vamos precisar de uma imagem no Hub do Docker, para gerar um Deployment;


Para isso vamos precisar de um Deployment, que é onde rodamos os containers das aplicações nos Pods: 
```sh
kubectl create deployment <NOME> --image=<IMAGEM>
```
Para verificar o Deployment vamos utilizar: kubectl get deployments
E para receber mais detalhes deles:
```sh
kubectl describe deployments
```
Para verificar os Pods utilizamos:
```sh
kubectl get pods
```
E para saber mais detalhes deles: 
```sh
kubectl describe pods
```

As aplicações do Kubernetes não tem conexão com o mundo externo;
Por isso precisamos criar um Service, que é o que possibilita expor os Pods;
Isso acontece pois os Pods são criados para serem destruídos e perderem tudo, ou seja, os dados gerados neles também são apagados;
Então o Service é uma entidade separada dos Pods, que expõe eles a uma rede;

Para criar um serviço e expor nossos Pods devemos utilizar o comando:
```sh
kubectl expose deployment <NOME> --type=<TIPO> --port=<PORT>
```
O tipo de Service, há vários para utilizarmos, porém o LoadBalancer é o mais comum, onde todos os Pods são expostos;
E uma porta para o serviço ser consumido;

Podemos acessar o nosso serviço com o comando: 
```sh
minikube service <NOME>
```
Podemos também obter detalhes dos Services já criados;
O comando para verificar todos é:
```sh
kubectl get services
```
E podemos obter informações de um serviço em específico com:
```sh
kubectl describe services/<NOME>
```
Vamos aprender agora a como utilizar outros Pods, replicando assim a nossa aplicação,o comando é: 
```sh
kubectl scale deployment/<NOME> --replicas=<NUMERO>
```
Além do get pods e da Dashboard, temos mais um comando para checar réplicas, que é o: 
```sh
kubectl get rs
```
Podemos facilmente também reduzir o número de Pods;
Esta técnica é chamada de scale down;
O comando é o mesmo, porém colocamos menos réplicas e o Kubernetes faz o resto:
```sh
kubectl scale deployment/<NOME> --replicas=<NUMERO_MENOR>
```
Podemos sempre relembrar o IP/URL do nosso serviço;
O comando é:
```sh
minikube service --url <NOME>
```
Para atualizar a imagem vamos precisar do nome do container, isso é dado na Dashboard dentro do Pod;
E também a nova imagem deve ser uma outra versão da atual, precisamos subir uma nova tag no Hub:
```sh
kubectl set image deployment/<NOME> <NOME_IMAGEM_SEM_TAG>=<NOVA_IMAGEM>
```
Para desfazer uma alteração utilizamos uma ação conhecida como rollback;
O comando para verificar uma alteração é:
```sh
kubectl rollout status deployment/<NOME>
```
Com ele e com o kubectl get pods, podemos identificar problemas;
Para voltar a alteração utilizamos: 
```sh
kubectl rollout undo deployment/<NOME>
```
Para deletar um serviço do Kubernetes vamos utilizar o comando: 
```sh
kubectl delete service <NOME>
```
Para deletar um Deployment do Kubernetes vamos utilizar o comando: 
```sh
kubectl delete deploymnet <NOME>
```

**Modo Declarativo**

Tags do .yml

apiVersion: versão utilizada da ferramenta;
kind: tipo do arquivo (Deployment, Service);
metadata: descrever algum objeto, inserindo chaves como name;
replicas: número de réplicas de Nodes/Pods;
containers: definir as especificações de containers como: nome e imagem;
para separar objetos no yml utilizamos: ---

Vamos então executar nosso arquivo de Deployment!
O comando é: 
```sh
kubectl apply -f <ARQUIVO>
```
Para parar de executar este deployment baseado em arquivo, o declarativo, utilizamos também o delete:
```sh
kubectl delete -f <ARQUIVO>
```


</p>
</details>


</p>
</details>

## License

MIT

**Free Software, Hell Yeah!**
