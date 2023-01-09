<!-- Simple logo -->
<a href="#meu-guia-de-docker"><img width="400px" src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/4e/Docker_%28container_engine%29_logo.svg/2560px-Docker_%28container_engine%29_logo.svg.png" align="right" /></a>

# Meu guia de Docker

🛠 Passo a passo que adoto na minha utilização de Docker

- [Meu guia de Docker](#meu-guia-de-docker)
  - [1. Instalação](#1-instalação)
    - [1.1. Windows e MAC](#11-windows-e-mac)
    - [1.2. Linux](#12-linux)
  - [2. Comandos Básicos](#2-comandos-básicos)
  - [3. Imagem vs Container](#3-imagem-vs-container)
  - [3. Docker File](#3-docker-file)
  - [4. Comandos Intermediários e Avançados](#4-comandos-intermediários-e-avançados)
    - [4.1. Imagem](#41-imagem)
      - [4.1.1. Resumo](#411-resumo)
    - [4.2. Container](#42-container)
      - [🢚 O que acontece no "docker container run"](#-o-que-acontece-no-docker-container-run)
      - [✍ Exercício de fixação: Gerenciando vários containers](#-exercício-de-fixação-gerenciando-vários-containers)
      - [🢚 Abrir um *shell* dentro de um container](#-abrir-um-shell-dentro-de-um-container)
      - [🢚 Redes no Docker](#-redes-no-docker)
      - [4.2.1. Resumo](#421-resumo)
  - [5. FAQ](#5-faq)
    - [Imagens](#imagens)
    - [Containers](#containers)
    - [Dockerfile](#dockerfile)
    - [Docker Hub](#docker-hub)
    - [Docker Registry](#docker-registry)
    - [Docker Swarm](#docker-swarm)
    - [Docker Compose](#docker-compose)

## 1. Instalação

Docker é uma plataforma aberta para desenvolvimento, envio e execução de aplicativos. O Docker permite que você separe seus aplicativos de sua infraestrutura para que possa entregar o software rapidamente. Com o ele, você pode gerenciar sua infraestrutura da mesma forma que gerencia seus aplicativos. Tirando proveito das metodologias do Docker para enviar, testar e implantar código rapidamente, pode-se reduzir significativamente o atraso entre escrever o código e executá-lo na produção.

É possível baixar e instalar o Docker em várias plataformas. As subseções a seguir guiarão na instalação do docker para os três eco-sistemas: Windows, MAC e Linux.

### 1.1. Windows e MAC

Atualmente, o Docker é divido em dois produtos, Community Edition (CE) e Enterprise Edition (EE). Como os nomes sugerem, o Community é gratuito e voltado a comunidade, enquanto o Enterprise é recomendado para uso empresarial. Tudo que é necessário para trabalhar com Docker é fornecido pela versão Community que é gratuita.

O Docker possui uma versão para Desktop que irá facilitar nossa vida. Se você gosta de linha de comando, também fará a instalação do CLI. Vamos então acessar a página de início do Docker e clicar em **Download Desktop and Take a Tutorial**. Isto vai levar a página de **Downloads**. Selecione a versão que atende seu sistema operacional, como **Docker for Windows ou Docker for Mac** e na tela seguinte selecione **Get Docker**. Siga a instalação dos pacotes para realizar todo o processo. Recomendamos que ao término do mesmo reinicie seu computador.

**WINDOWS ONLY**
Durante a instalação do Docker para Windows, você será questionado sobre utilizar containers Windows ao invés de Linux. Fique à vontade em testar esta opção, mas para utilização do Docker em nossos cursos, recomendamos que NÃO DEIXE-A MARCADA. **Sempre vamos utilizar containers Linux** como padrão.

### 1.2. Linux

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

Para esclarecer melhor quais são as diferenças entre imagens e contêineres, tente pensar em uma linguagem orientada a objetos. Nessa analogia, a classe representa a imagem enquanto sua instância, o objeto, é o contêiner. A mesma imagem pode criar mais contêineres. Portanto, a virtualização de contêiner é fundamentalmente baseada em imagens, nos arquivos disponíveis no Docker Hub e usados para criar e inicializar um aplicativo em um novo contêiner do Docker.

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

| Ação      | Comando                                         | Descrição                                                                                                                                                          |
| --------- | ----------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Iniciar   | `docker run [OPTIONS] IMAGE [COMMAND] [ARG...]` | Primeiro cria suma camada de contêiner gravável sobre a imagem especificada (`docker create`) e, em seguida inicia (`docker start`), usando o comando especificado |
| Parar     |                                                 |                                                                                                                                                                    |
| Listar    |                                                 |                                                                                                                                                                    |
| Deletar   |                                                 |                                                                                                                                                                    |
| Pausar    |                                                 |                                                                                                                                                                    |
| Despausar |                                                 |                                                                                                                                                                    |

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

#### 🢚 Abrir um *shell* dentro de um container

O *Shell* pode ser definido como sendo um intérprete de comandos com uma interface entre o usuário e o sistema operacional. Existem vários tipos de *shell*, sendo os mais comuns o sh (chamado *Bourne shell*), o bash (Bourne again shell), o csh (C Shell), o Tcsh (Tenex C shell), o ksh (Korn shell) e o zsh (Zero shell).

Durante a execução de um comando no shell, é criado um processo que abrirá três fluxos:

* stdin  - entrada padrão - o stdin se refere ao teclado e é identificado pelo número 0;
* stdout - saída padrão - o stdout se refere à tela e é identificado pelo número 1;
* stderr - erro padrão - o stderr se refere à tela e é identificado pelo número 2:

Sem mais delongas, para obtermos um shell dentro de um container,  pode ser realizado um dos seguintes passos:

1. `docker container run -it` - para iniciar um novo container de forma interativa;
2. `docker container exec -it` - para rodar um comando adicional em container já existente;

A opção `-it` que acompanha os comandos acima, significa a junção de dois comandos: o `-t` - pseudo-tty (que simula um terminal real, como é feito no SSH) e `-i` - interactive (que mantem a sessão aberta para receber entradas do terminal (stdin)). Caso você rode este comando, deve ser passado a opção de qual terminal será aberto com o container. Como exemplo, usaremos o **bash**.

```docker
docker container run -it --name proxy nginx bash
```

Ao entrar no shell do container, todos os comandos normais que seriam dados à alguma máquina podem ser testados, como o `ls -al`. Para sair, basta dar `exit` na linha de comando.

Para o caso de já possuir um container, a opção (2) abrirá um novo processo dentro deste container que já está rodando.

```docker
docker container exec -it mysql bash
```

Mas lembre, só é possível rodar comandos (como o **bash**) em containers que já possuem aquela aplicação instalada. Caso seja feito um `pull` do Alpine e tentar rodar ele com a opção `-it alpine bash`, uma mensagem de erro aparecerá, pois o **bash** não está presente na imagem do Alpine, mas sim o **sh**.

#### 🢚 Redes no Docker

* Cada container conecta em uma rede virtual privada em "bridge";
* Cada rede virtual roteia através do firewall NAT no IP do host;
* Todos os containers em uma rede virtual pode conversar com outros sem o `-p`;
* As boas práticas são criar uma nova rede virtual para cada app:
  * rede "my_web_app" para os containers mysql e php/apache;
  * rede "my_api" para o container mongo e nodejs.
* Vincule containers a mais de uma rede virtual (ou não);
* Ignore as redes virtuais e utilize o IP do host (--net=host);
* Use diferentes drivers de rede Docker para ganhar novas habilidades

Se utilizarmos o `ifconfig` para enxergar o IP do container vamos ter um dado. Por outro lado, se utilizar o seguinte comando para ver o IP, teremos um diferente do primeiro:

```docker
docker container inspect --format "{{ .NetworkSettings.IPAddress }}" <container>
```

A explicação disso se dá pela utilização de NAT no docker.

Para mostrar as redes, utilizar o comando:

```docker
docker network ls
```

Para inspecionar uma rede específica:

```docker
docker network inspect
```

Para criar uma rede nova:

```docker
docker network create --driver
```

Assim, ao criar uma rede, ela pode ser inicializada com um container com:

```docker
docker container run -d --name new_nginx --network my_app_net nginx
```

Vincular e desvincular uma rede com um container:

```docker
docker network connect
docker network disconnect
```

**Padrões de segurança em redes ne docker**
* Crie seus aplicativos para que o frontend/backend fique na mesma rede Docker;
• Sua intercomunicação nunca sai do host;
• Todas as portas expostas externamente são fechadas por padrão;
• Você deve expor manualmente via -p, que é o melhor padrão de segurança!;
• Isso fica ainda melhor mais tarde com redes Swarm e Overlay.

**DNS e como os containers se comunicam**

O Docker utiliza os nomes do container como equivalência de um nome de host para eles se conversarem.

Supondo ambiente com dois containers: um chamado `new_nginx` e outro `my_nginx`(verificá-los utilizando `docker container ls`). Se pedimos para inspecionar as redes dos containers veremos que cada um pertence a mesma rede `my_app_net` (inspecionar por `docker network inspect <container name/id>`). Agora, rodando o `my_nginx` com `docker container exec -it my_nginx ping new_nginx` ele vai estar pingando já, apenas pelo DNS da rede, não precisando de IP.
  

#### 4.2.1. Resumo

| Comando                        | Descrição                                               |
| ------------------------------ | ------------------------------------------------------- |
| docker container run           |                                                         |
| docker container stop          |                                                         |
| docker container ls            |                                                         |
| docker container rm            |                                                         |
| docker container top           | lista os processos de um container                      |
| docker container inspect       | detalha a configuração de um container                  |
| docker container stats         | apresenta as estatísticas de todos os containers        |
| docker container port          | checkar quais as portas estão abertas naquele container |
| docker network ls              |                                                         |
| docker network inspect         |                                                         |
| docker network create --driver |                                                         |
| docker network connect         |                                                         |
| docker network disconnect      |                                                         |

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

## 5. FAQ

### Imagens

1. **Como buildar uma nova imagem de um Dockerfile sem o cache?** Caso algum pacote instalado em uma versão anterior for salvo na cache, e essa versão se atualizar, você vai buildar a imagem com a versão antiga. Assim, `docker image build --no-cache -t <tag>:<version> <Dockerfile path>`.

### Containers

1. **Como sair do shell do container sem pará-lo?** <kbd>Ctrl</kbd> + <kbd>P</kbd> + <kbd>Q</kbd> (*read escape sequence*)
2. **Como conectar em um container que está rodando?** `docker container attach <container id>`
3. **Rodei um container do apache/nginx com terminal interativo (`-ti`) e não abre nenhum shell. Por que?**
O container do nginx/apache não tem como entrypoint o bash, mas sim o próprio processo do servidor. Todo processo em execução neste container precisa estar rodando em foreground, não pode estar "daemonizado" (rodando como daemon - em segundo plano/background). Logo, é preciso passar a opção `-d` para rodar o container, ao invés de `-ti` - isso faz com que o container seja um daemon (não é possível dar `attach`).
4. **Então, como conectar em um container rodando como daemon?** `docker container exec -ti <container id> <cmd>`
5. **Como ver todos os detalhes de um container?** `docker container inspect <container id>`
6. **Como ver o histórico de acesso e requisições para o container?** `docker container logs -f <container id>` ou, caso estiver rodando em foreground, o `attach` real-time log (entretanto, para sair depois o atalho de *read escape sequence* não funcionará).
7. **Como passar para o container quanta memória e CPU o container pode utilizar?** `docker container run -d --memory 128M --cpus 0.5 nginx`. Pode-se verificar o tanto de memória e núcleo com o `inspect`, em "*Memory*" e "*NanoCpus*" (no qual 500000000 de nanos cpus = 0.5 CPU).
> Para estressar o container, instalar o pacote **stress** com `apt update && apt install stress`, e rodar `stress --cpu 1 --vm 1 --vm-bytes 64M`
8. **Como fazer a atualização na configuração de um container já em execução?** `docker container update <options> <container id>`. E.g. `--cpus 0.8 --memory 64M`.
9. **Qual a diferença de *mount* do tipo *bind* e *volume*?** O bind será utilizado para quando eu já tenho um diretório no host e quero utilizá-lo dentro do container (e.g. `docker container run -ti --mount type=bind,src=<source path>,dst=<container mount path> <image name>` - as pastas ficam compartilhadas e sincronizadas). Já os volumes são administrados dentro de `/var/lib/docker/volumes` e precisam ser administrados para não saírem com nomes aleatórios. É possível compartilhar volumes entre containers. (e.g. `docker volume create <volume name>`, `docker container run -ti --mount type=volume,src=<volume name>,dst=<container mount path> <image name>`).
10. **Em um container data-only, como fazer backup automaticamente?** No exemplo do volume criado por este container postgres: `docker container run -d -p 5432:5432 --name pqsql1 --mount type=volume,src=dbdados,dst=/data -e POSTGRESQL_USER=docker -e POSTRGRESQL_PASS=docker -e POSTGRESQL_DB=docker kamui/postgresql`, é necessário criar um container para isso, apontando o diretório onde ele vai salvar o backup: `docker container run -ti --mount type=volume,src=dbdados,dst=/data --mount type=bind,scr=/opt/backup,dst=/backup debian tar -cvs /backup/bkp-banco.tar /data`.
11. **Qual a diferença entre a opção do `docker container run`: `-p` e `-P`?** Para o `-p` é preciso passar a porta do host e a do container. O `-P` verifica se tem alguma porta aberta na imagem (EXPOSE do Dockerfile) e "binda" uma porta aleatória ao host.
12. **O que o docker commit faz?** Basicamente, cria a imagem de um container a partir de um container já existente e customizado. Entretanto, não é a melhor maneira de fazer. O ideal sempre é ter o Dockerfile. `docker commit -m "<msg>" <container id>`

### Dockerfile

1. **O Dockerfile cria um container?** Não, ele cria uma imagem personalizada.
2. **Qual a diferença do COPY para o ADD?** O ADD tem a mesma função que o COPY, entretanto ele pega arquivos .tar e copia ele extraído para dentro do container. Outra diferença é para arquivos remotos, que o ADD consegue fazer o download e adicionar dentro do container.

> O ideal é colocar HEALTHCHECKING no compose
### Docker Hub

1. **Como subir uma imagem personalizada para o Docker hub?** Você precisa primeiramente colocar uma tag na sua imagem com `docker image tag <image id> <tag>`, sendo que o `<tag>` deve seguir o formato de `username/imagename:version`. Após isso, logar no seu Docker hub com: `docker login` (preencher com o login e senha) e dar o `docker push`.

### Docker Registry

1. **O que é o Docker Registry?** É o nome dado ao repositório remoto do Docker.
2. **Como criar um Docker Registry?** Nada mais é que um container para registro: `docker run -d -p 5000:5000 --restart always --name registry registry:2`. Assim, a primeira coisa a ser feita para fazer o push para o Registry é dar logout do Docker Hub: `docker logout`. Depois, retaguear a imagem do registry local: `docker image tag <image id> <repository address>/<image name>:<version>` (onde, neste caso, `<repository addres>` = **localhost:5000**). Finalmente, para o push: `docker image push <repository address>/<image name>:<version>`.
3. **Como ver as imagens que tenho carregadas no meu registry?** `curl localhost:5000/v2/_catalog`.
4. **Como ver as tags de uma imagem no repositório registry?** `curl localhost:5000/v2/<image name>/tags/list`, ou dentro do container registry (`docker exec -ti <container id> sh`) na pasta: `cd /var/lib/registry/docker/registry/v2/repositories/`.

### Docker Swarm

1. **O que é o Docker Swarm?** É um orquestrador que já vem embutido no Docker. Tem dois papéis importantes: o manager - administrando os clusters - e o worker - cuja principal função é somente ter container em execução. Entretanto, é possível executar container no manager, diferentemente do Kubernetes. DICA: sempre tem que ter mais de 50% dos managers em pé para o cluster estar saudável.

### Docker Compose

<!-- Markdown's Links -->
<!-- SITES -->
[1]: https://landscape.cncf.io/?zoom=200
[2]: https://docs.docker.com/engine/install/
[3]: https://docs.docker.com

<!-- ARQUIVOS -->

<!-- IMAGENS -->

<!-- COMENTÁRIOS -->
