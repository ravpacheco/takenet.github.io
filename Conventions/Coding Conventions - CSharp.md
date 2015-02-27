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

|Identificador|Notação|Exemplo|  
|Classe|Pascal|AppDomain|