---

# Instalação do Samba como Controlador de Domínio Active Directory no Alpine Linux

Este guia fornece instruções passo a passo para instalar e configurar o _Samba_ como um _Controlador de Domínio Active Directory (AD)_ no _Alpine Linux_. O domínio que será configurado é ms.lab.

## 🔧 Requisitos

- _Sistema Operacional:_ Alpine Linux
- _Nome do Domínio:_ ms.lab

---

## 1️⃣ Instalar os Pacotes Necessários

Antes de começar, certifique-se de que seu sistema está atualizado e pronto para a instalação dos pacotes necessários:

```bash
sudo apk update
sudo apk add samba samba-dc samba-winbind samba-winbind-clients krb5-server krb5-libs krb5-dc tdb-tools openrc
```

---

## 2️⃣ Configurar o Kerberos

O Kerberos é crucial para a autenticação no Active Directory. Vamos configurá-lo:

### Editar o arquivo de configuração do Kerberos:

```bash
sudo nano /etc/krb5.conf
```

### Substituir o conteúdo por:

```ini
[libdefaults]
default_realm = MS.LAB
dns_lookup_realm = false
dns_lookup_kdc = true

[realms]
MS.LAB = {
kdc = ad.ms.lab
admin_server = ad.ms.lab
}

[domain_realm]
.ms.lab = MS.LAB
ms.lab = MS.LAB
```

> _Nota:_ Certifique-se de que os nomes de domínio e servidores estão corretamente configurados.

---

## 3️⃣ Configurar o Samba

Agora vamos remover a configuração padrão do Samba e configurar o controlador de domínio.

### Remover qualquer configuração antiga:

```bash
sudo rm /etc/samba/smb.conf
```

### Provisionar o Controlador de Domínio:

Execute o seguinte comando para provisionar o Samba como _Controlador de Domínio Active Directory_:

```bash
sudo samba-tool domain provision --use-rfc2307 --realm=MS.LAB --domain=MS --adminpass=SenhaSegura! --server-role=dc
```

> _Dica:_ Substitua SenhaSegura! por uma senha forte de sua escolha.

---

## 4️⃣ Iniciar o Samba Automaticamente

Configure o Samba para iniciar automaticamente sempre que o sistema for inicializado.

### Adicionar o Samba ao OpenRC:

```bash
sudo rc-update add samba default
```

### Iniciar o Samba manualmente pela primeira vez:

```bash
sudo rc-service samba start
```

---

## 5️⃣ Verificar a Configuração

### Verificar o Nível do Domínio:

Certifique-se de que o Samba foi configurado corretamente:

```bash
sudo samba-tool domain level show
```

### Testar o Kerberos:

Execute os comandos abaixo para verificar se o Kerberos está funcionando corretamente:

```bash
kinit administrator
klist
```

---

## 6️⃣ Configurar o DNS

Se você estiver utilizando o DNS embutido do Samba, certifique-se de que ele está funcionando como esperado:

```bash
dig -t SRV \_ldap.\_tcp.ms.lab
```

---

## 7️⃣ Configurar o Winbind

O _Winbind_ permite que máquinas Linux e Windows interajam com o servidor Samba.

### Editar o arquivo nsswitch.conf:

```bash
sudo nano /etc/nsswitch.conf
```

### Certifique-se de que as seguintes linhas estejam presentes:

passwd: compat winbind
group: compat winbind

### Iniciar o serviço _Winbind_:

```bash
sudo rc-service winbind start
sudo rc-update add winbind default
```

---

## 8️⃣ Conclusão

Parabéns! O Samba foi configurado como um Controlador de Domínio Active Directory no domínio ms.lab.

Agora você pode:

- Conectar máquinas Windows ao domínio
- Gerenciar centralmente os usuários e recursos de rede

> _Dica:_ Para personalizações adicionais, você pode editar o arquivo de configuração localizado em /etc/samba/smb.conf.

---

## 📜 Comandos Úteis

Aqui estão alguns comandos que podem ser úteis para manutenção e monitoramento do Samba e do Kerberos:

### Verificar o status do Samba:

```bash
sudo samba-tool domain level show
```

### Verificar o status do Kerberos:

```bash
kinit administrator
klist
```

### Ver logs e mensagens de erro do Samba:

```bash
tail -f /var/log/samba/log.samba
```

---

## 📚 Recursos Adicionais

- Consulte a [Documentação Oficial do Samba](https://wiki.samba.org/index.php/Main_Page) para obter mais informações e recursos.

---
