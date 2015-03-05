---
layout: page
title: Como contribuir?
---

O blog é hospedado no github pages e utiliza [Jekyll](http://jekyllrb.com/), um gerador de páginas estáticas.  

Os posts devem ser em [markdown](http://daringfireball.net/projects/markdown/), [neste link](http://takenet.github.io/2012/02/07/example-content/) existem alguns exemplos de elementos que podem ser utilizados.  

Os posts seguem o [formato Jekll](http://jekyllrb.com/docs/posts/) e por padrão devem conter autor, tag(s) e category:

    ---
    layout: post
    title: <title here>
    comments: <True|False>
    tags: <tags here>
    category: <android,.net,ios,web,xamarin,cordova any platform>
    author: <a username in _data/members.yml>
    ---

    <blog post here ...>

Exemplo:

    ---
    layout: post
    title: Sample post
    comments: True
    tags: ionic,framework
    category: cordova
    author: ridermansb
    ---

    the best...

Existem duas formas de contribuir: 

 * Github: Se você tem acesso ao repositório no Github, você pode escrever o post e adicioná-lo na pasta `_posts`
 * Pull Request: Se não tiver acesso ao repositório, basta realizar um fork, adicionar o post (e/ou alterações no blog que julgue necessárias) e fazer um pull request. Este será analizado e se aprovado será publicado as alterações.


