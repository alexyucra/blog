---
layout: post
title: Como fazer o deploy no Github pages
categories: [gh-pages, deploy, github]
description: Como fazer o deploy no Github pages
keywords: gh-pages, deploy
---

## Como fazer o deploy no Github pages

Solução sensacional tanto para hospedar projetos pessoais e profissionais, como para hospedar os repositórios do seu portfólio.

O processo é bem simples e exigem poucos passos.

### Prerequisitos

- React
- Git e Github
- Comandos do terminal

>  Pode usar o `yarn` como gerenciador de pacotes do projeto, mas você pode utilizar o `npm` no lugar se desejar.

### passo a passo

1. Crie um projeto React (ou utilize um existente)

Vamos aprender como hospedar sites estáticos criados com Hugo, Next.js ou Gatsby no GitHub Pages!

```
# pode oviar este passo em caso ja tenha outro projeto
yarn create-react-app your-app-name
```

2. Crie um repositório no Github e configure-o ao seu projeto.

adicione a pasta do seu projeto

```
cd your-app-name
git init
git remote add git@github.your_github_name/your-app_name.git
```

> Não esqueça de substituir `your_github_name` e `your-app_name` pelo seu nome e repositorio que você criou.

Depois de criar e armazenar Next.js, Nuxt.js, Gatsby, Hugo, Jekyll ou HTML em um repositório, navegue até a guia de configurações desse repositório.

3. Instale o gh-pages como dependência de desenvolvimento no projeto

```
yarn add -D gh-pages
```

4. Adicione propriedades no package.json

```json
"homepage": "git@github.your_github_name/your-app_name.git",
"scripts": {
    "predeploy": "npm run build",
    "deploy": "gh-pages -d build",
},

```

5. Configure o arquivo de rotas da aplicação

Se seu projeto não tem rotas na aplicação ou se ele não utiliza a biblioteca react-router-dom, você pode pular este passo.

Caso possua, para que a aplicação possa carregar todas as rotas corretamente, adicione no componente BrowserRouter a propriedade basename={process.env.PUBLIC_URL}:

```
<BrouserRouter basename={process.env.PUBLIC_URL}>
//...
</BrouserRouter>
```

6. Dê o comando de deploy

Agora, já estamos preparados para realizar o deploy da sua aplicação. Basta dar o comando:

```
yarn run deploy
```

7. Acesse a sua aplicação

Após o processo de deploy ser concluído, a sua aplicação já estará no ar.

Agora basta acessar https://yourgithubname.github.io/your-app-name substituindo yourgithubname pelo seu nome do github e your-app-name pelo nome do repositório que você criou.

Simples, não?

### o processo detraz dos panos

O build da nossa aplicação e o push deste build para um repositório remoto do github em um branch chamado gh-pages.

O github já é pré-configurado para entender que o conteúdo do branch gh-pages será o conteúdo da página web do repositório.
