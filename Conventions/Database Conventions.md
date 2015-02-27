---
layout: page
title: Database Conventions
---

# Introdução

O objetivo deste documento é orientar os desenvolvedores da Takenet a como proceder na construção de bases de dados no SQL Server, apresentando boas práticas e pontos de atenção que devem ser considerados. Além disso, visa manter a padronização do esquema dos bancos afim de minimizar os custos de manutenção.

# Definição do esquema

Esta seção trata as recomendações para a definição da estrutura física dos bancos de dados das aplicações.

## Nomenclatura

O nome de todos os objetos dos banco de dados devem utilizar a notação **PascalCase** (notação conhecida também como UpperCammelCase). Apesar disso, o COLLATION do esquema deve ser **Case Insensitive**.

### Banco de dados

Para o nome do banco de dados, deve-se utilizar o nome da aplicação ou plataforma que utilizará a base de dados. Normalmente, este nome é em **inglês**, mas existem casos que pode estar em português, como por exemplo, quando é uma aplicação que possuí uma marca comercial.

Em casos que hajam versões diferentes do banco e que seja necessário conviver uma versão antiga do mesmo, deve-se utilizar um numeral com sufixo do mesmo. **Não utilize sufixos** como "New" ou "Old" para identificar versões. De qualquer forma, sempre que possível evite manter múltiplas versões do banco de uma aplicação em produção. Prefira sempre a atualização do banco existente.

Exemplos:

    Tangram
    ChargingGateway2
    Torpedao

### Tabelas

As tabelas devem ser nomeadas de acordo com a entidade conceitual que representam, sem abreviações, em inglês e no singular. Em caso de entidades de relacionamento (normalmente em uma relação muitos-para-muitos) o nome da mesma deve ser composto pelas entidades envolvidas na relação, na ordem de importância.

Exemplos:

    Person
    Product
    Store
    Message
    ProductStore

### <span style="font-size: 13px; font-weight: normal;">Caso a tabela seja replicada de algum outro banco, o nome desta deve conter o nome do banco de origem como prefixo, no formato:</span>

**<span style="font-size: 13px;"><Nome do Banco de Origem>_<Nome da Tabela></span>**

Exemplos:

    Tangram3_RequestMessageNotification

### Campos

Os campos devem ser nomeados em inglês, sem abreviações e no singular. Devem representar claramente a informação que armazenam, no contexto da entidade em questão.** Evite utilizar prefixos**, como o nome da entidade (ex: _PersonName_ na tabela _Person_. Utilize apenas _Name_) ou algum identificador do tipo de dados.

Se o campo for** chave primária** da tabela (e o mesmo não seja uma chave primária composta por chaves estrangeiras) deve-se utilizar o sufixo **Id** para identificá-lo, no fomato: 

**<Nome da Entidade>Id**.

No caso do campo ser uma **chave estrangeira**, deve-se grafá-lo da mesma forma que na tabela de origem. A exceção é caso haja mais de uma chave estrangeira para a mesma tabela. Neste caso, inclua um prefixo que qualifique a relação para diferenciá-los (Ex: _ParentPersonId_, _ChildPersonId_).

### Views

As views devem ser nomeadas com o prefixo **Vw**, incluindo o nome das entidades principais e opcionalmente, uma descrição do filtro aplicado pela mesma. Utilize apenas caracteres alfanuméricos. O formato que deve ser utilizado é:

**Vw<Nome da Entidades Principais>[<Descrição do Filtro>]**

Como uma view pode referenciar mais de uma tabela, deve-se escolher para o nome a entidade mais forte envolvida, como uma entidade transacional, excluindo do nome eventuais tabelas de _lookup_ relacionadas. Caso haja mais de uma tabela transacional, deve-se incluir o nome das mesmas na descrição.

Caso haja mais de uma view associada a uma mesma tabela, pode-se incluir no nome da mesma uma descrição dos filtros que a mesma aplica, de forma conceitual.

Exemplos:

    VwMessage
    VwMessageFailed
    VwMessageMtMessageMo
    VwTransaction

### Stored Procedures

As store procedures devem ser nomeadas com o prefixo **Usp**, seguido do nome da entidade principal e o nome da funcionalidade executada, separados pelo caractere "**_**" (_underscore_). O formato que deve ser utilizado é:

**Usp<Nome da Entidade>_<Nome da Funcionalidade>**

O nome da funcionalidade deve indicar de forma clara a interação que a procedure realiza com a tabela. Abaixo uma lista de sugestões de nomes para as funcionalidades das procedures:

