<!-- O Distinguished Name (DN) é a forma completa de identificar um objeto em uma árvore LDAP (Lightweight Directory Access Protocol). Ele descreve a localização exata de um objeto dentro da árvore de diretórios (Directory Information Tree - DIT) e é composto por vários componentes que descrevem o caminho completo até o objeto.

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

[Baixar o PDF da Explicação do DN em manuscrito](./CamScanner%2019-09-2024%2023.08.pdf) -->

---

# Componentes do Distinguished Name (DN)

## DN Completo:

_CN=20221148060002,OU=Alunos,OU=DG-PAR,OU=RE,OU=IFRN,DC=ifrn,DC=local_

---

## 1. Explicação dos Componentes

Componentes do DN:

### Tabela Explicativa dos Componentes do DN

| _Componente_ | _Significado_       | _Descrição_                                                                              |
| ------------ | ------------------- | ---------------------------------------------------------------------------------------- |
| _CN_         | Common Name         | Nome comum ou identificador único do objeto (neste caso, a matrícula do aluno).          |
| _OU_         | Organizational Unit | Unidades organizacionais que categorizam o objeto, indicando subgrupos ou departamentos. |
| _DC_         | Domain Component    | Componentes de domínio que especificam o domínio da organização (ex: ifrn.local).        |

---

## 2. Tabela Detalhada do DN

Tabela detalhada descrevendo cada componente do DN:

| _Componente_ | _Valor_        | _Descrição_                                                         |
| ------------ | -------------- | ------------------------------------------------------------------- |
| _CN_         | 20221148060002 | Número de matrícula do aluno.                                       |
| _OU_         | Alunos         | Grupo de alunos.                                                    |
| _OU_         | DG-PAR         | Diretoria Geral de Parnamirim (DG-PAR), parte da estrutura do IFRN. |
| _OU_         | RE             | Reitoria do IFRN.                                                   |
| _OU_         | IFRN           | Instituto Federal do Rio Grande do Norte (IFRN).                    |
| _DC_         | ifrn           | Nome do domínio da organização (IFRN).                              |
| _DC_         | local          | Domínio local, indicando que se trata de uma rede interna.          |

---

## 3. Componentes do DN

Aqui está uma descrição detalhada de cada componente do DN e o que ele representa:

---

### _1. CN (Common Name):_

- _Valor:_ 20221148060002
- _Descrição:_ O CN (Common Name) é o identificador único do objeto dentro da árvore LDAP. No caso, 20221148060002 é o número de matrícula do aluno, usado como identificador exclusivo.

---

### _2. OU (Organizational Unit):_

As _Unidades Organizacionais (OU)_ definem grupos e subgrupos dentro da organização.

- _Valor:_ Alunos  
  _Descrição:_ Representa a unidade organizacional para os alunos da instituição. Esse grupo categoriza o objeto como um aluno.

- _Valor:_ DG-PAR  
  _Descrição:_ Refere-se à _Diretoria Geral do Campus Parnamirim_. Essa OU organiza objetos dentro dessa divisão administrativa específica.

- _Valor:_ RE  
  _Descrição:_ Representa a _Reitoria (RE)_, a administração central do IFRN. Essa OU categoriza o objeto dentro da estrutura administrativa da Reitoria.

- _Valor:_ IFRN  
  _Descrição:_ A OU de nível mais alto que representa o _Instituto Federal do Rio Grande do Norte (IFRN)_. Ela identifica a organização como um todo.

---

### _3. DC (Domain Component):_

Os _Domain Components (DC)_ definem o domínio ao qual o objeto pertence, geralmente representando o nome do domínio da organização.

- _Valor:_ ifrn  
  _Descrição:_ Este _DC_ representa o domínio do Instituto Federal do Rio Grande do Norte (IFRN).

- _Valor:_ local  
  _Descrição:_ Este segundo _DC_ indica que o domínio é local, o que significa que é utilizado exclusivamente dentro da rede interna da organização, sem estar exposto publicamente na internet.

---

### Resumo Visual:

- _CN:_ 20221148060002 (Matrícula do Aluno)
- _OU:_
  - Alunos (Grupo dos Alunos)
  - DG-PAR (Diretoria Geral do Campus Parnamirim)
  - RE (Reitoria)
  - IFRN (Instituto Federal do Rio Grande do Norte)
- _DC:_
  - ifrn (Domínio da instituição)
  - local (Rede interna local)

---

## 4. Resumo da Estrutura do DN

| _Nível_   | _Componente_      | _Descrição_                                                          |
| --------- | ----------------- | -------------------------------------------------------------------- |
| _Nível 1_ | DC=ifrn, DC=local | Indica o domínio organizacional local (ifrn.local).                  |
| _Nível 2_ | OU=IFRN           | Unidade organizacional representando o IFRN como uma entidade.       |
| _Nível 3_ | OU=RE             | Subdivisão da reitoria, representando a administração central.       |
| _Nível 4_ | OU=DG-PAR         | Diretoria Geral do Campus Parnamirim.                                |
| _Nível 5_ | OU=Alunos         | Grupo de alunos na organização.                                      |
| _Nível 6_ | CN=20221148060002 | Identificador exclusivo do aluno, neste caso, o número de matrícula. |

---

## 5. Conclusão

O DN completo fornecido (CN=20221148060002,OU=Alunos,OU=DG-PAR,OU=RE,OU=IFRN,DC=ifrn,DC=local) descreve a localização exata do objeto (um aluno) dentro da árvore LDAP. A hierarquia é claramente representada através das unidades organizacionais e componentes de domínio que categorizam o objeto no contexto do IFRN.

Essa estrutura permite que o _LDAP_ localize e gerencie o objeto de forma eficaz dentro de uma rede organizada e hierárquica.

---

---

## 📄 Explicação do DN em Manuscrito

Você pode acessar a explicação completa do _Distinguished Name (DN)_ em formato PDF através do link abaixo:

> _[Clique aqui para baixar o PDF](./CamScanner%2019-09-2024%2023.08.pdf)_  
> (Explicação detalhada do DN em manuscrito)

---
