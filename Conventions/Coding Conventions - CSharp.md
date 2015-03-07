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
 * Upper case – Todas as letras são maiúsculas. Exemplo:
    OK
    IO
    VALUE_FILTER

## Regras de capitalização para identificadores

Quando um identificador for constituído de múltiplas palavras, não utilize '_' (underscore) ou '-'' (hífen) entre as palavras. Ao invés disto, utilize maíuscula na primeira letra de cada palavra. A exceção a esta regra são as constantes, que utilizam notação Upper case, o que dificultaria a identificação das palavras. Neste caso, utilize '_' (underscore) entre as palavras.

<table>
<thead>
<tr>
<th>Identificador</th>
<th style="text-align:center">Notação</th>
<th style="text-align:center">Exemplo</th>
</tr>
</thead>
<tbody>
<tr>
<td>Classe</td>
<td style="text-align:center">Pascal</td>
<td style="text-align:center">AppDomain</td>
</tr>
<tr>
<td>Tipo Enumerador</td>
<td style="text-align:center">Pascal</td>
<td style="text-align:center">ErrorLevel</td>
</tr>
<tr>
<td>Valor de Enumerador</td>
<td style="text-align:center">Pascal</td>
<td style="text-align:center">FatalError</td>
</tr>
<tr>
<td>Evento</td>
<td style="text-align:center">Pascal</td>
<td style="text-align:center">ValueChanged</td>
</tr>
<tr>
<td>Classe de Exceção</td>
<td style="text-align:center">Pascal</td>
<td style="text-align:center">WebException</td>
</tr>
<tr>
<td>Campo somente-leitura</td>
<td style="text-align:center">Pascal</td>
<td style="text-align:center">RedValue</td>
</tr>
<tr>
<td>Interface</td>
<td style="text-align:center">Pascal</td>
<td style="text-align:center">IDisposable</td>
</tr>
<tr>
<td>Método</td>
<td style="text-align:center">Pascal</td>
<td style="text-align:center">ToString</td>
</tr>
<tr>
<td>Namespace</td>
<td style="text-align:center">Pascal</td>
<td style="text-align:center">System.Drawing</td>
</tr>
<tr>
<td>Parâmetro</td>
<td style="text-align:center">Camel</td>
<td style="text-align:center">typeName</td>
</tr>
<tr>
<td>Variável local</td>
<td style="text-align:center">Camel</td>
<td style="text-align:center">carTire</td>
</tr>
<tr>
<td>Propriedade de Classe</td>
<td style="text-align:center">Pascal</td>
<td style="text-align:center">BackColor</td>
</tr>
<tr>
<td>Constante</td>
<td style="text-align:center">Upper Case</td>
<td style="text-align:center">DEFAULT_BACKCOLOR</td>
</tr>
</tbody>
</table>


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

## Eventos

 * Utilize as mesmas regras gerais para definição de classes;
 * Utilize um verbo ou uma locução verbal;
 * O delegate do evento deve ser EventHandler, caso receba apenas EventArgs ou EventHandler<T>, caso exista uma implementação especifica de EventArgs para o evento. Neste caso, T é o tipo desta implementação;
 * Nomeie os eventos nos tempos verbais gerúndio para eventos que estão acontecendo e particípio para eventos que acabaram de acontecer;
 * 
Exemplo:

    public class MessageParser
    {
        public event EventHandler<MessageEventArgs> Parsing;

        public event EventHandler<MessageEventArgs> Parsed;
    }

    public class MessageEventArgs : EventArgs
    {
        public string Text { get; set; }
    }

## Arquivos de código-fonte

O nome de um arquivo de código fonte geralmente deve ser o nome da classe que o contém. No caso de um arquivo ter mais de uma classe, então o arquivo deve ter o nome da classe de maior relevância. De qualquer forma, é recomendado evitar arquivos com mais de uma classe.

Exemplo:   
A classe ItemType deve ter o seu arquivo nomeado como ItemType.cs 

## Namespaces

