<!-- # Instalação do SAMBA

Pontuação: [30 pontos]

Documente a instalação do Samba no Alpine Linux

Dica:

1. Use o [aplicativo ChatGPT do Celular](https://play.google.com/store/apps/details?id=com.openai.chatgpt&hl=pt_BR)
2. Copie a resposta (Formato Markdown)
3. Cole em uma conversa do WhatsApp com seu colega de grupo
4. Abra o [WhatsApp Web](https://web.whatsapp.com/) em um PC/Notebook
5. Copie o conteúdo da conversa, que deve estar no formato Markdown, e cole em sua documentação.

!!! note "Dica de *prompt* para o [ChatGPT](https://chatgpt.com)"

- Como instalar um servidor Samba como contraldor de domínio do ActiveDirectory. O sistema operacional é o Alpine Linux. O domínio "<estado>.lab". -->

# Instalação do Samba como Controlador de Domínio Active Directory no Alpine Linux

Este guia detalha como instalar e configurar o Samba como um controlador de domínio Active Directory (AD) no Alpine Linux. O domínio que será configurado é ms.lab.

## Requisitos

- _Sistema Operacional_: Alpine Linux
- _Nome do Domínio_: ms.lab

## 1. Instalar os Pacotes Necessários

Primeiro, atualize os repositórios e instale os pacotes necessários para o Samba e o Kerberos:

```bash
sudo apk update
```

```bash
sudo apk add samba samba-dc samba-winbind samba-winbind-clients krb5-server krb5-libs krb5-dc tdb-tools openrc
```

---

## 2. Configurar o Kerberos

Edite o arquivo de configuração do _Kerberos_:

```bash
sudo nano /etc/krb5.conf
```

Substitua o conteúdo por:

ini
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

> _Nota:_ Certifique-se de que o nome de domínio e os servidores estão corretamente configurados.

---

## 3. Configurar o Samba

### Remover Configuração Padrão

Caso haja um arquivo de configuração anterior, remova-o:

```bash

sudo rm /etc/samba/smb.conf
```

### Provisionar o Controlador de Domínio

Execute o seguinte comando para provisionar o Samba como controlador de domínio Active Directory:

```bash
sudo samba-tool domain provision --use-rfc2307 --realm=MS.LAB --domain=MS --adminpass=SenhaSegura! --server-role=dc
```

---

## 4. Iniciar o Samba Automaticamente

Adicione o serviço _Samba_ ao OpenRC para que ele seja iniciado automaticamente:

```bash
sudo rc-update add samba default
```

Inicie o serviço Samba manualmente pela primeira vez:

```bash
sudo rc-service samba start
```

---

## 5. Verificar a Configuração

### Verificar o Nível do Domínio

Verifique se o Samba foi configurado corretamente:

```bash
sudo samba-tool domain level show
```

### Testar o Kerberos

Para verificar se o Kerberos está funcionando corretamente, use:

```bash
kinit administrator
klist
```

---

## 6. Configurar DNS

Se você estiver usando o DNS embutido do Samba, verifique se ele está funcionando corretamente:

```bash
dig -t SRV \_ldap.\_tcp.ms.lab
```

---

## 7. Configurar Winbind

### Editar nsswitch.conf

Abra o arquivo de configuração do _Winbind_:

```bash
sudo nano /etc/nsswitch.conf
```

Certifique-se de que as seguintes linhas estão presentes:

```
passwd: compat winbind
group: compat winbind
```

### Iniciar o Winbind

Inicie o serviço _Winbind_:

```bash
sudo rc-service winbind start
sudo rc-update add winbind default
```

---

## 8. Conclusão

Seu controlador de domínio Active Directory com Samba foi configurado com sucesso no domínio ms.lab. Agora, você pode:

- Conectar máquinas Windows ao domínio
- Gerenciar o ambiente de rede centralizado via Samba.

> _Dica:_ Para mais personalizações, você pode editar o arquivo de configuração do Samba localizado em /etc/samba/smb.conf.

---

## Comandos Úteis

- Para verificar o status do Samba:

```bash
  sudo samba-tool domain level show
```

- Para verificar o status do Kerberos:

```bash
  kinit administrator
  klist
```

- Para ver logs e mensagens de erro do Samba:

```bash
 tail -f /var/log/samba/log.samba
```

---

Se você encontrar problemas ou precisar de mais ajuda, consulte a [documentação oficial do Samba](https://wiki.samba.org/index.php/Main_Page).

---

Com esse formato, a documentação fica mais organizada, usando cabeçalhos claros, blocos de código diferenciados e notas para destacar pontos importantes.
