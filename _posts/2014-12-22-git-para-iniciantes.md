---
layout: post
title: Git para iniciantes
---

# Introdução

## O que é?

Git é um sistema open source para controle de versão distribuído e gerenciamento de código fonte.
Distribuido significa que cada máquina terá uma cópia de todo o repositório git e este poderá apontar para um repositório central.

Abaixo um exemplo de repositório central (como no TFS)

![CSV Centralizado](http://i.stack.imgur.com/eqmGk.png)

Com o Git o modelo seria este:

![CSV Descentralizado](http://i.stack.imgur.com/9IW5z.png)

# Instalação

A instalação é bem simples, baixe e instale o [MSysGit](https://msysgit.github.io/).
Após a instalação você pode validar a instalação acessando o prompt de comando e digitando `git --version` a versão deve ser exibida logo abaixo.

![Git version](http://i.imgur.com/MLlGFEm.png)

Caso você encontre prolemas na instalação, no [link oficial](https://github.com/msysgit/msysgit/wiki/InstallMSysGit#if-netinstaller-fails-for-you) tem algumas dicas.


# Como funciona?

Quando que você clona uma repositório, o git baixa os arquivos e cria uma cópia da base de dados em sua máquina, como tudo no git  tem seu checksum calculado antes que seja armazenado

## Clonando um repositório

Para clonar um repositório basta utilizar o comando git clone. O comando tem o seguinte formato:

    git clone [url do repositório]
    
Segue um exemplo de como clonar um repositório (no caso estamos criando este repositório):  
Observer que temos mais um parâmetro no comando clone "Git example", esse parâmetro é o nome que você deseja que a pasta raiz do repositório tenha, quando não informado esse parâmetro ele usa o último caminho(path) da url como nome da pasta raiz.  
No caso do TFS, ele irá pedir a suas credencias, caso ocorra falha na autenticação, pode ser que seja necessário habilitar o login secundário no tfs.

![Como clonar um repositório](https://curupira.visualstudio.com/DefaultCollection/Git%20Example/_api/_versioncontrol/itemContent?repositoryId=e9d05324-fa0d-4a9f-ba4d-4e6507c2bb85&path=%2Fgit_clone.png&version=GBmaster&contentOnly=true&__v=5 "Clonando repositório")


# Git e TFS

Para trabalhar com o git no TFS é Fácil, basta selecionar o GIT como controle de versão, quando criar um novo projeto.  
Atualmente não é possível alterar um repositório GIT para TFS ou vice-versa, ou seja para migrar um repositório é necessário criar um novo projeto.


![Criar projeto tfs git](https://curupira.visualstudio.com/DefaultCollection/Git%20Example/_api/_versioncontrol/itemContent?repositoryId=e9d05324-fa0d-4a9f-ba4d-4e6507c2bb85&path=%2Fgit_project_tfs.png&version=GBmaster&contentOnly=true&__v=5 "Criando projetos TFS com git")

 

# Referencias
[Introducao ao git conceitos basicos](http://www.borges-solutions.com/introducao-ao-git-conceitos-basicos/)

# Materiais
 * [Learn Git Branching](http://pcottle.github.io/learnGitBranching/)
 * [Try Git](https://try.github.io/levels/1/challenges/1)
 * [Try Git on CodeSchool](https://www.codeschool.com/courses/try-git)
 * [Git in 5 minutes](http://classic.scottr.org/presentations/git-in-5-minutes/)
