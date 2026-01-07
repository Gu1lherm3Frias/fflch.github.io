---
layout: default
title: Laravel
parent: Tutoriais
nav_order: 6
---
1. TOC
{:toc}
---

# Pixelfed: Configuração e Desenvolvimento

## Realizando um Fork do pixelfed.

```bash 
git clone git@github.com:pixelfed/pixelfed.git
```

Após clonar o diretório diretamente do repositório oficial do pixelfed, siga para o diretorio salvo na sua máquina. Utilize o comando:

```bash 
cd pixelfed
```

Agora copie o `.env.example`, a fim de ter seu próprio arquivo env, utilize o comando:

```bash 
cp .env.example .env
```

Em seguida utilize o `Composer` para instalar os pacotes necessário para o funcionamento da aplicação. Os comandos `--no-ansi` `--no-interaction` `--optimize-autoloader`, servem argumentos para a execução do comando install, definem respectivamente a realizar o comando sem a utilização de cores ansi do terminal, realizar o comando sem interações do usuário (perguntas de *yes* ou *no*) e otimização da execução do comando utilizado.

```bash
composer install --no-ansi --no-interaction --optimize-autoloader
```