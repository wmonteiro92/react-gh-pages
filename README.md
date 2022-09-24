# Fazendo o deploy de um React App* (criado com o create-react-app) no GitHub Pages

\* criado a partir do `create-react-app`

# Introdução

Este tutorial ([traduzido do inglês do guia escrito por @gitname](https://github.com/gitname/react-gh-pages)) mostra como você pode fazer o deploy da sua aplicação escrita em React usando o GitHub Pages.

Dessa forma, o primeiro passo será criar um React app. Para este tutorial usaremos o [`create-react-app`](https://create-react-app.dev/), o qual é uma ferramenta que os desenvolvedores podem utilizar para usar e criar um React app do zero. Para fazer o deploy deste app usaremos o [`gh-pages`](https://github.com/tschaub/gh-pages), que é um pacote do npm que as pessoas podem utilizar para fazer o deploy no [GitHub Pages](https://docs.github.com/pt/pages/getting-started-with-github-pages/about-github-pages), que é um serviço de hospedagem web gratuito do próprio GitHub.

Se você seguir os passos deste tutorial deverá ter no final um React app propriamente hospedado no GitHub Pages, e que você terá toda a liberdade para customizar como quiser.

# Tutorial

## Pré-requisitos

1. Que o [node e npm](https://nodejs.org/pt-br/download/) estejam instalados. As versões que estarão sendo usadas neste tutorial são:

    ```shell
    $ node --version
    v16.13.2

    $ npm --version
    8.1.2
    ```
    > Ao instalar o npm você terá acesso a dois comandos adicionais dentro do prompt/terminal do seu computador: o `npm` e o `npx`. Ambos serão usados neste tutorial.

2. Que o [git](https://git-scm.com/book/pt-br/v2/Começando-Instalando-o-Git) esteja instalado. Aqui está a versão utilizada por este tutorial:

    ```shell
    $ git --version
    git version 2.29.1.windows.1
    ```

3. Uma conta no [GitHub](https://github.com/signup). :octocat:

## Passo-a-passo

### 1. Crie um repositório **vazio** no GitHub

1. Faça login na sua conta do GitHub.
2. Visite o formulário para [criar um novo repositório](https://github.com/new).
3. Preencha o formulário com as seguintes informações:
    - **Repository name:** preencha com o nome que preferir\*.

        > \* Para um [site de projeto](https://pages.github.com/#project-site), você pode preencher qualquer nome que quiser. Para um [site de usuário](https://pages.github.com/#user-site), o GitHub [requere](https://docs.github.com/pt/pages/getting-started-with-github-pages/about-github-pages#tipos-de-site-do-github-pages) que o nome do repositório siga o seguinte formato: `{nome do usuário}.github.io` (ex.: `wmonteiro92.github.io`)
        
        > O nome que você informar aparecerá em alguns lugares: (a) nas referências ao repositório dentro de vários lugares do GitHub, (b) na URL do repositório, e (c) na URL do React app disponibilizado ("deployado").

        > Neste tutorial faremos o deploy de um React app como um *site de projeto*.

        Dessa forma, informarei como o nome do repositório para este tutorial: `react-gh-pages`
        
   - **Repository privacy:** Selecione _Public_ (ou _Private_\*).

        > \* Para usuários do [GitHub Free](https://docs.github.com/pt/get-started/learning-about-github/githubs-products#github-free-para-contas-pessoais) você é obrigado a escolher o _Public_ se quiser usar o GitHub Pages. Já os usuários do [GitHub Pro](https://docs.github.com/pt/get-started/learning-about-github/githubs-products#github-pro) e demais usuários que pagam pelo GitHub podem escolher tanto o _Public_ como o _Private_ para que façam uso do GitHub Pages.

        Dessa forma, escolherei o _Public_ para este tutorial.

   - **Initialize repository:** pode deixar todas as caixas desmarcadas.

        > Isto fará com que o GitHub crie um repositório totalmente vazio ao invés de deixá-lo já pré-populado com algumas páginas como, por exemplo, o `README.md`, `.gitignore`, e o arquivo de `LICENSE`.
4. Clique em `Create repository`.

Agora, temos em mãos um repositório vazio dentro da sua conta do GitHub e com o nome e nível de privacidade que você especificou.

### 2. Criando um React app

1. Crie um React app chamado `my-app`:

    > Se você precisar de um nome que seja diferente de `my-app` (ex.: `web-ui`), você pode fazê-lo ao substituir todas as menções/vezes em que o texto `my-app` aparece neste tutorial pelo nome que você quer usar (ex.: toda vez que falarmos de `my-app` você substituirá pelo `web-ui` ou qualquer outro nome da sua preferência).
  
    ```shell
    $ npx create-react-app my-app
    ```

    > Este comando irá criar um React app feito em JavaScript em seu computador. Se ao invés de usar o JavaScript você preferir usar [TypeScript](https://create-react-app.dev/docs/adding-typescript/#installation), rode o comando abaixo ao invés do comando que acabamos de mencionar acima:
    
    > ```shell
    > $ npx create-react-app my-app --template typescript
    > ```

    Com isso, você terá uma nova pasta chamada de `my-app` e que terá o código-fonte do seu React app.

    > In addition to containing the source code of the React app, that folder is also a Git repository. That characteristic of the folder will come into play in Step 6.    

2. Enter the newly-created folder:
  
    ```shell
    $ cd my-app
    ```

At this point, there is a React app on your computer and you are in the folder that contains its source code. All of the remaining commands shown in this tutorial can be run from that folder.

### 3. Install the `gh-pages` npm package

1. Install the [`gh-pages`](https://github.com/tschaub/gh-pages) npm package and designate it as a [development dependency](https://nodejs.dev/learn/npm-dependencies-and-devdependencies):
 
    ```shell
    $ npm install gh-pages --save-dev
    ```

At this point, the `gh-pages` npm package is installed on your computer and the React app's dependence upon it is documented in the React app's `package.json` file.

### 4. Add a `homepage` property to the `package.json` file

1. Open the `package.json` file in a text editor.
   
    ```shell
    $ vi package.json
    ```

    > In this tutorial, the text editor I'll be using is [vi](https://www.vim.org/). You can use any text editor you want; for example, [Visual Studio Code](https://code.visualstudio.com/).

2. Add a `homepage` property in this format\*: `https://{username}.github.io/{repo-name}`

    > \* For a [project site](https://pages.github.com/#project-site), that's the format. For a [user site](https://pages.github.com/#user-site), the format is: `https://{username}.github.io`. You can read more about the `homepage` property in the ["GitHub Pages" section](https://create-react-app.dev/docs/deployment/#github-pages) of the `create-react-app` documentation.

    ```diff
    {
      "name": "my-app",
      "version": "0.1.0",
    + "homepage": "https://gitname.github.io/react-gh-pages",
      "private": true,
    ```
At this point, the React app's `package.json` file includes a property named `homepage`.

### 5. Add deployment scripts to the `package.json` file

1. Open the `package.json` file in a text editor (if it isn't already open in one).
   
    ```shell
    $ vi package.json
    ```

2. Add a `predeploy` property and a `deploy` property to the `scripts` object:

    ```diff
    "scripts": {
    +   "predeploy": "npm run build",
    +   "deploy": "gh-pages -d build",
        "start": "react-scripts start",
        "build": "react-scripts build",
    ```

At this point, the  React app's `package.json` file includes deployment scripts.

### 6. Add a "remote" that points to the GitHub repository

1. Add a "[remote](https://git-scm.com/docs/git-remote)" to the local Git repository.

    You can do that by issuing a command in this format: 
    
    ```shell
    $ git remote add origin https://github.com/{username}/{repo-name}.git
    ```
    
    To customize that command for your situation, replace `{username}` with your GitHub username and replace `{repo-name}` with the name of the GitHub repository you created in Step 1.

    In my case, I'll run:

    ```shell
    $ git remote add origin https://github.com/gitname/react-gh-pages.git
    ```

    > That command tells Git where I want it to push things whenever I—or the `gh-pages` npm package acting on my behalf—issue the `$ git push` command from within this local Git repository.

At this point, the local repository has a "remote" whose URL points to the GitHub repository you created in Step 1.

### 7. Deploy the React app to GitHub Pages

1. Deploy the React app to GitHub Pages

    ```shell
    $ npm run deploy
    ```

    > That will cause the `predeploy` and `deploy` scripts defined in `package.json` to run.
    >
    > Under the hood, the `predeploy` script will build a distributable version of the React app and store it in a folder named `build`. Then, the `deploy` script will push the contents of that folder to a new commit on the `gh-pages` branch of the GitHub repository, creating that branch if it doesn't already exist.

    > By default, the new commit on the `gh-pages` branch will have a commit message of "Updates". You can [specify a custom commit message](https://github.com/gitname/react-gh-pages/issues/80#issuecomment-1042449820) via the `-m` option, like this:
    > ```shell
    > $ npm run deploy -- -m "Deploy React app to GitHub Pages"
    > ```

    GitHub Pages will automatically detect that a new commit has been added to the `gh-pages` branch of the GitHub repository. Once it detects that, it will begin serving the files that make up that commit — in this case, the distributable version of the React app — to anyone that visits the `homepage` URL you specified in Step 4.

**That's it!** The React app has been deployed to GitHub Pages! :rocket:
    
At this point, the React app is accessible to anyone who visits the `homepage` URL you specified in Step 4. For example, the React app I deployed is accessible at https://gitname.github.io/react-gh-pages.

### 8. (Optional) Store the React app's _source code_ on GitHub

In the previous step, the `gh-pages` npm package pushed the distributable version of the React app to a branch named `gh-pages` in the GitHub repository. However, the _source code_ of the React app is not yet stored on GitHub.

In this step, I'll show you how you can store the source code of the React app on GitHub.

1. Commit the changes you made while you were following this tutorial, to the `master` branch of the local Git repository; then, push that branch up to the `master` branch of the GitHub repository.

    ```shell
    $ git add .
    $ git commit -m "Configure React app for deployment to GitHub Pages"
    $ git push origin master
    ```

    > Recomendamos que você explore o repositório do GitHub neste momento. Ele terá dois branches: `master` e `gh-pages`. O branch `master` terá o código-fonte do React app, e o branch `gh-pages` terá a versão do seu React app que pode ser disponibilizada para consumo pelas pessoas.
    
# Referências

1. [O guia oficial de deploy do `create-react-app`](https://create-react-app.dev/docs/deployment/#github-pages)
2. [GitHub blog: Build and deploy GitHub Pages from any branch](https://github.blog/changelog/2020-09-03-build-and-deploy-github-pages-from-any-branch/)
3. [Preserving the `CNAME` file when using a custom domain](https://github.com/gitname/react-gh-pages/issues/89#issuecomment-1207271670)

# Notas

- Agradecimentos especiais ao GitHub (a empresa) por ter disponibilizado para nós o serviço GitHub Pages gratuitamente.
- E agora é hora de fazer com que o seu `create-react-app` tenha a sua cara, trazendo as suas customizações do jeito que você quiser!
- Este repositório possui dois branches:
    - `master` - o _código-fonte_ do React app
    - `gh-pages` - o React app _feito a partir_ do código-fonte

# Contribuidores da versão original do guia ([em inglês](https://github.com/gitname/react-gh-pages))

Thanks to these people for contributing to the maintenance of this tutorial.

<!--

Template:
---------

<a href="https://github.com/____" target="_blank" title="____">
  <img src="https://github.com/____.png?size=40" height="40" width="40" alt="____" />
</a>

Instructions:
-------------

1. Copy the template and paste it below.
2. Replace the four "____" strings with the contributor's GitHub username.

Note: I specified the avatars using HTML because, when I did so using Markdown,
      only the _custom_ avatars appeared at the size I specified via the URL
      (e.g. 40px squared, for `https://github.com/gitname.png?size=40`);
      the GitHub-generated avatars seemed to ignore the size parameter and,
      instead, appear at their full size (approximately 420px squared).
      By using HTML, I can force _both_ types to appear at 40px squared.

-->

<a href="https://github.com/gitname" target="_blank" title="gitname">
  <img src="https://github.com/gitname.png?size=40" height="40" width="40" alt="gitname" />
</a>
<a href="https://github.com/rhulse" target="_blank" title="rhulse">
  <img src="https://github.com/rhulse.png?size=40" height="40" width="40" alt="rhulse" />
</a>
<a href="https://github.com/AbhishekCode" target="_blank" title="AbhishekCode">
  <img src="https://github.com/AbhishekCode.png?size=40" height="40" width="40" alt="AbhishekCode" />
</a>
<a href="https://github.com/adnjoo" target="_blank" title="adnjoo">
  <img src="https://github.com/adnjoo.png?size=40" height="40" width="40" alt="adnjoo" />
</a>
<a href="https://github.com/thebeatlesphan" target="_blank" title="thebeatlesphan">
  <img src="https://github.com/thebeatlesphan.png?size=40" height="40" width="40" alt="thebeatlesphan" />
</a>
<a href="https://github.com/valerio-pescatori" target="_blank" title="valerio-pescatori">
  <img src="https://github.com/valerio-pescatori.png?size=40" height="40" width="40" alt="valerio-pescatori" />
</a>

This list is maintained manually—for now—and includes (a) each person who submitted a pull request that was eventually merged into `master`, and (b) each person who contributed in a different way (e.g. providing constructive feedback) and who approved of me including them in this list.