Os namespaces devem seguir obrigatoriamente o seguinte padrão:

    <Empresa>.<(Produto|Tecnologia)>.<(Funcionalidade|Módulo)>.<Submódulo>

 * Use nomes significativos, descritivos, no singular e em inglês.
 * As letras no início de cada palavra devem ser maiúsculas (Pascal case);
 * O namespace raíz de todos os projetos desenvolvidos na empresa é Takenet.   Não utilize TakeNET, TakeNet ou Take.net;
 * Não utilize nome de departamentos ou equipes em qualquer parte do namespace;
 * Considere pluralizar o nome das funcionalidades ou módulos no namespace sempre que necessário;
 * 
Exemplos:

    namespace Takenet.PRM.Entities
    {
        (...)
    }
    namespace Takenet.ChargingGateway.Admin.Forms
    {
        (...)
    }

## Comentários

### Simples

 * Os comentários devem ser incluídos no código fonte para indicar o que o código faz e para quebrar grandes seções do código.
 * Os comentários do código fonte devem ser claros, conciso, obrigatoriamente em inglês e devem possuir a gramática correta;
 * As linhas de comentários devem começar com // indentado no mesmo nível que o código está;
 * Não use /*... */ para blocos de comentários; 
 * Os comentários não devem incluir observações humorística. Seus comentários podem parecer engraçados quando você digita, mas não são para uma pessoa que tem que entender e corrigir seu código a meia noite para eliminar erros;
 * Os comentários não devem ser usados para ensinar ao leitor como programar. Suponha que o leitor saiba o mesmo tanto que você sabe sobre a linguagem de programação;
 * Os comentários não devem ser usados para descrever o código óbvio, mas lembre-se que sua lógica de programação não é tão obvia para as outras pessoas. A finalidade dos comentários é aumentar a legibilidade do código. Frequentemente usar bons nomes de variáveis e de métodos faz com que o código fique mais fácil de ler do que um código com muitos comentários;
 * Nunca comente uma parte do código. Se o código não for necessário, deve ser apagado;
 * Não use comentários confusos, tais como uma linha inteira dos asteriscos.  Em lugar disso, use uma única linha em branco para separar comentários do código;
 * Não desenhe "Caixas de Flores" em torno dos comentários usando fileiras dos asteriscos ou de outros caráteres;
 * O Visual Studio possui diversos atalhos para ajudar com os comentários. Para comentar um bloco, selecione o conteúdo e utilize o atalho “Ctrl+K, Ctrl+C” (default), e para remover o comentário “Ctrl+K, Ctrl+U”.

## Documentação das classes

No .NET Framework, a Microsoft introduziu um sistema para gerar documentação baseado em comentários XML. Esta documentação são basicamente comentários em linha C# contendo tags XML. O padrão que deve ser seguido é:

    /// <summary>
    /// This class ...
    /// </summary>

Comentários com múltiplas linhas seguem o seguinte padrão:

    /// <exception cref=”BogusException”>
    /// This exception is throw 
    /// if the error occours...
    /// </exception>

Exemplo:

    /// <summary>
    /// Get the default product price in the current store
    /// </summary>
    /// <param name="product">Instance of <see cref="Product"/></param>
    /// <returns>Instance of <see cref="Price"/> with the valid prices
    /// for the product</returns> 
    private Price GetPrice(Product product)
    {
        (...)
    }


No caso de estar desenvolvendo alguma biblioteca, é importante disponibilizar estes comentários para outros desenvolvedores. Para isso, nas propriedades do projeto, dentro da aba “Build”, marque a opção “XML documentation file” e escolha um caminho para o arquivo.

## Regiões

Utilize as diretivas `#region/#endregion` para agrupar partes relacionadas da classe facilitar a leitura do código da mesma. Deve ser utilizado para separar propriedades dos métodos, além dos construtores. Além disso, as propriedades públicas e privadas podem ser separadas em regiões diferentes. 

