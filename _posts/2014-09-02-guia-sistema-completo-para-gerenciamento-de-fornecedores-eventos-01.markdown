---
layout: post
title:  "Guia: Sistema completo para gerenciamento de fornecedores/serviços de eventos - Parte #01 de ?"
date:   2014-09-02 11:23:25
categories: guia scg-fornecedores-eventos
author: Leonardo Lima Ribeiro
meta: web arquitetura ideias guia tutorial
tags: web arquitetura ideias guia tutorial
excerpt: >
  É isso mesmo! Estou propondo a vocês criarem um sistema comigo, do zero!
---
É isso mesmo! Estou propondo a vocês criarem um sistema comigo, do zero e terminá-lo sabe-se lá quando (espero
que em poucos meses). A ideia disso é tentar cobrir todos os aspectos da criação de software desde a arquitetura
do projeto, implementação, desenvolvimento do backend, frontend, testes, deployment, geração de app para mobile,
novas iterações de desenvolvimento, melhorias e o que mais for possível. E meu objetivo principal com isso é aprender com
vocês através de debates, novas ideias, qual tecnologia nova está surgindo enquanto estamos tocando o projeto e,
também, o que estamos fazendo de errado que poderíamos melhorar.

Tá, mas o que significa "Gerenciamento de fornecedores/serviços de eventos"? Eu ainda não pensei em um nome para
o site/app e nem me incomodo de alguém "copiar" a ideia e desenvolvê-la mais rápida. Mas seria uma ferramenta
que auxiliaria as pessoas criarem cotações de festas. Em contrapartida, auxiliaria também os fornecedores
e prestadores de serviços a obterem mais clientes, controlarem seus serviços e anunciarem seus produtos.
Segue o cenário:

> Sou um recém-papai e estive numa batalha sem fim para cotar tudo que vou precisar na festa de
1 ano do meu filho. O orçamento, como sempre, é apertado e queremos o mundo. Mas por onde começar a pesquisa?
Bom, esse foi o papel de minha esposa. Ela pesquisava diversos sites, buffets, páginas do facebook etc. É válido dizer que,
pelo próprio facebook, encontramos muitas pessoas que fazem esses tipos de serviços onde não temos certeza de
sua idoneidade. Por fim, tivemos que montar planilhas com preços de todos os serviços, o que poderíamos colocar
e o que deveríamos cortar, e escolher a dedo (com um pouco de sorte e confiança) os prestadores dos serviços.
Não achamos um serviço centralizado e aqueles sites que achamos que poderiam parecer com nossa proposta não eram dos melhores.

Então a minha ideia é, basicamente, criar um sistema onde nós possamos montar pacotes do que vamos precisar para um
evento, selecionar os fornecedores que mais gostamos, baseados no feedback de outros usuários, e enviar cotações.
O exemplo dado foi uma festa de um ano, mas poderia ser um casamento, churrasco, festa de aniversário, festa de
quinze anos, festa empresarial etc. O foco não é o evento em si, mas os serviços que você deseja contratar seja lá
qual for a ocasião! *Eu particularmente usaria o site para procurar por depósitos de bebida! XD*

Para ilustrar ainda mais, segue um exemplo: para uma festa infantil, comum, de um ano de aniversário, precisamos ao menos de
salgadinhos, docinhos, bolo, bebidas, decoração, garçons, brindes e aluguel de um espaço (se você não tiver um salão no
seu prédio). Você tem duas opções:

1. Contratar casas de festas que tem todos esses serviços, ou até mesmo organizações de eventos
que vão no local, mas ambos com pacotes absurdos de caros (eles também poderão se cadastrar no nossos sistema!);
2. Você pode montar planilhas de todos esses serviços separados como depósitos de bebidas, confeitarias, pacotes de
salgadinhos e lanchinhos, ver os portifólios dos fotógrafos ou DJ que mais te agradaram... É um trabalho sem fim,
que exige muita pesquisa e confiança na pessoa que você está contratando. Tirando o fato de que você
pode estar contratando um serviço que no dia do evento irá te deixar na mão e nunca mais você vai achar a pessoa que você
contratou. Eu sei o que é porque estou vivendo isso e, graças a Deus, depois de muita dificuldade, finalmente fechamos
quase tudo e a festa dele será em dezembro.

E agora, com o nosso sistema, teremos a terceira opção:

* Selecionar os serviços que queremos num só site, escolher fornecedores baseados nos preços anunciados, e
avaliações de outros usuários, e solicitar a cotação de todos eles através de um simples clique.

Com isso estaremos ajudando não só os demandantes que querem organizar as festas, mas também os fornecedores: estes terão
um sistema centralizado dos seus produtos e serviços, onde além de terem dados estatísticos de cotações de serviços, terão um
hotsite pra anunciar seu trabalho onde podem até chamar de página pessoal - isso é um recurso que será muito bacana, ainda mais
para fotógrafos, DJs, barmans que até possuem um blog/fanpages para mostrar seus serviços mas não conseguem controlar o que
entra, o que sai, preços, demandas etc. (fiz um benchmark com um amigo DJ e um fotógrafo que deram um feedback superpositivo para
esse projeto). E claro, eles vão ter que fazer um bom serviço para ganharem boas avaliações.

Se a ideia da aplicação final for falha, por qualquer motivo, não teremos perdido nada e, pelo contrário, teremos como experiência
a criação desse monstrinho que não é nada pequeno.

Minha ideia inicial para as próximas partes (podemos alterar, reordenar etc.):

* 2 - Arquitetura de sistemas e organização do fluxo de trabalho/desenvolvimento
* 3 - Controle de versão com Git - Contribuição via Github
* 4 - Regras do negócio, esboçando o core business e serviços
* 5 - IDE de desenvolvimento, Prototipando & TDD (Test driven development)

Não sei quantas partes o guia completo terá e também não vou prometer prazo para finalizar, mas a ideia está lançada! Ainda
não tive ideias para o nome do sistema, por favor contribuam, mandem sugestões de nomes aqui nos comentários! Aliás vou pedir a
contribuição de vocês sempre! Nos vemos no Github a partir da parte 3! :-)
