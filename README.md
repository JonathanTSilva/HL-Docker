# HL-Docker

🛠 Passo a passo que adoto na minha utilização de Docker

- [HL-Docker](#hl-docker)
  - [1. Instalação](#1-instalação)
    - [1.1. Windows](#11-windows)
    - [1.2. MAC](#12-mac)
    - [1.3. Linux](#13-linux)
  - [2. Comandos Básicos](#2-comandos-básicos)
  - [3. Imagem vs Container](#3-imagem-vs-container)
    - [2.1. Imagem](#21-imagem)
    - [2.2. Container](#22-container)
  - [3. Docker File](#3-docker-file)
  - [4. Comandos Intermediários e Avançados](#4-comandos-intermediários-e-avançados)

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

Uma outra analogia simples para melhor compreensão é pensar em uma imagem do Docker como uma receita e um contêiner como o bolo preparado a partir dessa receita. A receita apresenta as instruções para assar o bolo. Você não pode gostar de comer o bolo se não colocar as instruções em ação. É preciso seguir a receita para preparar o bolo e comê-lo. Da mesma forma, você deve seguir as instruções na imagem do Docker para criar e iniciar um contêiner e aproveitar os benefícios do Docker. Você pode assar tantos bolos quanto possível com uma única receita - assim como uma imagem pode criar vários contêineres. No entanto, se você alterar a receita, o sabor dos bolos existentes não mudará. Apenas bolos recém-assados ​​usarão a receita modificada. Da mesma forma, se você fizer alterações em uma imagem de contêiner, não afetará os contêineres já em execução.

### 2.1. Imagem

| Ação    | Comando | Descrição |
| ------- | ------- | --------- |
| Iniciar |         |           |
| Parar   |         |           |
| Listar  |         |           |
| Deletar |         |           |

### 2.2. Container

| Ação    | Comando | Descrição |
| ------- | ------- | --------- |
| Iniciar |         |           |
| Parar   |         |           |
| Listar  |         |           |
| Deletar |         |           |

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

## 3. Docker File

## 4. Comandos Intermediários e Avançados

<!-- Markdown's Links -->
<!-- SITES -->
[1]: https://landscape.cncf.io/?zoom=200
[2]: https://docs.docker.com/engine/install/

<!-- ARQUIVOS -->

<!-- IMAGENS -->

<!-- COMENTÁRIOS -->