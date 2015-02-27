---
layout: page
title: Coding Conventions - C#
---

# Introdução

Este documento define a padronização para formatação de código fonte desenvolvidos em C#, além de expor algumas boas práticas de programação que devem ser seguidas pelos desenvolvedores da Takenet.

# Definições

## Convenções de Capitalização

**Notações**
Os termos seguintes descrevem diferentes formas de se capitalizar identificadores:

 * Pascal case: A primeira letra do identificador e de cada palavra concatenada subsequente é escrita em maiúscula. 
    BackColor
    Person

 * Camel case: A primeira letra do identificador é minúscula e cada palavra concatenada subsequente é escrita em maiúscula.
    backColor
    person
    Upper case – Todas as letras são maiúsculas. Exemplo:
    OK
    IO
    VALUE_FILTER

## Regras de capitalização para identificadores

Quando um identificador for constituído de múltiplas palavras, não utilize '_' (underscore) ou '-'' (hífen) entre as palavras. Ao invés disto, utilize maíuscula na primeira letra de cada palavra. A exceção a esta regra são as constantes, que utilizam notação Upper case, o que dificultaria a identificação das palavras. Neste caso, utilize '_' (underscore) entre as palavras.

| Identificador          | Notação    | Exemplo           |
|------------------------|:----------:|:-----------------:|
| Classe                 | Pascal     | AppDomain         |
| Tipo Enumerador        | Pascal     | ErrorLevel        |
| Valor de Enumerador    | Pascal     | FatalError        |
| Evento                 | Pascal     | ValueChanged      |
| Classe de Exceção      | Pascal     | WebException      |
| Campo somente-leitura  | Pascal     | RedValue          |
| Interface              | Pascal     | IDisposable       |
| Método                 | Pascal     | ToString          |
| Namespace              | Pascal     | System.Drawing    |
| Parâmetro              | Camel      | typeName          |
| Variável local         | Camel      | carTire           |
| Propriedade de Classe  | Pascal     | BackColor         |
| Constante              | Upper Case | DEFAULT_BACKCOLOR |


## Nomenclatura

As definições abaixo se aplicam a variáveis locais, privadas, propriedades e parâmetros dos métodos:

* Use algo significativo, descritivo e em inglês;
 * Mesmo para uma variável temporária que possa aparecer somente em algumas linhas do código, use um nome significativo;
 * Use nomes de variáveis com uma letra, tais como i, j ou k, apenas para índices de um loop e expressões lambda;
 * Coleções de objetos (listas, dicionários, arrays, etc.) devem ser identificadas por palavras no plural.

## Variáveis locais

Os nomes das variáveis locais (declaradas dentro de métodos e usadas como parâmetro) devem seguir a regra abaixo:

 * A primeira letra deve ser minúscula e as letras no início de cada palavra devem ser maiúsculas. (Camel case);
 * Em expressões lambda, utilize nos nomes de variáveis da funções a primeira letra da classe relacionada, caso não seja um tipo primitivo, ou a primeira letra do nome da propriedade em caso de tipos primitivos. Caso o nome já esteja sendo utilizado na mesma expressão, inclua a próxima letra;
 * Na declaração de variáveis de tipos genéricos (dicionários, coleções, etc.), considere utilizar var para melhorar a legibilidade do código;

Faça assim:

    var messages = new List<Message>();
    var sourceMessages = messages.Where(m => m.Source.Equals("553199990000"));

Não faça assim:

    var messages = new List<Message>();
    var sourceMessages = messages.Where(x => x.Source.Equals("553199990000"));

## Variáveis privadas

Os nomes das variáveis privadas devem seguir as regras abaixo:

 * A primeira letra deve ser minúscula e as letras no início de cada palavra devem ser maiúsculas (Camel case);
 * Utilize um substantivo ou uma oração substantiva; 
 * Utilize o prefixo "_" (underscore) em variáveis privadas para diferenciar de variáveis locais ou parâmetros;
 * Em casos que de variáveis privadas com propriedades públicas de leitura, considere utilizar get e private set ao invés de definir uma variável privada e uma propriedade separadamente. Separe apenas em casos de necessidade, como seja necessário passar a variável como referência para algum método, o que não é permitido a propriedades.

Faça assim:

    // Class variable
    private static ServiceHost _serviceHost;
    // Local variable
    string userName = "Nome do usuário";

Não faça assim:

    // Class variable
    public ArrayList glst;  
    // Local variable
    string UserName;
    int Index;

