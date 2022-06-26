## Comandos para usar no docker

## Comandos

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

## License

MIT

**Free Software, Hell Yeah!**
