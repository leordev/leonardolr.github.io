---
layout: post
title:  "Guia: Sistema completo para gerenciamento de fornecedores/serviços de eventos - Parte #02 de ?"
date:   2014-09-04 12:29:25
categories: guia scg-fornecedores-eventos
author: Leonardo Lima Ribeiro
meta: arquitetura hexagonal apis workflow fluxo backend frontend testes node angular sails hapi sgbd html5 bootstrap ui ux javascript mysql postgres
tags: arquitetura hexagonal apis workflow fluxo backend frontend testes node angular sails hapi sgbd html5 bootstrap ui ux javascript mysql postgres
excerpt: >
  Na segunda parte iremos abordar na parte teórica a arquitetura hexagonal e APIs e também a organização do workflow de desenvolvimento. Na parte prática iremos definir qual o stack adotado ao desenvolvimento do sistema. Vamos lá?!
---

E lá vamos nós! Pretendo seguir o guia e as matérias da seguinte forma: na primeira parte de cada artigo falaremos sobre os aspectos teóricos, alguns exemplos e pesquisas; e na segunda parte aplicamos o que vimos na primeira parte ao SCG(o nosso famoso sistema completo de gerenciamento).

# Teoria: Arquitetura e workflow de desenvolvimento

## Arquitetura do sistema: Arquitetura Hexagonal -> APIs

Um dos maiores problemas das aplicações ao longo dos anos foi a invasão das regras de negócios (business logic) em camadas externas, como por exemplo a interface gráfica (UI) e desta forma a aplicação não consegue ser
testada devidamente. Um exemplo clássico pode ser dado pelo tamanho de campo definido na própria tela e obviamente isso não é relevante para outros programas consumidores que tenham interesse em se conectar com o nosso sistema ou para automatização de testes que poderíamos escrever para rodar em batch.

Com isso, surgiram diversos padrões de projetos para separar cada uma das camadas existentes do core da aplicação. Mesmo assim com o passar do tempo, quando paravam pra ver, já existiam mais regras de negócios em outras camadas externas da aplicação.

Imagine agora que cada funcionalidade da aplicação fosse disponibilizada através de uma interface de aplicação programada (ou, mais conhecido como API - application programmed interface). Por exemplo, uma interface para registro
de usuário e uma outra interface para troca de senha. Começamos aqui a falar de arquitetura hexagonal ou arquitetura de portas e adaptadores, onde cada interface representa uma porta/adaptador que se pluga com qualquer dispositivo.
No nosso exemplo poderíamos registrar o usuário através de um site que se "pluga" ao nosso sistema através do adaptador (API) que estamos disponibilizando. Quem sabe posteriormente o mesmo usuário altera sua senha através do seu celular que também conversa com nossa API.

A ideia aqui é que nossa aplicação tenha o código necessário para atender todas as suas funcionalidades dentro dele mesmo. Essa camada de código é o que chamamos de core, que obrigatoriamente deveria possuir todas as regras de negócio. E não devemos permitir nunca que o código necessário "vaze" para outras camadas ou aplicações. Criamos aqui também o conceito de dentro e fora da aplicação ou _inside/outside application_.

>**A regra que devemos obedecer é que o código interno (inside) não deve nunca sair para a camada externa (outside).**

E dessa forma conseguimos disponibilizar nossa aplicação para qualquer tipo de dispositivo, seja ele um celular, um tablet, um computador, um carro, uma geladeira, um controle etc. A comunicação desses dispositivos com o nosso
aplicativo é feita através das APIs que criamos dentro dele (inside) e estamos disponibilizando pro mundo externo (outside). Alguns exemplos:

* Uma página web é um exemplo de adaptador que mapeia as ações de uma pessoa para chamar a API do nosso aplicativo.
* O "pedômetro" nos celulares são os adaptadores que controlam os movimentos das pessoas para chamar a API dos aplicativos/redes sociais que gravam as atividades físicas do usuário.

Até aqui falamos da visão de coisas do mundo externo que se comunicam com o nosso aplicativo. Mas obviamente também existe o contrário. Lembra que nossos aplicativos possuem bancos de dados que também são outros aplicativos? Então,
da mesma forma que os usuários, outros aplicativos e outros dispositivos se comunicam com nosso aplicativo, o nosso aplicativo deve se comunicar com o mundo externo também. Não deixa de ser interfaces também:

