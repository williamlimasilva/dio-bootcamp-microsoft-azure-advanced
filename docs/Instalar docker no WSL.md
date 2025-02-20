# 🚀 Guia Definitivo: Instalando Docker no WSL 2 sem Docker Desktop 🎯

Se você deseja rodar o Docker no Windows sem precisar do Docker Desktop, este guia passo a passo ajudará você a instalar e configurar tudo corretamente no **WSL 2** (Windows Subsystem for Linux). Vamos cobrir a instalação para **Bash, Zsh e PowerShell**! 💻🐳

---

## 1️⃣ Habilitando o WSL 2 🔥

Se ainda não tem o WSL 2 instalado, siga estes passos:

### No PowerShell:

```powershell
# Instalar o WSL
wsl --install

# Definir o WSL 2 como padrão
wsl --set-default-version 2

# Instalar uma distribuição Linux (ex: Ubuntu)
wsl --install -d Ubuntu
```

Ou instale via **Microsoft Store**.

### Atualizar o Kernel do WSL 2:

Baixe e instale o pacote do kernel do WSL 2 através deste link: 🔗 [Download do Kernel WSL 2](https://aka.ms/wsl2kernel)

---

## 2️⃣ Instalando o Docker no WSL (Ubuntu/Debian) 🐳

Agora, vamos instalar o Docker diretamente na distribuição Linux dentro do WSL.

### Atualizar pacotes do sistema:

```bash
sudo apt update && sudo apt upgrade -y
```

### Instalar pacotes necessários:

```bash
sudo apt install -y ca-certificates curl gnupg lsb-release
```

### Adicionar a chave GPG do Docker:

```bash
sudo mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo tee /etc/apt/keyrings/docker.asc > /dev/null
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

### Adicionar o repositório oficial do Docker:

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### Instalar o Docker:

```bash
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### Adicionar seu usuário ao grupo Docker (para não precisar usar sudo):

```bash
sudo usermod -aG docker $USER
newgrp docker
```

### Verificar a instalação do Docker:

```bash
docker --version
```

---

## 3️⃣ Executando o Docker no WSL 🚀

Por padrão, o serviço do Docker **não inicia automaticamente** dentro do WSL. Então, inicie-o manualmente:

### No Bash/Zsh:

```bash
sudo service docker start
```

### Verificar se o serviço está rodando:

```bash
sudo service docker status
```

### Testar com um container simples:

```bash
docker run hello-world
```

---

## 4️⃣ Tornando o Docker Automático no WSL ⚡

Para evitar iniciar o Docker manualmente sempre que abrir o WSL, crie um script de inicialização:

### Editar o perfil do shell (Bash/Zsh):

```bash
nano ~/.bashrc  # Ou nano ~/.zshrc se estiver usando Zsh
```

### Adicionar a linha no final do arquivo:

```bash
sudo service docker start > /dev/null 2>&1
```

### Salvar e fechar (CTRL + X, Y, Enter).

### Recarregar o shell:

```bash
source ~/.bashrc  # Ou source ~/.zshrc para Zsh
```

Agora, o Docker será iniciado automaticamente sempre que abrir o WSL. 🎉

---

## 5️⃣ Rodando Docker via PowerShell ⚙️

Se quiser rodar comandos Docker diretamente do **PowerShell** sem precisar entrar no WSL, execute:

```powershell
wsl -d Ubuntu -- docker ps
```

### Criar um alias para facilitar o uso no PowerShell:

```powershell
function docker { wsl -d Ubuntu -- docker $args }
```

Agora, você pode rodar `docker ps` no PowerShell como se fosse um comando nativo. 😎

---

## 🎯 Conclusão 🚀

Agora você tem o Docker rodando no **WSL 2** sem precisar do Docker Desktop! Isso economiza **recursos do sistema** e mantém um ambiente mais leve e eficiente para desenvolvimento. 🎉🐳

📌 **Se esse guia te ajudou, compartilhe com a comunidade!** 💡