Não utilize regions dentro do código de métodos/construtores da classe, pois a necessidade disso pode indicar que este código está longo demais e deve ser refatorado ou dividido em outros métodos.

## Source control
Os comentários são obrigatórios em todo check-in/commit realizado no source control (TFS, Git, etc.). Estes devem explicar de forma objetiva as principais mudanças realizadas no código. Da mesma forma que os comentários de código, devem sem em inglês. 

Uma recomendação para evitar descrições longas demais é realizar o check-in/commit sempre que possível em porções funcionais do código alterado. Desta forma, evita-se esquecer alterações importantes que por ventura foram realizadas mas que não constam no comentário.

 ## Tipos de dados

Use sempre os tipos pré-definidos do C# e não utilize os pseudônimos do namespace System.

Faça assim:

    <pre>`string firstName;
    bool isPerson;
    short itemCounter;`</pre>

Não faça assim:

    <pre>`String firstName;
    Boolean isPerson;
    Int16 itemCounter;`</pre>

## Formatação

### Espaços e linhas em branco

Use um espaço antes e depois da maioria dos operadores. As exceções incluem ++ e --. Os ";" (ponto e vírgula) devem ser o último caráter da linha, não podendo haver espaços depois.

Além disso, separe blocos de código com uma linha em branco para facilitar a leitura.

Faça assim:

    <pre>`public void ShowMessage(string message, bool showTime)
    {
        string newMessage = string.Format("A mensagem original é: {0}",
            message);

        if (showTime)
        {
            DateTime currentTime = DateTime.Now;
            newMessage = string.Format("{0}. {1}", message, 
                currentTime);
        }

        MessageBox.Show(newMessage);
    }`</pre>

Não faça assim:

    <pre>`public void ShowMessage(string message, bool showTime)
    {
        string newMessage=string.Format("A mensagem original é: {0}",
            message) ;

        if (showTime)
        {
            DateTime currentTime=DateTime.Now ;
            newMessage =string.Format("{0}. {1}",message,currentTime) ;
        }        
        MessageBox.Show(newMessage);
    }`</pre>

### Uma expressão por linha

Cada linha do código não deve conter mais de uma declaração. Declarar várias variáveis em uma só linha faz o código ficar mais difícil de ler.

Faça assim:

    <pre>`string city;
    string state;
    string zip;`</pre>

Não faça assim:

    <pre>`string address, city, state, zip;`</pre>

### Indentação

Deve-se indentar todas as expressões dentro das classes, métodos, loops, switchs, blocos de try/catch, etc. Utilize para indentação a tecla TAB, e defina o número de espaços de tabulação como quatro.

Faça assim:

    <pre>`private bool IsInZone()
    {
        private const double MAX_LATITUDE_LONGITUDE_DIFFERENCE = .0003;

        foreach (TourZone tourZone in TourZones)
        {
            if (tourZone.ZoneID != this.currentZone.ZoneID)
            {
                double latituteDifference = Math.Abs(Math.Abs(tz.Lat) -  
                    Math.Abs(mCurrentLat));
                double longitudeDifference = Math.Abs(Math.Abs(tz.Long) – 
                    Math.Abs(mCurrentLong));

                if (latDiff < latLongDiff
                    && longDiff < latLongDiff)
                {
                    // The user is fairly close to the coordinates 
                    mCurrentZone = tz;
                    return true;
                }
            }
        }

        return false;
    }`</pre>

Não faça assim:

    <pre>`private bool InZone()
    {
        private const double MAX_LATITUDE_LONGITUDE_DIFFERENCE = .0003;
        foreach (TourZone tz in mTourZones)
        {
        if (tz.ZoneID != mCurrentZone.ZoneID)
        {
        double latDiff = Math.Abs(Math.Abs(tz.Lat) -  
        Math.Abs(mCurrentLat));
        double longDiff = Math.Abs(Math.Abs(tz.Long) – 
            Math.Abs(mCurrentLong));
            if (latDiff < latLongDiff
            && longDiff < latLongDiff)
            {
            // The user is fairly close to the coordinates 
            mCurrentZone = tz;
            return true;
            }
        }
        }
    return false;
    }`</pre>

