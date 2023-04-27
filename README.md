# Código

Meu blog Pessoal：<https://alexyucra.github.io/blog/>，seja Bem-Vindo。

## Visão geral

<!-- vim-markdown-toc GFM -->

- [Código](#código)
  - [Visão geral](#visão-geral)
  - [Visualização](#visualização)
  - [Como usar](#como-usar)
  - [Trabalhando com documentação](#trabalhando-com-documentação)
  - [experiência e pensamento](#experiência-e-pensamento)
  - [Contate-me](#contate-me)
  - [Obrigado!](#obrigado)

<!-- vim-markdown-toc -->

## Visualização

**[Visitar blog](https://alexyucra.github.io/blog)**

![screenshot home](https://alexyucra.github.io/blog/assets/images/screenshots/home.png)

## Como usar

Depois de bifurcar este projeto, há algumas coisas que precisam ser feitas para que sua página funcione "corretamente".

1. Defina o nome do projeto e a ramificação corretamente.

   De acordo com o GitHub Pages, o branch master de voce pode criar um projeto chamado `username.github.io`.

2. Modifique o nome de domínio.

   Se você precisar vincular seu próprio nome de domínio, modifique o conteúdo do arquivo CNAME e consulte [configurando domínios personalizados](https://docs.github.com/cn/pages/configuring-a-custom-domain-for-your-github-pages-site) para sites do GitHub Pages; se você não precisar vincular seu próprio nome de domínio, exclua o arquivo CNAME.

3. Altere a configuração.

   A configuração do site fica basicamente concentrada no arquivo `_config.yml`, mude as partes relacionadas às informações pessoais pelas suas, como url do site, título, legenda e configuração de módulos de comentários de terceiros.

   **Módulo de comentários:** atualmente suporta disqus, gitment, gitalk, enunciados, beaudar e giscus, basta escolher um deles, e giscus é recomendado. Seus respectivos links do guia de configuração oficial são postados na seção Comentários do arquivo `_config.yml`, consulte a configuração do guia oficial.

   **Nota:** Se você usa disqus, porque a política de manipulação de nomes de usuário e lista de permissões de nomes de domínio do disqus é falha, certifique-se de modificar o disqus.username para o seu próprio, caso contrário, deixe este campo em branco. `disqus.username`.

4. Excluir meus artigos e fotos.

   Exceto pelo arquivo `template.md` nas pastas a seguir, você pode excluir todos eles e adicionar seu próprio conteúdo.

   * Na pasta _posts estão minhas postagens de blog publicadas.
   * Na pasta _drafts estão minhas postagens de blog não publicadas.
   * Na pasta _wiki estão minhas páginas wiki publicadas.
   * Na pasta _fragments estão trechos dos meus artigos publicados.
   * A pasta de imagens contém imagens usadas em meus artigos e páginas.

5. Modifique a página "Sobre".

   O conteúdo do arquivo pages/about.md corresponde à página "Sobre" do site. O conteúdo nele é principalmente pessoal. Substitua-os por suas próprias informações, incluindo os dados nos arquivos `skills.yml` e `social.yml` em o diretório _data.

   Para a configuração do conteúdo em skills.yml e social.yml, consulte:[Significado do conteúdo do arquivo yml no directorio _data](https://mazhuang.org/2020/05/03/blog-template-qna/#_data-%E7%9B%AE%E5%BD%95%E4%B8%8B%E7%9A%84-yml-%E6%96%87%E4%BB%B6%E5%86%85%E5%AE%B9%E5%90%AB%E4%B9%89)。

## Trabalhando com documentação

- Como visualizar localmente, consulte [Setting up your Pages site locally with Jekyll](https://help.github.com/articles/setting-up-your-pages-site-locally-with-jekyll/)。

## experiência e pensamento

* Evite frases longas que são difíceis de quebrar e entender. Se você não conseguir dividi-las em várias frases curtas, isso significa que o entendimento em seu cérebro não está claro.

## Contate-me

Se você tiver alguma sugestão para o modelo ou conteúdo deste blog, pode entrar em contato comigo através do [Issues]([3])。

## Obrigado!

Repositorio traducido por [Alex Yucra](https://alexyucra.github.io/blog/)

[1]: https://github.com/mzlogin/chinese-copywriting-guidelines
[2]: https://help.github.com/articles/setting-up-your-pages-site-locally-with-jekyll/
[3]: https://github.com/mzlogin/mzlogin.github.io/issues/2