<thead>
<tr>
<th>Ação</th>
<th>Sugestão de nome</th>
</tr>
</thead>
<tbody>
<tr>
<td>Inserção de dados</td>
<td>Insert</td>
</tr>
<tr>
<td>Remoção de dados</td>
<td>Delete</td>
</tr>
<tr>
<td>Atualização de dados</td>
<td>Update</td>
</tr>
<tr>
<td>Obtenção de dados por uma coluna</td>
<td>GetBy<nome da="" coluna=""><nome da="" coluna=""></nome></nome></td>
</tr>
</tbody>
</table>

Exemplos:

    UspMessage_Insert
    UspMessage_Delete
    UspMessage_GetById
    UspAccount_GetByUserName

### User Functions

As user functions devem ser nomeadas com o prefixo Ufn seguido do nome da funcionalidade executada. O formato que deve ser utilizado é:

**Ufn<Nome da Funcionalidade>**

Exemplos:

    UfnParameterParser
    UfnAggregate

### Chaves-primárias (constraints)

As chaves-primárias das tabelas devem ser nomeadas utilizando o seguinte formato:

    PK_<Nome da Entidade>

Exemplos:

    PK_Account
    PK_Message

### Chaves-estrangeiras (constraints)

As chaves-estrangeiras das tabelas devem ser nomeadas utilizando o seguinte formato:

    FK_<Nome da Entidade>_<Nome da Propriedade>[_****<Nome da Propriedade>]

Exemplos:

    FK_Account_UserId
    PK_Message_MessageTypeId

Uma chave estrangeira pode ser composta por mais de uma propriedade, caso a tabela de origem tenha chave composta. Neste caso, inclua o nome de todas as colunas, separados por **"_"** (underscore).

### Índices

Os índices das tabelas deve ser nomeados utilizando o seguinte formato:

    IX_<Nome da Entidade>_<Nome da Propriedade>[_****<Nome da Propriedade>]

Exemplos:

    IX_Account_UserId
    IX_Message_MessageTypeId

Um índice pode ser composto por mais de uma propriedade. Neste caso, inclua o nome de todas as colunas, separados por **"_"** (underscore).

## Tipos de dados

Ao escolher os tipos de dados a serem utilizados nas colunas das tabelas, devem ser observados alguns critérios. Abaixo as orientações gerais para alguns dos tipos do SQL Server:

<table border="1">
<thead>
|Tipo|Utilização|
</thead>
<tbody>
<tr>
<td>VARCHAR</td>
<td>

Propriedades literais (strings). É importante definir sempre o tamanho máximo do campo,  
evitando utilizar VARCHAR(MAX), devido a problemas de performance que este tamanho pode trazer 
(além de não ser possível indexar colunas com este tipo).
Algumas sugestões de tamanho para este campo, a partir de informações comuns a vários bancos de dados:

*   Msisdn: 20
*   E-mail: 100
*   Nome: 100
*   Descrição: 250
</td>
</tr>
<tr>
<td>BIT</td>
<td>Propriedades booleanas, onde 0 correponde ao valor "falso" e 1 o valor "verdadeiro".</td>
</tr>
<tr>
<td>BIGINT
INT
SMALLINT
TINYINT</td>
<td>Propriedades numéricas e chaves-primárias de tabelas. 
Na maioria dos casos, o tipo INT deve ser utilizado.
Utilize BIGINT para propriedades que explicitamente precisem de 8 bits ou como chave-primária de tabelas transacionais 
que precisam armazenar um volume extremamente grande (acima de 2 bilhões) de registros.
Considerar utilizar SMALLINT ou TINYINT como chave-primária de tabelas não-transacionais (_lookup_) 
que possam ser referenciadas por tabelas transacionais, com intuito de economizar espaço em disco, observando o 
tamanho máximo suportado por cada tipo e a previsão de crescimento da tabela.</td>
</tr>
<tr>
<td>VARBINARY</td>
<td>Propriedades binárias, como arquivos de mídia (imagens, sons, etc.) com tamanho de até 1 MB.
Considerar criar tabelas separadas para armazenamento de conteúdo, para facilitar a adminstração
do banco.
<nome da="" coluna=""></nome></td>
</tr>
<tr>
<td>FILESTREAM</td>
<td>Propriedades binárias, com tamanho maior que 1 MB.
<nome da="" coluna=""></nome></td>
</tr>
<tr>
<td>UNIQUEIDENTIFIER</td>
<td>

