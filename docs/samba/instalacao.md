# Instalação do Samba como Controlador de Domínio do Active Directory no Alpine Linux

!!! note "Observações"

    1. Não existe o pacote `samba-tools`
    2. Vocês não configuraram o nome totalmente qualificado da máquina (FQDN: `<capital>.<estado>.lab`)

## Introdução
Guia de instalação e configuração do Samba como um controlador de domínio do Active Directory no Alpine Linux (domínio ms.lab)


## Pré-requisitos
- Alpine Linux.
- Acesso com permissão de usuário root.

## Passo 1: Atualizar o Sistema
Atualize os repositórios e pacotes do Alpine:

```bash
apk update
apk upgrade
```

## Passo 2: Instalando dependências
Instale os pacotes necessários para o Samba, incluindo o controlador de domínio e o Kerberos:

```bash
apk add samba samba-client samba-tools samba-dc krb5 openrc
```

## Passo 3: Configurar o Samba

### 3.1 Modificar o Arquivo /etc/hosts
Edite o arquivo /etc/hosts para incluir o hostname e o IP local:

```bash
micro /etc/hosts
```

Adicione as seguintes linhas:


127.0.0.1 localhost.localdomain localhost
10.1.1.10 ms.lab ms


### 3.2 Criar o Arquivo de Configuração
Crie um novo arquivo de configuração para o Samba:

```bash
micro /etc/samba/smb.conf
```

Adicione a seguinte configuração:

```ini
[global]
   server role = domain controller
   workgroup = ms
   realm = ms.lab
   netbios name = MS
   passdb backend = samba4
   idmap_ldb:use rfc2307 = yes

[netlogon]
   path = /var/lib/samba/sysvol/ms.lab/scripts
   read only = No

[sysvol]
   path = /var/lib/samba/sysvol
   read only = No
```

### 3.3 Criar o Banco de Dados do Samba
Inicialize o banco de dados do Samba:

```bash
samba-tool domain provision --use-rfc2307 --realm=ms.lab --domain=ms --adminpass=SUA_SENHA
```

> *Nota:* Substitua SUA_SENHA por uma senha forte.

## Passo 4: Configurar DNS

### 4.1 Adicionar o Servidor DNS
Edite o arquivo de configuração do DNS em /etc/samba/smb.conf:

```bash
micro /etc/samba/smb.conf
```

Adicione ou edite a linha:

```ini
dns forwarder = 8.8.8.8
```

### 4.2 Configuração do Kerberos
Link o arquivo krb5.conf gerado pelo Samba:

```bash
ln -sf /var/lib/samba/private/krb5.conf /etc/krb5.conf
```

### 4.3 Iniciar o Samba e o DNS
Ative os serviços do Samba:

```bash
rc-update add samba default
rc-service samba start
```

markdown
## Passo 5: Configurar o Firewall

Se você estiver usando um firewall, certifique-se de permitir o tráfego para as portas do Samba. Abaixo está a configuração necessária:

### Configuração de Portas

```bash
# TCP
iptables -A INPUT -p tcp --dport 53 -j ACCEPT
iptables -A INPUT -p tcp --dport 88 -j ACCEPT
iptables -A INPUT -p tcp --dport 135 -j ACCEPT
iptables -A INPUT -p tcp --dport 139 -j ACCEPT
iptables -A INPUT -p tcp --dport 445 -j ACCEPT

# UDP
iptables -A INPUT -p udp --dport 53 -j ACCEPT
iptables -A INPUT -p udp --dport 88 -j ACCEPT
iptables -A INPUT -p udp --dport 137 -j ACCEPT
iptables -A INPUT -p udp --dport 138 -j ACCEPT
```

### Diagrama de Fluxo

```plaintext
+---------------------------+
|       Firewall            |
+---------------------------+
          |
          | Permitir Tráfego
          v
+---------------------------+
|      Permitir TCP         |
|  Portas: 53, 88, 135,     |
|         139, 445          |
+---------------------------+
          |
          | Permitir Tráfego
          v
+---------------------------+
|      Permitir UDP         |
|  Portas: 53, 88, 137,     |
|         138               |
+---------------------------+
```

## Passo 6: Verificar a Instalação
Verifique se o Samba está funcionando corretamente:

```bash
samba-tool domain level show
```

## Passo 7: Adicionar Usuários
Para adicionar usuários ao domínio, use o seguinte comando:

```bash
samba-tool user create SEU_USUARIO SUA_SENHA
```

> *Nota:* Substitua SEU_USUARIO e SUA_SENHA pelos valores desejados.

---

## Diagrama de Configuração do Samba

```
  +-------------------+
  |   Alpine Linux    |
  +-------------------+
           |
           |
  +-------------------+
  |   Samba AD DC     |
  +-------------------+
           |
           |
  +-------------------+
  |  Active Directory |
  +-------------------+
```

---

## Tabela de Portas do Samba

| Protocolo | Porta | Descrição                |
| --------- | ----- | ------------------------ |
| TCP       | 53    | DNS                      |
| TCP       | 88    | Kerberos                 |
| TCP       | 135   | RPC                      |
| TCP       | 139   | NetBIOS Session Service  |
| TCP       | 445   | SMB over TCP             |
| UDP       | 53    | DNS                      |
| UDP       | 88    | Kerberos                 |
| UDP       | 137   | NetBIOS Name Service     |
| UDP       | 138   | NetBIOS Datagram Service |

---
