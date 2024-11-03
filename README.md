# Docker Introdução

Facilita a execução de aplicações em ambientes de desenvolvimento e de produção, de forma isolada (camadas de isolamento)

## Rodar um container
`$ docker container run <imagem>`

## Roda com a imagem do ubuntu com o terminal (modo interativo)
`$ docker container run -it ubuntu /bin/bash`

## Roda com a imagem do nginx (em segundo plano -d) com a porta 8080(minha maq) redirecionada a 80(container nginx)
`$ docker container run -d -p 8080:80 nginx`

## Executa o terminal dentro do container em execução
`$ docker exec -i <CONTAINER ID> /bin/bash`

## Lista todos os containers, só IDs
`$ docker container ls -aq`

## Remove (a força) todos os containers criados (aplica o comando para cada um no subcomando)
`$ docker container rm -f $(docker container ls -aq)`

## Declarar uso de volume (pegar o arquivo ou pasta e mapeia no nginx)
`$ docker container run -d -p 8080:80 -v ./index.html:/usr/share/nginx/html/index.html nginx`

## Colocar a página direto na imagem (no seu file system)? Criar a imagem com o Dockerfile
- Dockerfile
```
FROM nginx
COPY ./index.html /usr/share/nginx/html/index.html
```
criar a imagem
`$ docker build -t docker-intro -f Dockerfile .`

## listar as imagens locais
`$ docker image ls`

## Rodar o container com a imagem criada
`$ docker container run -d -p 8080:80 docker-intro`

## Nomenclatura para subir no dockerhub
namespace/repositorio:tag

## Mudar o nome da imagem
`$ docker tag docker-intro betoxvt/live-aquecimento:v1`

## Conectar no dockerhub
`$ docker login`

## Subir no dockerhub
`$ docker push betoxvt/live-aquecimento:v1`

## Rodar o container com sua imagem no dockerhub
`$ docker container run -d -p 8080:80 betoxvt/live-aquecimento:v1`

## Criar de forma declarativa, em vez de interativa
Vai de docker compose:
- docker-compose.yml (versões antigas)
- compose.yaml (novas versões)
```
services:
  app:
    image: betoxvt/live-aquecimento:v1
    ports:
      - 8080:80
```
`$ docker compose up -d` inclusive recria o container com novas configs do compose.yaml
