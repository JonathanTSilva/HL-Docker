# HL-Docker

🛠 Passo a passo que adoto na minha utilização de Docker

- [HL-Docker](#hl-docker)
  - [1. Instalação](#1-instalação)
    - [1.1. Windows](#11-windows)
    - [1.2. MAC](#12-mac)
    - [1.3. Linux](#13-linux)
  - [2. Comandos Básicos](#2-comandos-básicos)
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

```docker
docker --version
```

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
docker run [IMAGEM]
docker run ubuntu echo "Hello World"
docker run -it ubuntu
```

```docker
docker ps
docker ps -a
```

```docker
docker start [CONTAINER ID]
docker start -a -i [CONTAINER ID]
```

```docker
docker stop [CONTAINER ID]
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