Propriedades do tipo Global Unique Identifier (GUID). Deve-se ter cuidado ao utilizar propriedades deste tipo,
devido ao espaço ocupado. Deve-se sempre que possível evitar utilizar colunas deste tipo como
chave-primária de tabelas e em índices, devido a problemas relacionados a fragmentação de índice.
Para diminuir o impacto neste caso, utilize GUIDs gerados de forma sequencial.

</td>
</tr>
<tr>
<td>DATETIMEOFFSET 
DATETIME
SMALLDATETIME</td>
<td>Propriedades do tipo data e hora.
Para propriedades de tabelas não-transacionais que não é necessário precisão de milissegundos, utilize SMALLDATETIME.
Para propriedades que é necessário esta precisão, utilize DATETIME.
Para propriedades de tabelas transacionais, utilize DATETIMEOFFSET, que inclui a zona de horário e evita problemas
relacionados a diferentes locais e mudanças de hora (horário de verão). Utilize este tipo com a precisão 2.<nome da="" coluna=""></nome></td>
</tr>
</tbody>
</table>

# Desempenho

Algumas considerações de desempenho:

*   Evite o uso de HINTS (ex: NOLOCK) ou comandos (ex: SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED) que alterem o **nível de isolamento** da transação em **stored procedures**. Prefira sempre utilizar o nível padrão do banco de dados;
*   Em comandos UPDATE e DELETE que irão afetar muitos registros (acima de ????), considere incluir a hint ROWLOCK, para evitar o escalonamento do bloqueio para a tabela;
*   Considere utilizar **store procedures** em consultas complexas de aplicações críticas que possam ser beneficiadas com a flexibilidade e desempenho que este recurso pode trazer, mas evite deixar regras da aplicação no banco de dados. Informe tudo que for possível através de parâmetros;

# Segurança

As seguintes recomendações de segurança devem ser consideradas na definição dos banco de dados de aplicações:

*   Utilize **Windows Authentication** ao invés de **SQL Authentication**: A utilização do Windows Authentication evita que seja necessário a aplicação armazenar a senha do banco de dados;
*   Considere utilizar **schemas** em bancos de dados utilizados por aplicações diferentes e que podem acessar conjuntos diferentes de tabela. Crie um **login** separado para cada aplicação e dê permissão somente nos schemas necessários;
*   Ao desenvolver, utilize os ambientes de **desenvolvimento e homologação** para testar as mudanças antes de aplicá-las nos bancos de **produção**. Sempre que possível, teste cenários de carga para avaliar de forma mais precisa os impactos das mudanças. Lembre-se de manter o schema dos bancos de desenvolvimento e homologação atualizados em relação a produção, incluindo todas otimizações realizada neste ambiente;
*   Em **stored procedures**, lembre-se de adicionar o comando SET NOCOUNT ON para evitar a impressão de forma desnecessária do total de linhas afetadas pelos comandos;
*   As rotinas agendadas (jobs) em produção são criados apenas pelo System Administrator, que devem avaliar a consulta e a frequencia que será executada para avaliar possíveis impactos no banco de dados;
*   Permissões de acesso a objetos devem ser concedidas a roles (papéis) da base de dados. Cada role deve ter apenas as permissões que cabem ao papel que representa. Adicione usuários ou grupos apenas aos roles que concederão o acesso necessário ao seu trabalho;

## 

# Boas práticas e recomendações

Algumas recomendações a serem consideradas no desenvolvimento de aplicações com banco de dados:

*   Deve-se sempre ter em mente que o trânsito intenso de dados através da rede compromete a performance da rede como um todo e, principalmente, a das aplicações consultando informações. Desta forma, os comandos de seleção devem estabelecer o retorno do menor conjunto de dados possível, apenas o necessário para a consulta;
*   Em **stored procedures**, inclua sempre um **cabeçalho** com as informações básicas da procedure, como autor e um resumo do funcionamento da mesma, em **inglês**. Utilize o **template** do SQL Management Studio para este fim e o preencha através do comando CTRL + SHIFT + M;
*   Em alguns ORMs, como o EntityFramework, as consultas LINQ são convertidas automaticamente para consultas SQL, sem intervenção do desenvolvedor. Muitas das vezes, estas consultas não são geradas da melhor forma possível, por isso, é importante validar as consultas geradas através de _profilers_, afim de ser possível intervir quando for necessário;
*   Utilize **stored procedures** para execução de **rotinas agendadas** no banco de dados. Considere utilizá-las também em consultas complexas, como sugerido no item Desempenho;
*   Considere a criação de índices em chaves-estrangeiras e em colunas frequentemente utilizadas em consultas da aplicação. Utilize o plano de consulta do SQL Server para conferir sugestões de índices que possam otimizar as mesmas;
</article>