* Os métodos do nosso aplicativo são os adaptadores que executam as regras de negócios para chamar a API do SGBD(Sistema de gerenciamento de Banco de dados: MySQL, Postgres, Oracle, SQL Server etc.).

Isto deve ser desenhado de forma que se o nosso SGBD venha a mudar um dia, por qualquer razão ou decisão tecnológica, nosso aplicativo não precise de nenhuma manutenção para funcionar.

A arquitetura hexagonal, ou de portas e adaptadores, foi desenhada para resolver esses tipos de problemas: uma aplicação que se comunica com o mundo externo através de diversas portas. E talvez o grande "pulo do gato", é que as
pessoas saibam segregar o que faz parte do core e o que faz parte do mundo exterior. A grosso modo uma tela pode parecer que faz parte do core, mas não é. É uma interface que se comunica com o core através de alguma forma. O que estamos sugerindo aqui é que essa forma seja uma API definida que você criou e irá servir tanto para essa tela quanto para qualquer outro dispositivo.

Claro que a ideia do core é ter o business logic mas também é preciso agregar no core alguns aspectos de configurações e serviços. Como a configuração de acesso ao banco de dados e a configuração de como serão disponibilizadas as APIs. E serviços como controle de autenticação, loggers, jobs e quaisquer outras ferramentas relevantes para nossa aplicação, mas que nunca devem impactar o funcionamento do nosso core. Lembre-se:

>**A regra que devemos obedecer é que o código interno (inside) não deve nunca sair para a camada externa (outside).**

Eu costumo pensar que programação é e também não é uma matéria exata, pois requer muita abstração e é por isso que a cada dia surge um novo padrão. Acredite, podemos construir um sistema inteiro num único arquivo PHP! Mas nós estamos estudando e nos atualizando sobre o que há de novo sempre, de modo a criarmos possibilidades de desenvolvimentos mais ágeis, interpretáveis, de fácil manutenção e que podem ser trabalhados por uma equipe (não só a técnica mas também todos os outros stakeholders). E qual dos dois estão corretos? Os dois, ambos funcionam! A diferença é que no último caso você vai construir algo mais aderente a qualquer negócio e mais visado por outras pessoas!

Então todo esse blá-blá-blá se deu com o objetivo de adotarmos a seguinte metodologia:

>**Nosso aplicativo será construído com todas as regras de negócio inside e se comunicará com o mundo externo (telas, web, outros programas etc.) através de interfaces APIs.**

## Organização do workflow de desenvolvimento

Com este conceito de APIs firmado e bem definido, baseado no padrão da arquitetura hexagonal, podemos reparar que uma aplicação operada por usuários basicamente tem no mínimo três pontas: as interfaces de entrada (interfaces gráficas, seja pelo browser, aplicativos mobile etc.); o core da aplicação que irá disponibilizar as APIs e realizar os processamentos das regras de nossa aplicação; e as interfaces de persistência que irão armazenar os nossos dados em bancos. 

Com isso podemos inferir o conceito de frontend e backend. Frontend seria o desenvolvimento das interfaces gráficas que irão se comunicar com a nossa aplicação (que seria o Backend). A partir daqui surgem os conceitos de desenvolvedores frontend e desenvolvedores backend. A grosso modo os desenvolvedores frontend são especializados na manipulação de telas (UI - user interface e UX - user experience) e os backends são especializados na manipulação da lógica do negócio, automatizações e camada de persistência: modelagem das classes necessárias, armazenamento de dados nos BDs etc.

Daí surge um dilema: qual seria o melor workflow de desenvolvimento? Começar pelo frontend, terminá-lo inteiro e depois fazer o backend? Ou o contrário? Finalizar o backend para só depois começar pelo frontend. Veja este trecho, na minha opinião, muito interessante:

