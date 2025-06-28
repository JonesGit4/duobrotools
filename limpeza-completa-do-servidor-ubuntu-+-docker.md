# Limpeza Completa do Servidor Ubuntu + Docker

## **1. Manual – Limpeza Completa do Servidor Ubuntu + Docker**

#### **A) Remover tudo do Docker (containers, volumes, imagens, redes)**

```bash
bashCopiarEditardocker system prune -af --volumes && echo "✅ Todos containers, imagens, volumes e redes removidos"
```

#### **B) Remover Docker e dependências**

```bash
bashCopiarEditarsudo apt-get remove --purge -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin && sudo apt-get autoremove -y && sudo apt-get autoclean && echo "✅ Docker e dependências removidos"
```

#### **C) Remover diretórios órfãos de stacks, dados e configs**

```bash
bashCopiarEditarsudo rm -rf /var/lib/docker /var/lib/portainer /var/lib/containerd /etc/docker /etc/portainer /opt/portainer /srv/* /opt/* ~/docker* ~/portainer* ~/twenty* ~/compose* ~/stacks* && echo "✅ Diretórios residuais removidos"
```

#### **D) Garantir serviços Docker/Containerd parados**

```bash
bashCopiarEditarsudo systemctl stop docker containerd && sudo systemctl disable docker containerd && echo "✅ Serviços docker/containerd parados"
```

#### **E) Forçar desmontagem de overlay2 (se necessário)**

```bash
bashCopiarEditarsudo umount -l /var/lib/docker/overlay2/*/merged 2>/dev/null && echo "✅ Overlays desmontados"
```

#### **F) Limpar diretório /tmp do Docker**

```bash
bashCopiarEditarsudo rm -rf /var/lib/docker/tmp/* && echo "✅ Docker /tmp limpo"
```

#### **G) Atualizar sistema**

```bash
bashCopiarEditarsudo apt update && sudo apt upgrade -y && echo "✅ Sistema atualizado"
```

#### **H) Instalar Docker e Compose (última versão estável)**

```bash
bashCopiarEditarsudo apt update && sudo apt upgrade -y && sudo apt install -y ca-certificates curl gnupg lsb-release && sudo mkdir -p /etc/apt/keyrings && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo tee /etc/apt/keyrings/docker.asc > /dev/null && sudo chmod a+r /etc/apt/keyrings/docker.asc && echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null && sudo apt update && sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin && sudo systemctl enable docker && sudo systemctl start docker && docker --version && docker compose version && echo "✅ Docker e Docker Compose instalados"
```