## Propriedades
 * Os nomes das propriedades de classe devem seguir as regras abaixo:
 * A primeira letra deve ser maiúscula e as letras no início de cada palavra devem ser maiúsculas (Pascal case);
 * Utilize um substantivo, uma oração substantiva ou um adjetivo;
 * Em propriedades booleanas, considere os prefixos Is, Can ou Has;
 * Para identificadores ou chaves de entidades do modelo de dados, inclua o sufixo Id;
 * Não crie propriedades que conflitem com métodos existentes na classe (ex: não crie uma propriedade PersonAddress em uma classe que possua um método GetPersonAddress);
 * Considere dar a propriedade o mesmo nome do seu tipo, principalmente em caso de enumeradores.
 
Faça assim:

    public class Message
    {
        public int MessageId { get; set; }
        public Peer From { get; set; }
        public Peer To { get; set; }
        public Content Content { get; set; }
        public string AppSpecific { get; set; }
        public bool HasToNotifySource { get; set; }
    }

Não faça assim:

    public class Message
    {
        public int IDMessage { get; set; }
        public Content ContentData { get; set; }
        public bool SourceNotification { get; set; }
        public Content GetContentData()
        {
            return ContentData;    
        }
    }

## Constantes

As constantes devem utilizar notação Upper case, utilizando underscore para separação das palavras. Devem ser nomeadas de forma clara, indicando com precisão qual o uso da mesma dentro da classe. Normalmente a primeira palavra indicará se é um valor limite (MIN ou MAX) ou um valor padrão (DEFAULT);

Faça assim:

    public class MessageDispatcher
    {
        public const int MAX_SEND_RETRIES = 3;
        public const string DEFAULT_SENDER_ADDRESS = "sender@server.com"; 
    }

Não faça assim:

    public class MessageDispatcher
    {
        public const int RETRY = 3;
        public const string SenderAddress = "sender@server.com"; 
    }

## Consistência

Variáveis que representam o mesmo dado no programa devem ser consistentemente nomeadas durante todas as partes de um programa.

Por exemplo, suponha que você está escrevendo um programa sobre informações de livros e um dado é a data em que o livro foi publicado. Escolha um nome para a data publicada e utilize sempre que o dado for usado. Isto inclui nomes variáveis, nomes de objetos com interface com o usuário, e nomes de colunas em banco de dados.

A única vez que você deve alterar este nome é quando você deve adicionar um prefixo ou mudar a capitalização. 

Faça assim:

    DateTime publishDate = DateTime.Parse(publishDateInput.Text);
    (...)
    books[index].PublishDate = publishDate;
    (...)
    publishDate = book.PublishDate;

Não faça assim:

    DateTime dtPub;
    (...)
    dtPub = DateTime.Parse(txtPubDate.Text);
    (...)
    mBooksArray[index].published = dtPub;
    (...)
    pubDate = book.DatePublshd;

## Métodos

 * Use um nome significativo, descritivo e em inglês.
 * As letras no início de cada palavra devem ser maiúsculas (Pascal case);
 * Os nomes dos métodos devem descrever o que o método faz e não como;
 * Utilize verbos ou expressões verbais.
 * Métodos assíncronos (que retonam Task or Task<T>) devem ter o sufixo Async.

Exemplos: 

    private bool IsDefault()
    {
        (...)
    }

    public Task<string> GetStringAsync(Uri address)
    {
        (...)
    }

    public decimal GetInvoiceTotal()
    {
        (...)
    }

## Classes e interfaces

 * Use um nome significativo, descritivo, no singular e em inglês.
 * As letras no início de cada palavra devem ser maiúsculas (Pascal case);
 * O nome da classe deve descrever o que ela representa;
 * O nome de uma classe geralmente é formado por substantivos;
 * Não utilize uma letra como prefixo de classes;

Faça assim:

    public class ItemType
    {
        (...)
    }

Não faça assim:

    public class TItemType
    {
        (...)
    }

 * Considere incluir no final do nome de classes derivadas o nome da classe base, principalmente se herdar de uma classe abstrata;
 * Inclua sempre no sufixo do nome de classes que herdarem de tipos essenciais do .NET Framework como Exception, Attribute, Stream e EventArgs;
 * Inclua o prefixo I em todas interfaces;
 * A implementação padrão de uma interface deve ter o mesmo nome da interface, exceto pelo prefixo I;

Exemplos:

    public class MessageFormatException : Exception
    {
        // Exception implementation
    }

    public interface IValidator
    {
        bool IsValid(Message message);
    }

## Parâmetros de tipo genérico

Utilize T como parâmetro de tipo genérico se a classe receber apenas um parâmetro deste tipo;

Em caso de classes com mais de um, utilize o prefixo T e um nome descritivo dentro do contexto da classe. Neste caso, utilize Pascal case.

Exemplo:

    public class Message<TContent, TDestination> where TDestination : Peer
    {
        public TContent Content { get; set; }

        public TDestination Destination { get; set; }
    }

## Enumeradores

Utilize as mesmas regras gerais para definição de classes;
Não inclua nenhum prefixo ou sufixo especial para identificar um enumerador;