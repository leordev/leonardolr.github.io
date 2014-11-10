---
layout: post
title:  "Guia: Sistema completo para gerenciamento de fornecedores/serviços de eventos - Parte #03 de ?"
date:   2014-11-10 12:29:25
categories: guia scg-fornecedores-eventos
author: Leonardo Lima Ribeiro
meta: cvs versionamento git backend frontend boilerplate sailsjs html5 angular team version webstorm
tags: cvs versionamento git backend frontend boilerplate sailsjs html5 angular team version webstorm
excerpt: >
  Git é um sistema de controle de versão [...] seria uma ferramenta que nos permite modificar o código repentinamente e termos como verificar o que foi alterado ao longo do tempo, com facilidades no próprio software. Caso contrário, precisaríamos ficar salvando cada versão do código, abrir os códigos fontes e comparar linha a linha para verificar a diferença.
---

Estive muito enrolado nos últimos meses e não conseguia dar prosseguimento nenhum… Juro que pensava no blog todas as noites antes de dormir! Se tornou um pesadelo! Ainda estou enrolado, mas consegui arrumar um tempinho para escrever aqui!

Antes de falar sobre GIT e versionamento, na última parte falei que estava optando entre utilizar o Sailsjs e o Hapi. Optei na utilização do Sailsjs por já possuir alguns recursos prontos onde eu precisaria implementar no Hapi como loggers, autenticação JWT, conexão ao BD, entre outros.
O HAPI é ótimo, não o descartem por isso, mas você precisará implementar alguns recursos adicionais (ou instalar plugins/pacotes) que um bom framework já tem embutido. Então dependendo do objetivo da sua aplicação você pode optar pela utilização de um framework ou não.

Enfim, vamos ver logo o que é esse tal de Git!

Git é um sistema de controle de versão, CVS, do Wikipedia:

O CVS, ou Concurrent Version System (Sistema de Versões Concorrentes) é um sistema de controle de versão que permite que se trabalhe com diversas versões de arquivos organizados em um diretório e localizados local ou remotamente, mantendo-se suas versões antigas e os logs de quem e quando manipulou os arquivos.

Então seria uma ferramenta que nos permite modificar o código continuamente e termos como verificar o que foi alterado ao longo do tempo, com diversas facilidades no próprio software. Caso contrário, precisaríamos ficar salvando cada versão do código, abrir os códigos fontes e comparar linha a linha para verificar a diferença. É uma facilidade e tanto, ainda mais para quem desenvolve em equipe, uma vez que também sabemos quem é o autor de cada modificação, certo?



O exemplo anterior mostra que o bloco em verde foi acrescentado na nova versão de código. Repare que antes o código acabava na linha 53 e, agora na linha 50, foi inserido o atributo vendor. A screen acima foi tirada no WebStorm (IDE de desenvolvimento), utilizando o Git como CVS.