Dica: O Visual Studio possui um atalho para formatar o código automaticamente. Basta selecionar a parte desejada e teclar “Ctrl+K, Ctrl+D”.

### Alinhamento de Chaves

Alinhe chaves abertas e fechadas verticalmente onde os pares das chaves devem ser colocados em uma linha por expressão.

Faça assim:

    <pre>`public void ShowMessage(string message, bool showTime)
    {
        if (showTime)
        {
            DateTime currentTime = DateTime.Now;
            message = string.Format("{0}. {1}", message, 
                currentTime);
        }

        MessageBox.Show(message);
    }`</pre>

Não faça assim:

    <pre>`public void ShowMessage(string message, bool showTime)   {
        if (showTime)  {
        DateTime currentTime = DateTime.Now;
        message = string.Format("{0}. {1}", message, 
        currentTime);
        }

        MessageBox.Show(message);
    }`</pre>

### Decisões

Sempre utilize chaves em uma condição if, mesmo se a condição for verdadeira e executar apenas uma linha.

Faça assim:

    <pre>`if (item != null)
    {
        itemCounter++;
    }`</pre>

Não faça assim:

    <pre>`if (item != null)
        itemCounter++;
    if (item != null) itemCounter++;`</pre>

Quando as expressões lógicas de uma condição incluem mais de duas expressões, coloque cada condição em uma linha ou no máximo duas e comece cada linha com o operador lógico, indentando um nível (4 espaços).

Faça assim:

    <pre>`if (txtID.Text.Length == 5
        && !string.IsNullOrEmpty(txtFirstName.Text)
        && txtClass.Text.Length == 2)
    {
        cmdCalculate.Enabled = true;
    }`</pre>

Não faça assim:

    <pre>`if (txtID.Text.Length == 5 && txtFirstName.Text != "" && test == true && txtLastName.Text != "" && txtStartDate.Text != "" && txtClass.Text.Length == 2)
    {
        cmdCalculate.Enabled = true;
    }`</pre>

### Using vs Namespace

Utilize o "using" no lugar de utilizar todo o namespace mais o nome do tipo na declaração da variável.

Faça assim:

    <pre>`using System.Net
    (...)
    IPAddress ipAdress = IPAddress.Parse("192.168.0.1");`</pre>

Não faça assim:

    <pre>`System.Net.IPAddress ipAd = System.Net.IPAddress.Parse("192.168.0.1");`</pre>

Uma exceção a esta regra é quando existem tipos com o mesmo nome em namespaces diferentes, e um dos namespaces estão nos using do arquivo. Considere utilizar a palavra-chave var nestes casos, para melhorar a legibilidade do código.

# Boas práticas de programação

 * Evite escrever métodos muito longos. Um método normalmente possui entre 1 e 25 linhas de código. Se um método estiver com mais de 25 linhas, considere a refatoração de partes do código em métodos separados;
 * Métodos devem fazer apenas um trabalho. Não combine mais de uma funcionalidade em apenas um método, mesmo que sejam pequenas;

Faça assim:

    <pre>`void SaveAddress(string address)
    {
        // Saves the address
        // ...
    }

    void SendEmail(string address, string email)
    {
        // Sends an e-mail to the manager about the address change        
    }`</pre>