> Implementações e especificações devem dançar delicadamente juntos. Você não quer que uma implementação ocorra antes que a especificação esteja completa, pois as pessoas dependem de detalhes da implementação e isso faz parte da especificação. Entretanto, você também não quer que a especificação esteja completa antes da implementação e dos testes feitos pelo autor com esta implementação, pois você precisa de um feedback. É inevitável que haja uma tensão aqui, mas isso é só uma pequena confusão. 
> _Dive Into HTML5, capítulo "Como Chegamos Aqui?", parte i. "Mergulhando" - [http://diveintohtml5.com.br/past.html](http://diveintohtml5.com.br/past.html) acessado em 04/09/2014._

Nesse caso, acredito que o autor esteja se referindo a definição das regras de negócio e especificação das mesmas, contra o desenvolvimento e implantação do software. Mas na minha opinião isso poderia se aplicar também ao desenvolvimento do backend e frontend. Eles "devem dançar delicadamente juntos"! Você acha que poderá definir todos os serviços (APIs) que seu aplicativo deverá disponibilizar sem ter um feedback de algum aplicativo/tela que o está consumindo? Acredito que se você partir dessa forma vários serviços em excesso serão criados, e nunca serão consumidos, e também haverão vários serviços que o nosso frontend irá precisar e que não os teremos previstos. O mesmo serve para o inverso, você poderá construir uma aplicação inteira que irá definir classes e suas respectivas associações fictícias e também consumir APIs fictícias que deverão ser criadas posteriormente no backend, mas que poderiam ser desenhadas de outras formas, seja por inviabilidades técnicas, ou por problemas de performance, quem sabe? Então é por isso que ambos devem dançar juntos!

Ainda como sugestão de desenvolvimento do padrão de arquitetura hexagonal, temos o seguinte fluxo de desenvolvimento:

![Imagem do fluxo](https://cloud.githubusercontent.com/assets/6147142/4151729/8fcc18f6-3448-11e4-9d14-8e6ef64d16f2.gif)

1. Testar a aplicação via **programa batch de testes unitários** em cima de **dados instanciados durante a execução**.
2. Testar a aplicação através de **interface gráfica** em cima de **dados instanciados durante a execução**.
3. Testar a aplicação via **programa batch de testes unitários** em que se comunica com uma **interface que acessa um BD real**.
4. Testar a aplicação através de **interface gráfica** em que se comunica com uma **interface que acessa um BD real**.

Um pequeno glossário:

* **Programa batch de testes unitários:** são bibliotecas/frameworks que testam e validam códigos através de métodos que verificam o valor esperado daquilo que você desenvolveu e o valor retornado da execução. Temos várias ferramentas dessas para qualquer tipo de linguagem como o JUnit para JAVA, Karma para JScript etc. Esses programas também geram relatórios de todos os testes executados.
* **Dados instanciados durante a execução:** são variáveis simples que utilizamos pra simular valores ou podemos criar estruturas Mocks também.
* **Interface que acessa um BD real:** geralmente bibliotecas que acessam o BD como o JDBC no JAVA, por exemplo. Para javascript temos o Waterline e Sequelize também!

Seguindo dessa forma, conseguimos validar com qualidade o core da nossa aplicação antes de disponibilizarmos para qualquer dispositivo ou usuário. E também conseguimos apurar três aspectos fundamentais que vimos até aqui:

1. O programa é funcional para um ser humano que esteja operando qualquer interface que se comunica com a nossa aplicação.
2. Qualquer aplicação ou dispositivo externo consegue operar nosso sistema com sucesso, uma vez que validamos isso através de programas batchs que testaram nossa aplicação.
3. As regras da aplicação se encontram totalmente dentro do nosso app e não "vazou" para a camada externa uma vez que o mesmo que foi apurado na interface gráfica por um humano também foi apurado por um sistema programado.

Bom pessoal, nada do que digo aqui é o correto e o absoluto sendo a única opção para você seguir. Mas é um caminho que você pode seguir que com certeza irá trazer bons resultados e dará certo. Essa é minha interpretação e abstração de como a arquitetura hexagonal pode nos ajudar a implementar nossas aplicações. E minha proposta, desde que iniciei o blog, é estar aberto a debates de todos esses conceitos demonstrados aqui para que nos force a pensar na melhor solução e quem sabe assim não chegamos em comum acordo sobre algo criando até uma coisa nova e melhor? Cada arquitetura e especificação serve melhor para alguém e pior para outros. Como falei, é possível fazer um sistema completo em um arquivo PHP!

Meu artigo foi embasado na [arquitetura hexagonal sugerida por Alistair Cockburn](http://alistair.cockburn.us/Hexagonal+architecture).

# Aplicação ao Sistema completo para gerenciamento de fornecedores/serviços de eventos

Até agora não botamos a mão na massa e também não vai ser dessa vez, por enquanto estamos trabalhando com definições do projeto antes de desenvolvê-lo! Mas juro que na próxima parte já vamos praticar algo! Por agora, a meta é adequar a arquitetura ao nosso sistema e definir quais serão as nossas pontas de interfaces.

Como falei na primeira parte do guia, nosso sistema é um website que irá funcionar em desktop, tablets e celulares. E temos basicamente três atores:

* **Usuários:** os organizadores de festas.
* **Fornecedores:** aqueles que irão anunciar seus serviços.
* **Administradores:** os donos do site que provavelmente terão um painel para moderar conteúdos do site e acompanhar índices.

Sendo assim, precisaremos de um frontend com layout recursivo (tecnologia que se adapta aos dispositivos requeridos: browsers em desktops, tablets e celulares) e de um backend que faça os processamentos necessários persistindo os dados no banco.

Para isso segue o stack que eu adotei:

## Frontend

* **HTML5**: linguagem de marcação interpretada pela maioria dos browsers.
* **Twitter Bootstrap**: framework frontend desenvolvido com HTML, CSS e JS voltado para o desenvolvimento web recursivo com diversas funções já prontas que iremos utilizar em nossos layouts.
* **Angular.js**: framework javascript MVW que nos auxiliará na separação de dados dinâmicos (models) do layout HTML propriamente dito; no processamento de algumas funções dinâmicas em javascript necessárias pelo frontend para tornar a experiência do usuário (UX) e a interface (UI) mais rica; e também facilitar as chamadas de nossas APIs que serão disponibilizadas pelo backend.

## Backend

* **Node.js:** escolhi o node porque ele é muito bom para trabalhar na disponibilização de APIs e também para manter apenas uma linguagem de programação (Javascript) tanto no frontend quanto no backend.
* **HAPI ou Sails.js:** frameworks que nos auxiliam na disponibilização de APIs e possuem diversas funcionalidades já prontas as quais nos permitirá economizar tempo e focar mais em nosso core (não precisaremos desenvolver serviços como autenticação, loggers, roteamento de URLs etc.). Ainda não decidi por qual dos dois eu vou utilizar, mas ambos são excelentes!
* **Waterline:** framework ORM que servirá de interface para persistência de dados.
* **MySQL ou Postgres:** SGBDs gratuitos que servirão de armazenamento de nossos dados. Também não decidi por qual utilizar, mas são os bancos SQL mais populares hoje. Preferi pela não utilização de bancos NoSQL por preferência pessoal mesmo, tenho razões pessoais para não utilizá-los mas não vem ao caso discorrer por aqui.

## Workflow de desenvolvimento

Quanto ao desenvolvimento vou seguir algo bem semelhante ao sugerido por Alistair Cockburn:

1. Desenvolver alguma funcionalidade no backend.
2. Testar os métodos que envolvem essa funcionalidade no backend **utilizando framework de automatização de testes** em cima de **dados instanciados durante a execução**.
3. Desenvolver o frontend relativo a esta funcionalidade.
4. Testar a aplicação através do **frontend desenvolvido** em cima de **dados instanciados durante a execução**.
5. Testar a aplicação **utilizando framework de automatização de testes** se comunicando com a **interface que acessa o banco**.
6. Testar a aplicação através do **frontend desenvolvido** se comunicando com a **interface que acessa o banco**.


## Conclusão

Então eu acho que é só isso povo! Acabou ficando bem extenso e talvez chato por não estarmos praticando nada, mas não tem como fugir. Primeiro temos que saber o que vamos fazer e qual trilha vamos seguir para depois nos adentrarmos de vez! Depois de planejado fica bem mais fácil sabermos como e o que seguir.

Queria solicitar a vocês que fiquem a vontade para escolher o stack da forma que desejar e se estiver me acompanhando poste seu stack e o motivo da escolha, mesmo que não esteja desenvolvendo o sistema do guia, poste seu stack favorito! Também queria dizer e incentivá-los a utilizar bancos NoSQL como o MongoDB ou CouchDB. Não estamos presos a nada, a ideia é evoluir sempre e construir com as ferramentas que mais nos dá prazer!
