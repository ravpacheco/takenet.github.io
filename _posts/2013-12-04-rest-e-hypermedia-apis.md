---
layout: post
title: Rest e hypermedia apis
---

![Imgur](http://i.imgur.com/LsZYXWN.jpg)

Muito se fala sobre REST e as práticas “corretas” que devem ser adotadas ao construir um sistema baseado neste estilo arquitetural. Mas o que acontece na verdade é uma grande confusão de conceitos que não tem relação com a proposta original do que seria uma aplicação RESTful.

REST é um acrônimo para Representational State Transfer (Transferência representacional de estado) e termo surgiu na [dissertação de doutorado](http://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm) de [Roy Fielding](http://roy.gbiv.com/untangled/), que também colaborou (não coincidentemente) com a especificação do protocolo HTTP. Ele definiu alguns pré-requisitos deve devem ser cumpridos para que uma arquitetura possa ser chamada de RESTful, que resumidamente são:

 * **Ser cliente-servidor** – Deve sempre haver um cliente que realiza as requisições e um servidor que as responde;
* **Sem estado** – As requisições feitas pelo cliente devem conter todas as informações necessárias para que o servidor consiga processar o pedido. Ou seja, o servidor não tem seu estado alterado e não trata requisições semelhantes de formas diferentes devido a isso. Note que os recursos que o servidor provê podem ser alterados, e que isso é completamente diferente do estado da aplicação;
* **Cache** – As respostas às requisições feitas pelo cliente podem ser marcadas como “cacheáveis” ou “não-cacheáveis” pelo servidor, indicando se podem ou não ser armazenadas em cache pelo cliente;
* **Interface uniforme** – Um dos pontos centrais do REST é a ênfase na interface uniforme entre os componentes da arquitetura. As informações devem ser transferidas de forma padronizada. Este pré-requisito define outros quatro pré-requisitos de interface:
  * **Identificação dos recursos** – Cada recurso deve possuir um identificador universal (URI – Universal Resource Identifier);
  * **Representação de recursos** – Os recursos são manipulados a partir de suas representações, que podem ser em diversos formatos, como XML, JSON, TEXT, etc. Um detalhe importante que uma aplicação REST não transmite o recurso efetivamente, mas sempre uma representação do mesmo, em um formato pré-acordado entre o cliente e o servidor;
  * **Mensagem auto descritivas** – Os pedidos e respostas devem conter meta-dados que indicam como o conteúdo transmitido deve ser tratado (cabeçalhos para formato, autenticação, etc.);
  * **Utilização de hipermídia para estado da aplicação** – Este pré-requisito é o [menos cumprido por aplicações autointituladas RESTful](http://roy.gbiv.com/untangled/2008/rest-apis-must-be-hypertext-driven): As representações de recursos obtidas em uma aplicação REST devem possuir hiperlinks que permitam a navegação do cliente pelos recursos. Ou seja, diferentemente de arquiteturas baseadas em RPC (Remote Procedure Call), o cliente não deve conhecer previamente as URIs para os recursos da aplicação (apenas a raiz do serviço), sendo que o servidor deve prover links que permita a descoberta dos recursos pelo cliente; não há contrato do serviço e não há garantia que um recurso em uma determinada URI possa estar disponível no futuro;
​* **Sistema em camadas** – A aplicação deve ser construída em camadas sendo que uma camada só pode ver a camada imediatamente abaixo. O objetivo principal deste pré-requisito é garantir que as aplicações sejam escaláveis;
* **Executar código sob demanda** – O cliente deve ser capaz de executar scripts armazenados no servidor de forma a estender as funcionalidades do cliente. Um exemplo disso é a habilidade dos browsers HTTP executarem JavaScripts. Este é o único pré-requisito opcional para arquiteturas REST.
Na teoria, o estilo não depende de nenhum protocolo, mas na prática é sempre implementado utilizando o protocolo HTTP. Portanto, preocupações relacionadas ao formato das URIs (http://servidor.com/lista_de_recursos/chave/), métodos (GET, POST, DELETE, PUT) e códigos de resposta estão relacionadas a utilização do protocolo HTTP de forma correta e não diretamente ao estilo REST. O que leva isso é que o pré-requisito de interface uniforme do REST foi pensado levando em consideração as capacidades do protocolo HTTP.

A World-Wide Web é considerada uma implementação do estilo arquitetural REST. Os browsers são os clientes que requisitam as representações de recursos, retornada no formatos HTML, JPEG, etc. O HTML suporta hipermídia de forma que um cliente não é obrigado a conhecer o caminho de todos os recursos (páginas) da aplicação, mas estes são normalmente apresentados na sua raiz (página inicial). A ideia da transferência representacional de estado está diretamente ligada à hipermídia retornada na junto aos recursos e por isso, uma aplicação não é RESTful se o formato utilizado na representação do recurso não suportar hipermídia.

Pensando na confusão gerada pelo uso do termo REST e suas pré-condições, alguns desenvolvedores estão propondo o uso de um novo termo, chamado [Hypermedia API](http://blog.steveklabnik.com/posts/2012-02-23-rest-is-over), que pode ser aplicado a APIs que cumprem apenas dois pré-requisitos, que são:

 * **Uso correto do protocolo HTTP** – Uso dos métodos, códigos de erro, cabeçalhos e formato de URLs definidos na especificação do protocolo HTTP;
 * **Formato de retorno com suporte a hipermídia** – Existência de hiperlinks que permitam a navegação pelo cliente pelas representações dos recursos, não existência de contrato da API, etc. Um formato que contempla este requisito e está cada vez mais utilizado por APIs hipermídia é o HAL que utiliza como base o JSON e XML.
Com a simplificação dos pré-requisitos, espera-se a diminuição da confusão em torno do termo REST, além da disseminação do conceito de hipermídia, ainda pouco utilizado pelos desenvolvedores de APIs.

**Referências:**

 * http://blog.steveklabnik.com/posts/2012-02-23-rest-is-over
 * http://2beards.net/2012/03/what-the-hell-is-a-hypermedia-api-and-why-should-i-care/
 * http://kellabyte.com/2011/09/04/clarifying-rest/
 * http://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm
 * http://blog.steveklabnik.com/posts/2011-07-03-nobody-understands-rest-or-http
 * http://roy.gbiv.com/untangled/2008/rest-apis-must-be-hypertext-driven​