Não faça assim:

    <pre>`// Saves the address and sends an e-mail to the manager about 
    // the address change
    void SaveAddress( string address, string email )
    {
    // Job 1.
    // Saves the e-mail
    // ...
    // Job 2.
    // Sends the e-mail
    // ...
    }`</pre>

 * **Jamais** deixe variáveis com valores fixos no código (hard-code), como por exemplo um caminho no disco ou um identificador qualquer de uma tabela. Utilize para isso o arquivo de configuração da aplicação, arquivos de recurso ou constantes. No caso de caminhos em disco, prefira utilizar caminhos relativos ou então descubra-os dinamicamente, através da classe **Path**;
 * Se for comparar uma string com outra, utilize o método **Equals**. E se a comparação for case insensitive, inclua o parâmetro **StringComparison.OrdinalIgnoreCase**;
 * Utilize **string.Empty** ao invés de aspas duplas vazias ("") para declarar uma string vazia;
 * Utilize o método **string.IsNullOrWhiteSpace(string)** para validar se uma string é nula, vazia ou espaço em branco. Evite comparar com **null** ou **string.Empty**;
 * Não deixe variáveis de classe com visibilidade protected ou public. Sempre mantenha-as private e as exponha utilizando propriedades **get** /** set**;
 * **Jamais** assuma que sua aplicação vai rodar em um drive de disco específico (C:, D:);
 * Mensagens de erro devem **ajudar** o usuário a resolver o problema. **Nunca** exiba mensagens do tipo “Erro na aplicação”, “Ocorreu um erro”, etc. Exiba mensagens **específicas**, como por exemplo “Ocorreu um erro ao acessar o banco de dados. Verifique se o usuário/senha estão corretos”;
 * Mostre mensagens **amigáveis** aos usuários. Mas insira em Log todas as informações possíveis sobre o erro, para ajudar a resolver o problema;
 * Evite ter arquivos muito grandes. Se um arquivo possui mais de 1000 linhas de código, ele é um sério candidato a refatoração. Divida-o em duas ou mais classes;
 * Evite **métodos públicos**, a não ser que realmente ele precise ser acessado de fora da classe. Utilize **internal** se o método for acessado dentro da mesma **assembly**;
 * Utilize **Enums** sempre que necessário. Nunca utilize números ou strings para indicar valores discretos:

Faça assim:

    <pre>`public enum MailType
    {
        Html,
        PlainText
    }

    private void SendMail(string message, MailType mailType)
    {
        switch (mailType)
        {
            case MailType.Html:
            // HTML
            break;
            case MailType.PlainText:
            // Text
            break;
        }
    }`</pre>

    Não faça assim:

    <pre>`void SendMail(string message, int mailType)
    {
        switch (mailType)
        {
            case 1:
                // HTML
                break;
            case 2:
                // Text
                break;
        }
    }

 * Evite passar muitos parâmetros para um método. Se você tem mais do que 4 ou 5 parâmetros, considere criar uma **struct** ou **class**;
 * Se você tem um método que retorna uma coleção, retorne uma **coleção vazia** ao invés de null, se for o caso de não existir dados para retornar;
 * Utilize o arquivo **AssemblyInfo.cs** para fornecer informações como versão, descrição, nome da empresa do assembly;
 * Organize os arquivos do seu projeto com pastas, que agrupam logicamente classes com funcionalidade em comum;
 * Declare variáveis o mais próximo possível de onde vai utilizá-la pela primeira vez;
 * Utilize a classe **StringBuilder** ao invés da string quando precisa concatenar string dentro de estruturas de loop. O objetos string no .NET possuem um comportamento estranho: toda vez que se concatena uma string, é descartado o objeto com o valor velho e é instanciado um novo objeto string com o novo valor, o que é uma operação cara;
 * Se for distribuir um assembly, como um cliente de sua aplicação ou uma biblioteca utilitária, utilize o NuGet. A Takenet tem uma instância do serviço em http://nuget.takenet.com.br;
 * Defina sempre **interfaces** para suas classes e evite referenciar uma implementação diretamente, mas sim uma interface. Esta prática facilita a criação de testes unitários pois torna possível criar mocks das referências. Caso esteja referenciando classes de bibliotecas externas sem interface pública definida, considere implementar uma classe container, definindo uma interface extraída da implementação (Dica: utilize o recurso Extract Interface do Visual Studio, dentro do menu Refactor);
 * Evite utilizar a palavra-chave **new** dentro de suas classes. Uma classe deve receber todas as referências necessárias no seu construtor. Considere utilizar um container de **injeção de dependência** para controlar o ciclo de vida dos seus objetos.