Vamos à prática! (Para isso você só precisará instalar o Git, siga as instruções no site oficial: http://git-scm.com)

Criemos um repositório chamado FestasJaApp:
$ git init FestasJaApp

Repositório nada mais é do que uma pasta que irá servir de armazenamento de todo seu projeto. No Git essa pasta é raíz é chamada de repositório.

Com o comando acima será criada uma pasta vazia, com o nome de FestasJaApp, dentro do local que você digitou esse comando.

Certo, agora vamos criar uma página inicial de teste, chamada index.html e inserimos o seguinte conteúdo dentro:
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title>Título da página</title>
</head>
<body>
<p>Conteúdo inicial</p>
</body>
</html>

Agora salve o arquivo. 

Dentro da mesma pasta do projeto insira o seguinte comando:
$ git status

Com o comando acima conseguimos verificar como está o status atual do nosso repositório. E no status atual temos um repositório vazio (que iniciamos através do comando git init) e um arquivo que ainda não está no repositório chamado index.html.
Como index.html é um arquivo do nosso projeto, queremos que ele seja adicionado no nosso repositório, para isso basta adicionar através do comando abaixo:

$ git add index.html

Se verificarmos o status mais uma vez, veremos que agora nosso arquivo está adicionado ao repositório:

$git status 
On branch master

Initial commit

Changes to be commited:
  (use "git rm --cached <file>..." to unstage)

        new file:    index.html

Bom então agora que nosso repositório já está pronto, com a primeira página, vamos commitar nossa versão zero. Commitar é um termo dado para versionar todo o código que se tem no momento atual. Então como nós criamos nossa página esqueleto, vamos fazer um commit inicial para registrar nosso esqueleto na linha do tempo (no futuro permite voltarmos para versão esqueleto ou começar novos projetos baseados na versão zero, em cima desse esqueleto). Para isso digite o comando abaixo:

$ git commit -am “initial commit, skeleton”

Repare que o que está entre aspas é o comentário das alterações feitas, você pode colocar o que quiser (por boas práticas colocar o comentário no verbo presente). Após esse comando ao verificarmos o status mais uma vez recebemos a seguinte mensagem:
$ git status
On branch master
nothing to commit, working directory clean

Essa mensagem identifica que tudo que está no repositório está fiel à última versão commitada. Se alterarmos o parágrafo <p>Conteúdo inicial</p> para <p>Conteúdo inicial 2</p> e salvarmos o arquivo, ao verificar o status mais uma vez receberemos a seguinte mensagem:

$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")

Então commitando mais uma vez para versionarmos essa pequena alteração:

$ git commit -am "alterar texto de conteúdo"
[master e9f7b0e] alterar texto de conteúdo
 1 file changed, 1 insertion(+), 1 deletion(-)

Verificando o status novamente:
$ git status
On branch master
nothing to commit, working directory clean

Ou seja, analisando todo fluxo até agora, ao criarmos um arquivo e adicionarmos ao repositório, ou alterarmos um arquivo já adicionado, o git identifica que o arquivo é novo/modificado no repositório e as alterações ainda não foram commitadas.  Então após terminarmos todas as alterações, realizamos o commit da versão atual através do comando git commit. 

Portanto um fluxo bastante comum é commitar as alterações feitas para cada funcionalidade/etapa do desenvolvimento do projeto. Se uma etapa levar mais de um dia de codificação é comum commitarmos o que foi feito no final do dia de trabalho. E para os mais precavidos, realizar o commit de todo trabalho feito até os momentos de pausa (almoço, cafés etc.). 

Vamos mudar o título e inserir uma imagem no repositório, segue nosso novo arquivo:
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title>Festas Já - Faça agora a sua festa!</title>
</head>
<body>
<p><img src="logo.png" alt="Festas Ja"/></p>
<p>Faça já sua festa!</p>
</body>
</html>

Certo, agora imagine que temos um arquivo pessoal chamado anotacoes-gerais.txt que queremos inserir nessa pasta, mas que não precise ser adicionado ao repositorio, pois ele tem tarefas pertinentes a você que não concerne ao projeto, algumas senhas suas etc. Se colocar esse arquivo na pasta do repositorio e não fizermos nada, OK. O arquivo não será adicionado ao repositório, mas raramente adicionamos arquivos um a um no repositorio como fizemos no início adicionando o arquivo index.html. Geralmente utilizamos o comando git add . e o ponto representa adicionar todos os arquivos dentro do local que você está. Mas se fizermos isso agora o arquivo anotacoes-gerais.txt também será inserido e nós não queremos isso. 

Bem, vamos verificar como está o repositório até agora:

$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   index.html

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	anotacoes-gerais.txt
	logo.png

no changes added to commit (use "git add" and/or "git commit -a")

Para evitar que o git adicione o arquivo vamos criar um arquivo chamado .gitignore com o seguinte conteúdo:

anotacoes-gerais.txt

Salve o arquivo e verifique o status mais uma vez:
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   index.html

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	.gitignore
	logo.png

no changes added to commit (use "git add" and/or "git commit -a")

Repare que o arquivo .gitignore é reconhecido pelo repositório mas o arquivo anotacoes-gerais.txt não é nem mais verificado pelo git. E era isso que nós queriamos, não tem problema de ter o arquivo .gitignore adicionado ao projeto, ele é muito útil e veremos isso posteriormente. 
Bem, vamos adicionar os arquivos e commitar para termos nossa primeira versão apresentável:

$ git add .
$ git commit -am "página inicial pronta"
[master 3b2bf07] página inicial pronta
 3 files changed, 4 insertions(+), 2 deletions(-)
 create mode 100644 .gitignore
 create mode 100644 logo.png
$ git status
On branch master
nothing to commit, working directory clean

Eu utilizo o IntellijIDEA WebStorm como minha IDE de desenvolvimento, gosto muito dos produtos do JetBrains, substitui o Eclipse por ele e estou muito feliz! Quando eu mando abrir meus projetos, ele já cria uns arquivos ocultos de sistemas dentro da pasta .idea, então como não quero isso no meu repositório já vou adicionar mais uma linha no meu arquivo .gitignore:

anotacoes-gerais.txt
.idea

Agora vou brincar um pouco com o WebStorm para mostrar pra vocês o poder do versionamento. (Tudo isso pode ser feito pela linha de comando do git, Eclipse, ou plugins para sublime text, e até mesmo para o editor que você já está acostumado).

Adicione mais duas linhas no arquivo index.html antes da tag <body>:

<p>Segue mais um novo parágrafo adicionado no webstorm</p>
<p><a href=“new.html”>Nova página</a></p>

Crie um arquivo Teste.html vazio que não irei adicionar ao repositório.

Crie um arquivo new.html com o seguinte conteúdo:
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title>Nova página</title>
</head>
<body>
<p>New!</p>
<p><a href="index.html">Início</a></p>
</body>
</html>

Adicione esse arquivo com o comando:
$ git add new.html

Repare que no sidebar do WebStorm, já me mostra em azul os arquivos modificados, em verde os arquivos novos, cinza os arquivos ignorados pelo .gitignore e vermelho os arquivos que ainda não foram adicionados ao repositório:



Adicione todos os arquivos com git add . e depois git commit -am “novas paginas”

Com isso temos todas as novas alterações versionadas no repositório. Lembra que falamos da comparação de código inicialmente? Vamos analisar o arquivo index.html:

Conseguimos fazer isso facilmente através do botão direito no webstorm:



Clicando com o botão direito mais uma vez no webstorm na primeira versão do arquivo e comparando com a versão atual:





Particularmente eu prefiro trabalhar com um IDE justamente por essas facilidades. Se você preferir visualizar essas diferenças por terminal também é possível através dos comandos git log e git diff!

Perfeito, já montamos nosso repositório inicial e já tivemos 4 versionamentos:

$ git log
commit f0706d9f08ff16a42eb90751a136b21a0ae9d364
Author: Leonardo Ribeiro <leonardolr@globo.com>
Date:   Sun Nov 9 15:03:08 2014 -0200

    novas paginas

commit 3b2bf077f45e7c8a3688afc5713590d083091071
Author: Leonardo Ribeiro <leonardolr@globo.com>
Date:   Sun Nov 9 13:41:51 2014 -0200

    página inicial pronta

commit e9f7b0e4a1d9af437aac7dc2f44c60cde6641412
Author: Leonardo Ribeiro <leonardolr@globo.com>
Date:   Sun Nov 9 13:24:04 2014 -0200

    alterar texto de conteúdo

commit e6c0ffe54017554b8fdfcea59e2b5832d6acdde0
Author: Leonardo Ribeiro <leonardolr@globo.com>
Date:   Sun Nov 9 13:14:25 2014 -0200

    initial commit, skeleton

Agora que tal enviarmos nosso repositório para um “servidor” e ter a possibilidade de outros companheiros de projeto atuarem nesse trabalho? Essa é uma das principais vantagens do Git. O Git trata cada repositório como um servidor! Isso te permite ter diversos backups do seu projetos em diversos locais. 



Bom, a maneira mais fácil de fazer isso é utilizar serviços prontos que tem essa serventia como o GitHub ou o BitBucket. Neste exemplo vamos usar o GitHub e para isso você vai precisar de uma conta lá, senão tiver, crie.

Após criar a conta, no próprio site do GitHub, tem os passos iniciais para criar um novo repositório. Como já temos o repositório criado, vamos apenas enviar para o GitHub, então:
1 - Crie um novo repositório no site do GitHub, nomeando-o de FestasJaApp, com a opção Inicializar repositório com arquivo Readme desmarcada (já temos um repositório, lembra?):


2 - Na pasta do nosso já criado repositório entre com os comandos abaixo:
$ git remote add origin https://github.com/SEU-USUARIO/FestasJaApp.git
$ git push -u origin master

3 - Se você fez tudo certo, ao digitar o segundo comando, irá receber uma solicitação para digitar seu nome de usuario e senha e seus arquivos serão enviados:
Counting objects: 17, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (13/13), done.
Writing objects: 100% (17/17), 17.65 KiB | 0 bytes/s, done.
Total 17 (delta 3), reused 0 (delta 0)
To https://github.com/leonardolr/FestasJaApp.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.

Ao realizar um refresh do repositório na página, conseguimos verificar os arquivos no repositório do github:


Com isso seu repositório já está publicado no GitHub, você pode divulgar para seus companheiros de projeto para que eles possam “clonar” o repositório. Clonar nada mais é que fazer o download do repositório através do comando git clone. Vocês já podem fazer o clone do nosso primeiro repositório pelo comando abaixo:

$ git clone https://github.com/leonardolr/FestasJaApp.git

Repare que o GitHub é um serviço aberto para o público, qualquer um pode clonar seus códigos, abrir Issues (problemas a serem corrigidos), comentar, favoritar (starring) etc.! Isso é o melhor dos mundos para os desenvolvedores de projetos opensources! Se isso não é o que você deseja você pode pagar na sua conta do GitHub para ter seu repositório privado ou então recorrer ao BitBucket que te dá a opção de ter o repositório privado sem custo algum!

Certo, então se você quer compartilhar seu projeto para seu time basta disponibilizar o repositório, dar acesso para os usuários do seu time fazerem commit e solicitar que eles clonem o repositório para iniciar o trabalho.

1 - Na página inicial do repositório clique em Configurações (settings).
2 - Clique em Colaboradores (collaborators).
3 - Digite o nome dos seus parceiros e aperte adicionar colaborador (add collaborator).

E pronto, é só isso, agora seus colaboradores já podem commitar no projeto também!  

Se seu projeto é aberto ao público em geral, você também pode receber contribuições de pessoas desconhecidas que gostaram do seu projeto, eles vão lhe enviar “pull requests” e você decide se aceita as contribuições ou não! Fantástico não?

E se você gostou muito de um projeto e quer começar um trabalho em cima dele? É isso que vamos fazer aqui, através do conceito de “fork”.

O Fork nada mais é que um clone de um projeto mas que será iniciado um novo desenvolvimento em cima desse projeto. Vamos à pratica deste conceito!

Lembra do artigo anterior onde falamos sobre arquitetura de sistemas hexagonal? Temos um Boilerplate perfeito para isso! Boilerplate é um conjunto de esqueletos necessários, prontos para que possamos iniciar nosso projeto. E no github temos diversos boilerplates para que possamos praticar o fork e iniciar um novo projeto! 

Iremos forkar o projeto angular-sailsjs-boilerplate que é constituído de duas partes: Frontend e Backend. No Backend temos o framework sailsjs em cima do Node.Js, ele será responsável pela nossa camada de business logic. Lembra? E no frontend temos um boilerplate baseado em AngularJs, com o Karma para fazermos testes unitários. Com esse setup podemos adicionar novos frontend, seja app nativo para android, app nativo para iOS etc. Basta criarmos novas pastas de frontend que se conectem com nosso backend através de suas APIs (pois é dessa forma que o frontend baseado em AngularJs que já vem no projeto se conecta também). 

Vamos ao fork:
1 - Acesse o repositório original: https://github.com/tarlepp/angular-sailsjs-boilerplate 
2 - Clique no botão Fork, no canto superior direito do site do GitHub
3 - Aguarde até o término do Fork e clique em Configurações (settings), agora mude o nome do repositório para o que deseja, no meu caso mudei para FestasJa, verifique meu repositório forkado aqui: https://github.com/leonardolr/FestasJa

Pronto, agora já temos nosso boilerplate inicial para começarmos a desenvolver o FestasJa (nome improvisado e bem feio por sinal, mas o melhor que tive até agora)!

Para que você veja as funcionalidades desse boilerplate leia o arquivo Readme.md para fazer as instalações necessárias para levantar este aplicativo, que já vem com uns exemplos legais de navegação em um acervo de livros e chat de mensagens também. A única coisa que você deve instalar antes é o Node.Js que pode ser obtido pelo site http://nodejs.org/. Após a instalação do Node você pode executar os comandos de instalação encontrado no Readme.MD normalmente.

O artigo ficou bem extenso mas tentei cobrir o máximo que pude para que vocês possam começar a caminhar com o Git, pois o que foi apresentado não é nem 1% da capacidade da ferramenta! Lembre-se que ainda podemos navegar em versões antigas, mudar de branch, execução de tarefas de deploy após um push no servidor (conhecido como hooks) etc.

Estudem esse boilerplate para que possamos caminhar juntos no próximo artigo! Estudem SailsJs e Angular! 

Segue o resumo dos comandos utilizados no Git hoje:

init - Inicialização de um novo repositório
add . - Adiciona todos os arquivos a partir da pasta que o comando está sendo digitado (ao invés de . pode ser usado o nome do arquivo a ser adicionado)
status - Exibe o status atual de alterações
commit - Efetua o versionamento das alterações atuais no repositório
clone - Faz o download de um repositório
add remote - Adiciona um servidor remoto
push - Envia o commit atual para o servidor remoto especificado
log - Exibe o histórico de modificações no repositório (se digitar o arquivo exibe o histórico de modificações no arquivo)
diff - Exibe as diferenças de código efetuadas no arquivo
rm - Ao contrário do comando Add, remove arquivo do repositório
rm remote - Exclui servidor remoto

Quando estivermos fazendo deploy veremos recursos mais avançados no Git! Lembro também que trabalhando em equipe podem surgir conflitos de alteração em um mesmo arquivo, para isso vocês precisam pesquisar como funciona o Merge do Git.

Espero que tenham gostado e até a próxima!
