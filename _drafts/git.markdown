---
layout: post
title:  "Guia: Sistema completo para gerenciamento de fornecedores/serviços de eventos - Parte #03 de ?"
date:   2014-09-04 12:29:25
categories: guia scg-fornecedores-eventos
author: Leonardo Lima Ribeiro
meta: cvs versionamento team flow 
tags: arquitetura hexagonal apis workflow fluxo backend frontend testes node angular sails hapi sgbd html5 bootstrap ui ux javascript mysql postgres
excerpt: >
  Na segunda parte iremos abordar na parte teórica a arquitetura hexagonal e APIs e também a organização do workflow de desenvolvimento. Na parte prática iremos definir qual o stack adotado ao desenvolvimento do sistema. Vamos lá?!
---

Estive muito enrolado nos últimos dias e não consegui dar prosseguimento... Ainda estou enrolado mas consegui arrumar um tempinho para escrever aqui!

Antes de falar sobre GIT e versionamento, na última parte falei que estava optando entre utilizar o Sailsjs e o Hapi. Optei na utilização do Sailsjs por já ter muitos recursos prontos onde eu precisaria implementar na mão no Hapi como loggers, autenticação JWT, conexão ao BD, entre outros.
O HAPI é ótimo, não o descartem por isso, mas você precisará implementar várias coisas que um bom framework já tem embutido. Então dependendo do objetivo da sua aplicação você pode optar pela utilização de um framework ou não.

Enfim, vamos ver logo o que é esse tal de GIT!
