---
layout: post
title: Perguntas frequentes sobre este modelo de blog Perguntas e respostas - Q & A
categories: GitHub
description: Resumo de perguntas e respostas.
keywords: Jekyll, GitHub Pages
topmost: true
---

Resumo de perguntas e respostas.

## Como visualizar localmente

Consulte as instruções oficiais do GitHub:

- [Setting up your Pages site locally with Jekyll](https://help.github.com/articles/setting-up-your-pages-site-locally-with-jekyll/)

## Erro de visualização local: undefined method map for false

```
GitHub Metadata: Failed to open TCP connection to api.github.com:443 (Connection refused - connect(2) for "api.github.com" port 443)
Liquid Exception: undefined method `map' for false:FalseClass Did you mean? tap in /_layouts/page.html
jekyll 3.8.5 | Error:  undefined method `map' for false:FalseClass
Did you mean?  tap
```

``undefined method `map` for false:FalseClass`` Este erro é sempre precedido por `Failed to open TCP connection to api.github.com:443` Aparecendo juntos, é depois de obter o erro de metadados do GitHub, que leva a este erro de frase:

{% raw %}
```liquid
{% assign repos = site.github.public_repositories | sort: "stargazers_count" | reverse %}
```
{% endraw %}

Solução:

No modelo, Metadados é usado principalmente nos dois arquivos _includes/sidebar-popular-repo.html e _pages/open-source.md Depois de modificar as condições de julgamento antes da frase acima, o problema é resolvido.

{% raw %}
```liquid
{% if site.github.public_repositories != null %}
```
{% endraw %}

alterado para

{% raw %}
```liquid
{% if site.github.public_repositories != false %}
```
{% endraw %}

O código mais recente do modelo foi modificado.

## Suporta fluxogramas de desenho, diagramas de sequência, sereia e MathJax

apoiar. Como os arquivos importados relativamente grandes podem afetar a velocidade de carregamento, ele não é habilitado para todos os arquivos por padrão. Você precisa adicionar uma declaração no Front Matter do arquivo que deseja abrir:

```yaml
---
flow: true
sequence: true
mermaid: true
mathjax: true
---
```

As quatro opções acima correspondem ao suporte de flowchart.js (fluxograma), sequence-diagram.js (diagrama de sequência), sereia e MathJax, respectivamente, e podem ser ativadas conforme necessário, e então você pode desenhar normalmente no texto. Para o efeito de exibição, consulte <https://alexyucra.github.io/blog/wiki/markdown/>，, consulte o arquivo de origem <https://github.com/mzlogin/mzlogin.github.io/blob/master/_wiki/markdown.md> para o método de escrita correspondente.

## Como modificar o estilo de destaque do código

O estilo de realce de código pode ser especificado no arquivo `highlight_theme`. Para obter a lista de nomes de estilos suportados, consulte

- <https://github.com/mzlogin/rouge-themes>

Você pode ver o efeito de visualização de cada estilo na página inicial do projeto.

## Quais idiomas o realce de código oferece suporte?

Consulte <https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers> para obter a lista de idiomas ou você mesmo pode executar rougify listo comando para visualizar a lista mais recente.

## Gitalk solicita erro 403 após login autorizado

A mensagem de erro específica que você vê é `Error: Requrest failed with status code 403`。

Para uma discussão detalhada, consulte <https://github.com/gitalk/gitalk/issues/429> . Este problema também menciona a causa e a solução do problema: atualize o Gitalk para a versão 1.7.2 ou crie um serviço de proxy CORS por você mesmo e adicionar configuração proxy: `proxy: '<seu_endereço_proxy>'`。

Se você estiver usando o código mais recente deste modelo, não precisa fazer nada, a versão mais recente será referenciada automaticamente. Se ainda não funcionar depois de atualizar repetidamente, você precisará atualizar seu cache local visitando os dois links a seguir:

- <https://purge.jsdelivr.net/npm/gitalk@1/dist/gitalk.min.js>
- <https://cdn.jsdelivr.net/npm/gitalk@1/dist/gitalk.min.js?v=1.7.2>

## A parte da caixa de comentários do Gitalk solicita o erro: não encontrado

Há um prompt na página `Error: Not Found.`，e o console do navegador pode ver a mensagem de erro `GET https://api.github.com/repos/<user>/<repo>/issues?labels=gitment,xxx 404`。

Nesse caso, o item de configuração gitalk.repo em _config.yml não foi preenchido corretamente. Este item de configuração é para preencher o nome de um depósito de código que usa seus problemas para armazenar o conteúdo do comentário. Verifique se o depósito de código correspondente ao nome preenchido existe. Se você quiser evitar problemas, pode preencher diretamente o nome do depósito correspondente ao código-fonte do blog, por exemplo `<user>.github.io`。

## Modificar a imagem do código QR

A seção components.qrcode em _config.yml é usada para controlar o código QR.

Não exibir o código QR: altere components.qrcode.enabled para falso.

Substitua a imagem do código QR: substitua o arquivo assets/images/qrcode.jpg.

## O significado do conteúdo do arquivo yml no diretório _data

O conteúdo do arquivo skills.yml corresponde às palavras-chave da habilidade na página "Sobre"

![](/images/posts/template/skills.yml.png)

O conteúdo do arquivo social.yml corresponde ao conteúdo do "Contato" na página "Sobre" .

![](/images/posts/template/social.yml.png)

O conteúdo do arquivo links.yml corresponde ao conteúdo da página "Links" .

![](/images/posts/template/links.yml.png)

[1]: https://mazhuang.org/about/
[2]: https://mazhuang.org/links/
