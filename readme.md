# Docker
Curso realizado na plataforma Alura. Link do curso [aqui](https://cursos.alura.com.br/course/docker-criando-gerenciando-containers).

## Conhecendo Docker

**Máquinas virtuais** são capazes de isolar sistemas, com isso, o controle sobre a aplicação fica mais fácil. Máquinas virtuais possuem camadas adicionais de virtualização em relação a um container;

**Containers** podem isolar diversas aplicações, facilitando o controle acerca de portas e versões.
* Containers funcionam como processos no host;
* Containers atingem isolamento através de namespaces;
* Os recursos dos containers são gerenciados através de cgroups.

Os containers *são mais leves* do que máquinas virtuais.

**Vantagens do Docker:** isolamento de contextos e versionamento de aplicações.

## Instalando o docker no Windows

Acessar o site da [Docker](https://docs.docker.com/get-docker/) e realizar o download para Windows.

## Docker Hub
O Docker Hub é um grande repositório de imagens que podemos utilizar;

A base dos containers são as imagens;

## Os primeiros comandos
### Comando docker run
O comando docker run é responsavel por executar um container em nosso host.
```
docker run hello-world
```
![](/imagem/docker-run.png)

* Procura a imagem localmente -> Informa que nao foi possivel encontrar na maquina local.
* Baixa a imagem caso não encontre localmente -> Realiza o download da imagem. Existe um grande repositorio de imagens (Docker Hub). hello-world é uma imagem.
* Valida o hash da imagem 
* Executa o container -> Executa a imagem/container.

Comandos:

Há o comando sleep> docker run ubunto sleep 1d

### Comando docker ps

```
docker ps
```
Informa quais os container estao em executação nesse momento.
Se informar so o cabeçalho, indica que a lista esta vazia. 

### Comando docker container ls
```
docker container ls
```
Semelhante ao comando docker ps, porem mais verboso.

### Comando docker container ls -a ou docker ps -a
```
docker container ls -a
#ou
docker ps -a
```

Informa as imagens que foram executadas e/ou estao em execução.

### Comando docker stop
Visualiza os container através de docker ps. Para parar uma imagem basta informar o id do container ou o names.
```
docker stop [container id ou names]
```
Visualizar os containers parados atraves do comando docker ps -a

é possivel passar um tempo.
```
docker stop -t=0 [container id ou names]
```

### Comando docker rm [container id ou names]
Remove o container

### Comando exec -it [container id] bash
Permite executar container em modo interativo.
Um comando bastante utilizado é:

```
docker run -it ubuntu bash
```
Criamos um container novo e ja estamos diretamente no terminal dele. 

## Docker run vs Docker exec
O **docker run** cria um novo container e o executa. O **docker exec** permite executar um comando em um container que já está em execução.

## Mapeando portas
-d nao trava o terminal
-P executa container e exibe a porta
```
- docker run -d -P dockersample/static-site
- docker ps
- docker port [id] (informa para onde foi mapeada)
- docker run -d -p 8080:80 dockersample/static-site
```

Este comando é responsável por exibir como o mapeamento de portas de um container está sendo feito.
```
docker port
```
## Comandos de Ciclo de vida dos containers
* **docker start**, para iniciar um container que esteja parado; 
* **docker stop**, para parar um que esteja rodando; 
* **docker pause**, para pausar um container ;
* **docker unpause** para iniciar um container pausado; 
* Conseguimos **mapear portas** de um container com as flags -p e -P.

## Criando e compreendendo imagens
### O que são imagens?
**Conjunto de camadas** que unidas formam imagens. Cada camada possui um identificador, isto é, são independentes. Logo, imagens são compostas por uma ou mais camadas. (As camadas são a menor unidade que compõem uma imagem.)

Consideradas **receitas** para gerar containers

Visualizar imagens baixadas:
```
docker images
```
Visualiza/inspeciona uma imagem:
```
docker inspect [ID]
```
Visualiza o historico:
```
docker history [ID]
```

### Criando imagem
Cria-se o arquivo Dockerfile.
Dentro deste arquivo, informamos o que iremos de base.
Ex: preciso do node, portanto
```
FROM node:14
WORKDIR /app-node
COPY . .
RUN npm install
ENTRYPOINT npm start
```
Após, cria-se, via terminal, a imagem:
```
docker build -t annekaroline/app-node:1.0 .
```

* A instrução **FROM** é usada para definirmos uma imagem como base para a nossa.
* A **instrução ARG** carrega variáveis apenas no momento de build da imagem
* A **instrução ENV** carrega variáveis que serão utilizadas no container.

![](/imagem/imagem-criando-docker.png)

Rodando docker criado:
![](/imagem/rodar-docker-criado.png)

## Subir imagem para o Docker Hub
1. Cadastrar e acessa o Docker Hub
## Persistindo dados
## Comunicação através de redes
## Coordenando Containers 