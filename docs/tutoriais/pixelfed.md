---
layout: default
title: Pixelfed
parent: Tutoriais
nav_order: 6
---
1. TOC
{:toc}
---

# Pixelfed: Configuração e Desenvolvimento

## Realizando a instalação do pixelfed.

Antes de qualquer coisa lembre-se de ter na sua máquina o Redis instalado, além do php e todas as ferramentas atreladas ao contexto de desenvolvimento como um banco de dados, seja mysql, mariadb ou postgresql.
Para verificar se ele está funcionando utilize o seguinte comando:

```bash
redis-cli ping
```

Deve retornar a palavra PONG no terminal. Pode utilizar as ferramentas de controle do sistema do linux. Exemplo:

```bash
sudo systemctl status redis
```
Agora é necessário configurar o banco de dados que iremos utilizar para o pixelfed. (Algumas dessas informações podem ser verificadas no site oficial).

Aqui neste tutorial estaremos utilizando o MariaDB, Caso já possua instalado um banco de sua preferêcia apenas crie o banco que irá utilizar na sua aplicação. Siga o processo abaixo:

```bash
sudo apt install mariadb-server mariadb-client

sudo systemctl start mariadb # para caso o serviço não tenha iniciado.
sudo systemctl status mariadb # para verificar o estado do serviço.

sudo mariadb
```

Agora crie a instância do banco que irá utilizar, fique a vontade com os nomes estaremos utilizando pixelfed, a senha é de seu encargo.

```java

CREATE DATABASE pixelfed CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

CREATE USER 'pixelfed'@'localhost' IDENTIFIED BY 'senha_de_sua_escolha';

GRANT ALL PRIVILEGES ON pixelfed.* TO 'pixelfed'@'localhost';

FLUSH PRIVILEGES;

EXIT;
```

Tudo pronto podemos dar início ao desenvolvimento com um fork do repositório oficial do pixelfed.

```bash 
git clone git@github.com:pixelfed/pixelfed.git
```

Após clonar o diretório diretamente do repositório oficial do pixelfed, siga para o diretorio salvo na sua máquina. Utilize o comando:

```bash 
cd pixelfed
```
Em seguida utilize o `Composer` para instalar os pacotes necessários para o execução da aplicação. Os comandos `--no-ansi` `--no-interaction` `--optimize-autoloader`, servem argumentos para a execução do comando install, definem respectivamente a realizar o comando sem a utilização de cores ansi do terminal, realizar o comando sem interações do usuário (perguntas de "*yes*" ou "*no*" que podem surgir) e a otimização da execução do comando utilizado.

```bash
composer install --no-ansi --no-interaction --optimize-autoloader
```
Agora copie o `.env.example`, a fim de ter seu próprio arquivo .env, utilize o seguinte comando:

```bash 
cp .env.example .env
```
Após esse processo será necessário configurar o `.env` para o funcionamento adequado e correto. Esse deve ser o contéudo presente no `.env` inicialmente:

```bash
APP_NAME="Pixelfed"
APP_ENV="production"
APP_KEY=
APP_DEBUG="false"

# Instance Configuration
OPEN_REGISTRATION="false"
ENFORCE_EMAIL_VERIFICATION="false"
PF_MAX_USERS="1000"
OAUTH_ENABLED="true"
ENABLE_CONFIG_CACHE="true"
INSTANCE_DISCOVER_PUBLIC="true"

# Media Configuration
PF_OPTIMIZE_IMAGES="true"
IMAGE_QUALITY="80"
MAX_PHOTO_SIZE="15000"
MAX_CAPTION_LENGTH="500"
MAX_ALBUM_LENGTH="4"

# Instance URL Configuration
APP_URL="http://localhost"
APP_DOMAIN="localhost"
ADMIN_DOMAIN="localhost"
SESSION_DOMAIN="localhost"
TRUST_PROXIES="*"

# Database Configuration
DB_CONNECTION="mysql"
DB_HOST="127.0.0.1"
DB_PORT="3306"
DB_DATABASE="pixelfed"
DB_USERNAME="pixelfed"
DB_PASSWORD="pixelfed"

# Redis Configuration
REDIS_CLIENT="predis"
REDIS_SCHEME="tcp"
REDIS_HOST="127.0.0.1"
REDIS_PASSWORD="null"
REDIS_PORT="6379"

# Laravel Configuration
SESSION_DRIVER="database"
CACHE_DRIVER="redis"
QUEUE_DRIVER="redis"
BROADCAST_DRIVER="log"
LOG_CHANNEL="stack"
HORIZON_PREFIX="horizon-"

# ActivityPub Configuration
ACTIVITY_PUB="false"
AP_REMOTE_FOLLOW="false"
AP_INBOX="false"
AP_OUTBOX="false"
AP_SHAREDINBOX="false"

# Experimental Configuration
EXP_EMC="true"

## Mail Configuration (Post-Installer)
MAIL_DRIVER=log
MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="pixelfed@example.com"
MAIL_FROM_NAME="Pixelfed"

## S3 Configuration (Post-Installer)
PF_ENABLE_CLOUD=false
FILESYSTEM_CLOUD=s3
#AWS_ACCESS_KEY_ID=
#AWS_SECRET_ACCESS_KEY=
#AWS_DEFAULT_REGION=
#AWS_BUCKET=<BucketName>
#AWS_URL=
#AWS_ENDPOINT=
#AWS_USE_PATH_STYLE_ENDPOINT=false
```



inicie o servidor, queue e o schedule

reconfigure a tabela statuses
