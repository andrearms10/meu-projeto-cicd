# 🐳 Minha Cola Rápida de Docker (Cheatsheet)

Anotações e comandos essenciais para a aula de Docker.

---

### 📦 Gerenciando Imagens (As Fôrmas)
* `docker pull <imagem>` ➔ Baixa uma imagem do Docker Hub.
* `docker images` ➔ Lista todas as imagens baixadas no meu PC.
* `docker rmi <id_ou_nome>` ➔ Apaga uma imagem do computador.

### 🚀 Rodando Containers (As Máquinas)
* `docker run <imagem>` ➔ Cria e liga um container.
* `docker run --rm <imagem>` ➔ Roda o container e o deleta ao desligar (não acumula lixo).
* `docker run -d <imagem>` ➔ Roda o container escondido em segundo plano.
* `docker run -it ubuntu:22.04 bash` ➔ Entra dentro do terminal do Linux (Ubuntu).

### 🔍 Monitorando o Sistema
* `docker ps` ➔ Lista apenas os containers **ligados** agora.
* `docker ps -a` ➔ Lista **todos** os containers (ligados e desligados).
* `docker logs <id_ou_nome>` ➔ Mostra as mensagens/erros que o container gerou.

### 🧹 Limpeza e Faxina
* `docker stop <id_ou_nome>` ➔ Desliga um container em execução.
* `docker rm <id_ou_nome>` ➔ Apaga um container que já está desligado.
* `docker system prune -a` ➔ O comando "faxina": apaga tudo que não está sendo usado.

### 🚨 Truque do Git Bash (Para o Windows)
Se o Git Bash der erro de caminho (`No such file or directory`), use duas barras:
* `docker run --rm ubuntu:22.04 cat //etc//os-release`
