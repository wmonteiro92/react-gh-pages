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

        > \* Para um [site de projeto](https://pages.github.com/#project-site), você pode preencher qualquer nome que quiser. Para um [site de usuário](https://pages.github.com/#user-site), o GitHub [requere](https://docs.github.com/pt/pages/getting-started-with-github-pages/about-github-pages#tipos-de-site-do-github-pages) que o nome do repositório siga o seguinte formato: `{nome_do_usuário}.github.io` (ex.: `wmonteiro92.github.io`)
        
        > O nome que você informar aparecerá em alguns lugares: (a) nas referências ao repositório dentro de vários lugares do GitHub, (b) na URL do repositório, e (c) na URL do React app disponibilizado ("deployado").

        > Neste tutorial faremos o deploy de um React app como um *site de projeto*.

        Dessa forma, informarei como o nome do repositório para este tutorial: `react-gh-pages`. Você poderá escolher qualquer outro nome, mas precisará substituir todas as menções do `react-gh-pages` nos próximos passos deste tutorial pelo nome que escolher. Por exemplo, se você preferir usar o nome `abacaxi`, substituia todas as menções a `react-gh-pages` nos comandos e operações dos próximos passos deste tutorial por `abacaxi`, beleza?
        
   - **Repository privacy:** Selecione _Public_ (ou _Private_\*).

        > \* Para usuários do [GitHub Free](https://docs.github.com/pt/get-started/learning-about-github/githubs-products#github-free-para-contas-pessoais) você é obrigado a escolher o _Public_ se quiser usar o GitHub Pages. Já os usuários do [GitHub Pro](https://docs.github.com/pt/get-started/learning-about-github/githubs-products#github-pro) e demais usuários que pagam pelo GitHub podem escolher tanto o _Public_ como o _Private_ para que façam uso do GitHub Pages.

        Dessa forma, escolherei o _Public_ para este tutorial.

   - **Initialize repository:** pode deixar todas as caixas desmarcadas.

        > Isto fará com que o GitHub crie um repositório totalmente vazio ao invés de deixá-lo já pré-populado com algumas páginas como, por exemplo, o `README.md`, `.gitignore`, e o arquivo de `LICENSE`.
4. Clique em `Create repository`.

Agora, temos em mãos um repositório vazio dentro da sua conta do GitHub e com o nome e nível de privacidade que você especificou.

### 2. Criando um React app

1. Abra uma janela do terminal (ou prompt de comando) no seu computador. Agora vamos criar um React app chamado `my-app`:

    > Se você precisar de um nome que seja diferente de `my-app` (ex.: `web-ui`), você pode fazê-lo ao substituir todas as menções/vezes em que o texto `my-app` aparece neste tutorial pelo nome que você quer usar (ex.: toda vez que falarmos de `my-app` você substituirá pelo `web-ui` ou qualquer outro nome da sua preferência).
  
    ```shell
    $ npx create-react-app my-app
    ```

    > Este comando irá criar um React app feito em JavaScript em seu computador. Se ao invés de usar o JavaScript você preferir usar [TypeScript](https://create-react-app.dev/docs/adding-typescript/#installation), rode o comando abaixo ao invés do comando que acabamos de mencionar acima:
    
    > ```shell
    > $ npx create-react-app my-app --template typescript
    > ```

    Com isso, você terá uma nova pasta chamada de `my-app` e que terá o código-fonte do seu React app.

    > Além de conter o código-fonte do seu React app, esta pasta também é um repositório em Git. Esta característica adicional da pasta será usada lá no Passo 6, um pouco mais para a frente.

2. Entre na pasta que você acabou de criar:
  
    ```shell
    $ cd my-app
    ```

Neste momento existe um React app dentro do seu computador, e você está dentro da pasta que contém o código-fonte deste React app. **Todos** os próximos passos mostrados neste tutorial serão rodados nesta pasta.

### 3. Instale o pacote npm `gh-pages`

1. Instale o pacote npm [`gh-pages`](https://github.com/tschaub/gh-pages) e o configure como sendo [uma dependência do seu React app](https://nodejs.dev/learn/npm-dependencies-and-devdependencies):
 
    ```shell
    $ npm install gh-pages --save-dev
    ```

Agora, o pacote npm `gh-pages` está instalado no seu computador e ele aparecerá como uma dependência do seu React app lá no arquivo `package.json` (que também está dentro da sua pasta).

### 4. Adicione uma propriedade chamada `homepage` ao seu arquivo `package.json`

1. Abra o arquivo `package.json` em um editor de texto.
   
    ```shell
    $ vi package.json
    ```

    > O comando acima funcionará no Linux ou no Mac porque utiliza o [vi](https://www.vim.org/). Por outro lado, nada impede que você abra este arquivo utilizando outros softwares como, por exemplo, o [Visual Studio Code](https://code.visualstudio.com/). Se você estiver usando o Windows você também poderá abrir este arquivo usando o Visual Studio Code, o bloco de notas, ou qualquer outra aplicação da sua preferência.

2. Adicione a propriedade `homepage` dentro do seu arquivo `package.json` seguindo este formato\*: `https://{nome_do_usuário}.github.io/{nome_do_repositório}`

    > \* Para um [site de projeto](https://pages.github.com/#project-site), este é o formato a ser seguido. Para um [site de usuário](https://pages.github.com/#user-site), o formato a ser seguido é: `https://{nome_do_usuário}.github.io`. Você pode ler mais sobre a propriedade `homepage` na [seção "GitHub Pages"](https://create-react-app.dev/docs/deployment/#github-pages) da documentação do `create-react-app`.

    ```diff
    {
      "name": "my-app",
      "version": "0.1.0",
    + "homepage": "https://wmonteiro92.github.io/react-gh-pages",
      "private": true,
    ```
Ao salvar as modificações você deverá ter no arquivo `package.json` do seu React app uma nova propriedade chamada `homepage` e configurada para o *seu* usuário.

### 5. Adicione os scripts de deploy no arquivo `package.json`

1. Abra novamente o arquivo `package.json` no editor de texto (isto se ele já não estiver aberto).
   
    ```shell
    $ vi package.json
    ```

2. Adicione agora duas novas propriedades: uma chamada de `predeploy` e a outra chamada de `deploy`. Ambas ficarão dentro do objeto `scripts`:

    ```diff
    "scripts": {
    +   "predeploy": "npm run build",
    +   "deploy": "gh-pages -d build",
        "start": "react-scripts start",
        "build": "react-scripts build",
    ```

Ao salvar o seu arquivo `package.json` você terá incluído os scripts de deploy do seu React app. Isto permitirá que o conteúdo do seu React app seja corretamente disponibilizado no Github Pages.

### 6. Adicione um "remote" que aponta para o seu repositório do GitHub

1. Adicione um "[remote](https://git-scm.com/docs/git-remote/pt_BR)" ao seu repositório local do Git.

    Você pode fazer isso ao rodar um comando no seguinte formato: 
    
    ```shell
    $ git remote add origin https://github.com/{nome_do_usuário}/{nome_do_repositório}.git
    ```
    
    Customize o comando acima para o seu caso específico, substituindo o `{nome_do_usuário}` com o nome do seu usuário do GitHub e o `{nome_do_repositório}` com o nome do repositório que você criou lá no Passo 1.

    Neste caso, eu rodaria assim:

    ```shell
    $ git remote add origin https://github.com/wmonteiro92/react-gh-pages.git
    ```

    > Este comando fará com que o Git entenda que eu quero que ele envie as modificações para o meu repositório no GitHub (faça um `push`) toda vez em que eu ou o pacote npm `gh-pages` façamos um `$ git push` dentro do meu computador.

Aqui, o repositório local terá um "remote" cuja URL aponta para o repositório do GitHub que criamos no Passo 1.

### 7. Fazendo o deploy do React app no GitHub Pages

1. Faça o deploy do React app no GitHub Pages

    ```shell
    $ npm run deploy
    ```

    > Isto fará com que os scripts `predeploy` e `deploy` que definimos anteriormente no arquivo `package.json` sejam executados.
    >
    > Debaixo dos panos, o script `predeploy` irá rodar uma versão distribuível do React app e armazenará em uma pasta chamada `build`. Depois disso, o script `deploy` irá disponibilizar os conteúdos desta pasta em um novo commit no branch `gh-pages` do repositório do Github, criando uma nova branch com este nome caso ela já não exista.

    > Por padrão, o novo commit no branch `gh-pages` terá o texto-padrão "Updates". Você pode [especificar uma mensagem customizada de commit](https://github.com/gitname/react-gh-pages/issues/80#issuecomment-1042449820) usando a opção `-m`, algo como:
    > ```shell
    > $ npm run deploy -- -m "Deploy do React app no GitHub Pages"
    > ```

    O GitHub Pages irá detectar automaticamente que um novo commit foi adicionado ao branch `gh-pages` do nosso repositório do GitHub. Assim que ele detectar isso, irá começar a disponibilizar todos os arquivos que fizeram parte daquele commit -- isto é, a versão distribuível do React app -- para todos que forem visitar a URL de `homepage` que especificamos no Passo 4.

**E isso é tudo, pessoal!** O React app foi disponibilizado com sucesso no GitHub Pages! :rocket:
    
Neste ponto, o seu React app estará acessível a todos os que acessarem a URL do `homepage` que você especificou no Passo 4. Por exemplo, o React app que eu disponibilizaria poderia estar disponível na URL https://wmonteiro92.github.io/react-gh-pages.

### 8. (Opcional) Armazene o _código-fonte_ do seu React app no GitHub

No passo anterior, o pacote npm `gh-pages` enviou ("fez um push") da versão distribuível do React app em um branch chamado `gh-pages` no nosso repositório do GitHub. Contudo, o _código-fonte_ do React app ainda não foi salvo lá.

Este passo demonstrará como fazer isso.

1. Faça um commit das mudanças que você fez enquanto estava seguindo este tutorial para o branch `master`\* do seu repositório Git dentro do seu computador (isto é, local). Depois, faça um push deste branch para o branch `master` no seu repositório do GitHub.

    ```shell
    $ git add .
    $ git commit -m "Configurar o React app para fazer deploy no GitHub Pages"
    $ git push origin master
    ```

    > \* Verifique se o seu repositório não possui um branch chamado `main` ao invés de `master`. Recentemente, o padrão deixou de ser `master` e os novos repositórios passaram a adotar o `main` como padrão. Se este for o seu caso, somente modifique as menções por `master` neste tutorial para usar o `main` em seu lugar.
    >
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
