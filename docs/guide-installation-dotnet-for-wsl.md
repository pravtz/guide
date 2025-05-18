
# 🧩 Instalação do .NET no WSL (Ubuntu)

Este guia mostra como instalar o SDK do .NET no WSL com Ubuntu.

---

## ✅ Passo 1: Atualize os pacotes

```bash
sudo apt update && sudo apt upgrade -y
````

---

## ✅ Passo 2: Instale os pré-requisitos

```bash
sudo apt install -y wget apt-transport-https software-properties-common
```

---

## ✅ Passo 3: Adicione o repositório da Microsoft

```bash
wget https://packages.microsoft.com/config/ubuntu/$(lsb_release -rs)/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
rm packages-microsoft-prod.deb
```

---

## ✅ Passo 4: Atualize os pacotes novamente e instale o SDK do .NET

```bash
sudo apt update
sudo apt install -y dotnet-sdk-8.0
```

> 🔄 Você pode substituir `dotnet-sdk-8.0` por `dotnet-sdk-7.0` ou `dotnet-sdk-6.0` conforme sua necessidade.

---

## ✅ Passo 5: Verifique a instalação

```bash
dotnet --version
```

Se retornar a versão do .NET, a instalação foi concluída com sucesso! ✅

---

## (Opcional) Instale o ASP.NET Core Runtime

Caso precise rodar aplicações web:

```bash
sudo apt install -y aspnetcore-runtime-8.0
```

---

## 📝 Observação

Esses comandos funcionam no Ubuntu no WSL 2. Certifique-se de que sua distro esteja atualizada.

```

