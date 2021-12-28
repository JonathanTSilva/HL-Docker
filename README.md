<!-- Simple logo -->
<a href="#meu-guia-de-docker"><img width="400px" src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/4e/Docker_%28container_engine%29_logo.svg/2560px-Docker_%28container_engine%29_logo.svg.png" align="right" /></a>

# Meu guia de Docker

🛠 Passo a passo que adoto na minha utilização de Docker

- [Meu guia de Docker](#meu-guia-de-docker)
  - [1. Instalação](#1-instalação)
    - [1.1. Windows](#11-windows)
    - [1.2. MAC](#12-mac)
    - [1.3. Linux](#13-linux)
  - [2. Comandos Básicos](#2-comandos-básicos)
  - [3. Imagem vs Container](#3-imagem-vs-container)
  - [3. Docker File](#3-docker-file)
  - [4. Comandos Intermediários e Avançados](#4-comandos-intermediários-e-avançados)
    - [4.1. Imagem](#41-imagem)
      - [4.1.1. Resumo](#411-resumo)
    - [4.2. Container](#42-container)
    - [🢚 O que acontece no "docker container run"](#-o-que-acontece-no-docker-container-run)
    - [✍ Exercício de fixação: Gerenciando vários containers](#-exercício-de-fixação-gerenciando-vários-containers)
      - [4.2.1. Resumo](#421-resumo)

## 1. Instalação

Docker é uma plataforma aberta para desenvolvimento, envio e execução de aplicativos. O Docker permite que você separe seus aplicativos de sua infraestrutura para que possa entregar o software rapidamente. Com o ele, você pode gerenciar sua infraestrutura da mesma forma que gerencia seus aplicativos. Tirando proveito das metodologias do Docker para enviar, testar e implantar código rapidamente, pode-se reduzir significativamente o atraso entre escrever o código e executá-lo na produção.

É possível baixar e instalar o Docker em várias plataformas. As subseções a seguir guiarão na instalação do docker para os três eco-sistemas: Windows, MAC e Linux.

### 1.1. Windows

### 1.2. MAC

### 1.3. Linux

Todo o processo de instalação apresentado neste item, pode ser conferido diretamente pelo site do Docker: [Install Docker Engine][2]. Para demais informações, verifique o site.

**Pré-Requisitos:** </br>
Antes de iniciar a instalação, certifique-se de ter permissão de super usuário, será necessário adicionar o repositório do Docker em seu sistema operacional para realizar o download do pacote. Para isso, execute a sequência de comandos a seguir:

1. Atualizando da lista de pacotes do repositório atual:

```cmd
$ sudo apt-get update
```

2. Instalando pacotes para permitir o apt utilizar repositórios sobre HTTPS:

```console
$ sudo apt-get install \
apt-transport-https \
ca-certificates \
curl \
gnupg \
lsb-release
```

3. Instalando a chave criptográfica do repositório (GPG key):

```console
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

4. Adicionando o repositório do Docker à lista de repositórios do sistema operacional:

```console
$ echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

**Instalação:** </br>

1. Atualizando da lista de pacotes do repositório atual:

```console
$ sudo apt-get update
```

2. Instalando a última versão do Docker e seus componentes:

```console
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
```

## 2. Comandos Básicos

Ao instalar o Docker, automaticamente fazemos a instalação do seu CLI, que disponibiliza o comando docker em nosso terminal.

Desta forma, abra um terminal e digite o seguinte comando para ver a versão do Docker instalada.

```docker
docker version
```

O comando acima comunica com o servidor Docker Engine instalado em sua máquina e retorna as informações de versão. Caso queira mais informações sobre o sistema, aplicar:

```docker
docker info
```

Este, retornará muitos outros detalhes sobre configuração setados para a máquina, status, entre outros.

Caso tenha dúvida sobre algum comando do docker, basta digitar `docker` no terminal e serão retornadas as todas as opções, comandos e comandos de gerenciamento. Da mesma forma, se não souber o que um comando faz, basta digitá-lo e acrescentar a opção `--help`:

```docker
docker <commando> --help
```

Vale ressaltar que há duas estruturas adotadas para os *Management Commands*. Apesar de a forma antiga ainda ser utilizada (docker <comando> <sub-comando> (options)), tem-se a nova variação:

```docker
docker <commando> <sub-comando> (options)
```

## 3. Imagem vs Container

Para esclarecer melhor quais são as diferenças entre imagens e contêineres, tente pensar em uma linguagem orientada a objetos. Nessa analogia, a classe representa a imagem enquanto sua instância, o objeto, é o contêiner. A mesma imagem pode criar mais contêineres. Portanto, a virtualização de contêiner é fundamentalmente baseada em imagens, nos arquivos disponíveis no Docker Hub e usados ​​para criar e inicializar um aplicativo em um novo contêiner do Docker.

Cada imagem é definida por um **Dockerfile**, um arquivo de configuração que contém todos os comandos que um usuário precisa executar para modelar a imagem. As imagens e contêineres do Docker trabalham juntos para permitir que você liberte todo o potencial da tecnologia inovadora do Docker. No entanto, eles têm diferenças sutis que podem ser difíceis de perceber, especialmente para um iniciante.

A tabela abaixo aponta as principais diferenças entre eles:

| Imagem do Docker                                                                 | Contêiner do Docker                                                            |
| -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| é um projeto de contêiner                                                        | é uma instância de uma imagem                                                  |
| é imutável                                                                       | é alterável                                                                    |
| não precisa de recursos de computação para operar                                | um contêiner deve executar uma imagem para existir                             |
| pode ser compartilhado por meio de uma plataforma de registro público ou privado | precisa de recursos computacionais para rodar - rodam como uma máquina virtual |
| crie apenas uma vez                                                              | múltiplos contêineres podem ser criados de uma mesma imagem                    |

Uma outra analogia simples para melhor compreensão é pensar em uma imagem do Docker como uma receita e um contêiner como o bolo preparado a partir dessa receita. A receita apresenta as instruções para assar o bolo. Você não pode gostar de comer o bolo se não colocar as instruções em ação. É preciso seguir a receita para preparar o bolo e comê-lo. Da mesma forma, você deve seguir as instruções na imagem do Docker para criar e iniciar um contêiner e aproveitar os benefícios do Docker. Você pode assar tantos bolos quanto possível com uma única receita - assim como uma imagem pode criar vários contêineres. No entanto, se você alterar a receita, o sabor dos bolos existentes não mudará. Apenas bolos recém-assados usarão a receita modificada. Da mesma forma, se você fizer alterações em uma imagem de contêiner, não afetará os contêineres já em execução.

## 3. Docker File

## 4. Comandos Intermediários e Avançados

### 4.1. Imagem

#### 4.1.1. Resumo

| Ação    | Comando                                         | Descrição                                                                                                                                                          |
| ------- | ----------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Iniciar | `docker run [OPTIONS] IMAGE [COMMAND] [ARG...]` | Primeiro cria suma camada de contêiner gravável sobre a imagem especificada (`docker create`) e, em seguida inicia (`docker start`), usando o comando especificado |
| Parar   |                                                 |                                                                                                                                                                    |
| Listar  |                                                 |                                                                                                                                                                    |
| Deletar |                                                 |                                                                                                                                                                    |

### 4.2. Container

Para iniciar um container, utilize o exemplo a seguir:

```docker
docker container run --publish 80:80 nginx
```

Primeiramente, o comando acima baixa a imagem 'nginx' do Docker Hub (Docker Store), para então começar um novo container dessa imagem. Assim, a porta 80 é aberta no IP host da máquina e o tráfego é roteado para o IP do container, porta 80.

> Note you'll get a "bind" error if the left number (host port) is being used by anything else, even another container. You can use any port you want on the left, like 8080:80 or 8888:80, then use localhost:8888 when testing.

Ao adicionar a opção `--detach` no código acima, uma execução em segundo plano é realizada.

Para enviar um sinal de parada ao processo docker quando estiver rodando em primeiro plano, utilize:

```docker
Ctrl + C
```

Entretanto, isso ocorre bem no sistema Mac e Linux. No Windows, o sistema é fechado do primeiro plano, mas ainda continua rodando em segundo. Assim, caso esteja no Windows, antes de utilizar o comando acima, é preciso dar:

```docker
docker stop <container id/name>
```

Para listar todos os containers **rodando** na máquina à nova maneira, substituindo `docker ps`:

```docker
docker container ls
```

Entretanto, note que caso apenas os containers que estão em operação `running` são listados. Para listar todos, acrescentar a opção `-a` ao código acima.

Note que o `docker container run` sempre inicia um **novo** container. Para iniciar estes containers listados e que estão parados, utilizar:

```docker
docker container start
```

Outro ponto importante notado neste estágio do estudo, é que os nomes dos containers são criados de forma randômica, caso não enviado nenhum comando, variando entre nomes de uma lista *open source* de adjetivos e sobrenomes de hackers e cientistas famosos. Para alterar um nome do container em sua criação, adicionar a opção `--name` no comando `docker run`

```docker
docker container run --publish 80:80 --detach --name <container name> nginx
```

O uso de um container é armazenado em logs, que caso esteja rodando em primeiro plano no console, aparecerão de forma automática. Entretanto, estes logs podem ser obtidos com o comando:

```docker
docker container logs <container id/name>
```

Com o comando `top`, é possível visualizar os processos em execução de um contêiner específico:

```docker
docker container top <container name>
```

Além disso, é possível visualizar todos os processos rodando no host, basta utilizar:

```console
ps aux
```

Há a opção de utilizá-lo com `ps aux | grep <keyword>` para filtrar a palavra desejada por todos os processos que estão rodando.

Para remover algum container, ou até mesmo todos de uma vez só (em alguns casos, subcomandos do Docker podem levar múltiplos valores) utilize, respectivamente:

```docker
docker container rm <container id1/name1> <container id2/name2> <container idN/nameN>
```

Um erro frequente para o processo acima é tentar excluir um container enquanto estiver rodando. Para realizar tal ação basta parar o container ou utilizar o comando `-f` para forçar a remoção.

#### 🢚 O que acontece no "docker container run"

Ao dar o comando `docker container run`, no plano secundário está  acontecendo os seguintes processos:

1. A imagem é procurada localmente no cache de imagens, mas nada é encontrado;
2. Então, a imagem é procurada remotamente no repositório default (Docker Hub);
3. Ao encontrar, a última versão da imagem é baixada (e.g. nginx:latest);
4. Cria um novo container baseado na imagem e prepara para a inicialização;
5. Dá para ele um IP virtual na rede privada dentro do docker engine;
6. Abre a porta 80 no host e aponta para a porta 80 do container;
7. Inicia o container usando o CMD no Dockerfile da imagem.

**Exemplo de mudança de padrão:**

```docker
docker container run --publish 8080:80 --name webhost -d nginx:1.11 nginx -T
```

A parte `8080:80`é responsável pela mudança da  porta "ouvida" pelo host. `nginx:1.11` altera a versão requerida do nginx e o comando posterior a esse, muda o CMD run no "start"

#### ✍ Exercício de fixação: Gerenciando vários containers

Antes de qualquer outra dúvida, vale ressaltar que os principais meios para resolver problemas e tirar dúvidas são o site de [documentação do docker][3] e o comando `--help`.

Assim, supondo uma utilização de 3 containers rodando simultaneamente: nginx, mysql e httpd (apache server):

1. Rodar todos eles com o `--detach` (ou `-d`) e nomear com o `--name`, para maior controle;
2. Alterar as portas, por exemplo: nginx para escutar 80:80, httpd na 8080:80 e o mysql na 3306:3306;
3. Quando rodar o mysql, usar a opção `--env` (ou `-e`) para passar em MYSQL_RANDOM_ROOT_PASSWORD=YES;
4. Usar o `docker container logs` no mysql para encontrar a senha randômica criada na inicialização.
5. Limpar tudo com o `docker container stop` e `docker container rm` (ambos os comandos permitem múltiplos nomes ou IDs);
6. Usar o `docker container ls` para se assegurar que tudo está correto após a exclusão (ou `ls -a`).

**⋙ Resposta**

```docker
docker container run -d -p 3306:3306 --name db -e MYSQL_RANDOM_ROOT_PASSWORD=yes mysql

docker container logs db

<encontrar a senha gerada randomicamente> e copiar

docker container run -d --name webserver -p 8080:80 httpd

docker container run -d --name proxy -p 80:80 nginx

docker container ls (para ver se os containers criados já estão rodando)

curl localhost (testar a resposta do nginx)
curl localhost:8080 (testar resposta do apache)

docker container stop webserver proxy db

docker container ls -a (para ver se os containers pararam)

docker container rm webserver proxy db
```

#### 4.2.1. Resumo

| Comando                  | Descrição                                        |
| ------------------------ | ------------------------------------------------ |
| docker container run     |                                                  |
| docker container stop    |                                                  |
| docker container ls      |                                                  |
| docker container rm      |                                                  |
| docker container top     | lista os processos de um container               |
| docker container inspect | detalha a configuração de um container           |
| docker container stats   | apresenta as estatísticas de todos os containers |

```docker
docker run <imagem>
docker run ubuntu echo "Hello World"
docker run -it ubuntu
```

```docker
docker ps
docker ps -a
```

```docker
docker start <container id>
docker start -a -i <container id>
```

```docker
docker stop <container id>
```

<!-- Markdown's Links -->
<!-- SITES -->
[1]: https://landscape.cncf.io/?zoom=200
[2]: https://docs.docker.com/engine/install/
[3]: https://docs.docker.com

<!-- ARQUIVOS -->

<!-- IMAGENS -->

<!-- COMENTÁRIOS -->
