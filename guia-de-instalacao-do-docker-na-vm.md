# 🐳 Guia de Instalação do Docker no Ubuntu

Este guia fornece um script automatizado para instalar o **Docker Engine** em sistemas **Ubuntu Linux**. O script cuida da instalação de dependências, configuração do repositório oficial do Docker, e inclusão do usuário ao grupo `docker`.

---

## 📄 Pré-requisitos

* Sistema operacional **Ubuntu 20.04+**
* Acesso de **superusuário (sudo)**
* Conexão com a internet

---

## 📥 Passo a Passo

### 1. Baixe o script

Crie um arquivo chamado `instalar-docker.sh`:

```bash
nano instalar-docker.sh
```

Cole o conteúdo abaixo no arquivo:

```bash
#!/bin/bash

set -e

echo "🔄 Atualizando pacotes do sistema..."
sudo apt update && sudo apt upgrade -y

echo "🐳 Instalando dependências para o Docker..."
sudo apt install -y \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

echo "🔐 Adicionando chave GPG oficial do Docker..."
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
    sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo "📦 Adicionando repositório do Docker..."
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

echo "🔄 Atualizando novamente para incluir repositório do Docker..."
sudo apt update

echo "📥 Instalando Docker Engine..."
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

echo "✅ Habilitando e iniciando o serviço Docker..."
sudo systemctl enable docker
sudo systemctl start docker

echo "👤 Adicionando seu usuário ao grupo docker..."
sudo usermod -aG docker $USER

echo "🚀 Docker instalado com sucesso! Faça logout/login ou reinicie a sessão para usar docker sem sudo."
```

### 2. Dê permissão de execução

```bash
chmod +x instalar-docker.sh
```

### 3. Execute o script

```bash
./instalar-docker.sh
```

---

## ✅ Verificando a instalação

Após reiniciar a sessão (logout/login):

```bash
docker --version
```

Você deve ver algo como:

```
Docker version 24.0.x, build xxxxx
```

---

## 🛠️ Possíveis ajustes

Se você não quiser reiniciar a sessão, rode:

```bash
newgrp docker
```

Assim, o grupo `docker` será aplicado imediatamente ao terminal atual.

---

## 📚 Referências

* [Documentação oficial do Docker](https://docs.docker.com/engine/install/ubuntu/)


