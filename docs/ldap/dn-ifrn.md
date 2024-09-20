O Distinguished Name (DN) é a forma completa de identificar um objeto em uma árvore LDAP (Lightweight Directory Access Protocol). Ele descreve a localização exata de um objeto dentro da árvore de diretórios (Directory Information Tree - DIT) e é composto por vários componentes que descrevem o caminho completo até o objeto.

Vou explicar detalhadamente cada componente do DN que você forneceu:

### DN Completo:

CN=20221148060002,OU=Alunos,OU=DG-PAR,OU=RE,OU=IFRN,DC=ifrn,DC=local

### 1. CN (Common Name):

- CN=20221148060002  
  O CN é o "Common Name" ou nome comum. Ele representa o nome do objeto específico dentro daquela organização. No meu caso, 20221148060002 é o identificador da matrícula. Normalmente, o CN contém o nome real do usuário ou algum código de identificação, como nessção interna.

### 2. OU (Organizational Unit):

- OU=Alunos  
  Essa unidade organizacional (OU) representa o grupo ou categoria de objetos aos quais o seu usuário pertence. Aqui, Alunos indica que meu usuário faz parte do grupo de Alunos.

- OU=DG-PAR
  Esta é outra unidade organizacional, uma subcategoria dentro da organização maior. No caso, DG-PAR refere-se a uma divisão ou departamento específico dentro da instituição, diretoria geral do campus parnamirim.

- OU=RE  
  RE provavelmente se refere à Reitoria ou à administração central do IFRN. Mostra que o objeto está dentro da estrutura administrativa da Reitoria.

- OU=IFRN  
  IFRN representa o Instituto Federal do Rio Grande do Norte, sua instituição educacional. É uma OU de nível mais alto, representando a entidade como um todo.

### 3. DC (Domain Component):

- DC=ifrn  
  O DC é o "Domain Component", e define partes do nome de domínio. Neste caso, ifrn refere-se ao nome do domínio principal da instituição, o IFRN.

- DC=local  
  Esse segundo DC, local, indica que este domínio é um domínio local, ou seja, usado apenas internamente na rede da instituição, e não é um domínio público da internet.

---

### Explicação Completa:

- O DN completo (CN=20221148060002,OU=Alunos,OU=DG-PAR,OU=RE,OU=IFRN,DC=ifrn,DC=local) descreve exatamente onde o objeto do seu usuário está localizado dentro da árvore LDAP.
- RDN (Relative Distinguished Name): O \*\*RDN é a parte do DN que identifica o objeto de forma única dentro de sua unidade organizacional. Neste caso, o RDN do seu usuário é o CN=20221148060002, o que significa que dentro da OU \*\*Alunos, o objeto identificado por esse número é único.

- DC (Domain Component) define o domínio organizacional em que o objeto reside, neste caso, DC=ifrn,DC=local, representando o domínio ifrn.local.

- OU (Organizational Unit) define a hierarquia dentro da organização, separando departamentos, grupos ou subgrupos. Neste exemplo, o usuário pertence a várias OUs: Alunos, *DG-PAR, \*\*RE, e \\*IFRN.

Resumindo, esse DN mostra que o usuário identificado como 20221148060002 está dentro da estrutura do IFRN, especificamente na categoria de Alunos, sob a administração de **DG-PAR, dentro da Reitoria (RE), e sob a organização maior **IFRN, no domínio local ifrn.local.

---

### Estrutura de Componentes:

- CN (Common Name): Nome ou identificador do objeto.
- OU (Organizational Unit): Unidades organizacionais em que o objeto está categorizado.
- DC (Domain Component): Componentes que identificam o domínio, geralmente seguindo o nome do domínio da organização.

Essa estrutura hierárquica é o que permite que o LDAP localize de forma precisa qualquer objeto dentro da árvore de diretórios.

[Baixar o PDF da Explicação do DN em manuscrito](./CamScanner%2019-09-2024%2023.08.pdf)
