---
title: "Agrupando elementos de um Array em JavaScript"
date: 2022-01-15T16:54:28-03:00
draft: false
tags: ["javascript"]
---

O agrupamento de arrays é uma operação muito comum seja pelo uso de **GROUP BY** em SQL ou funções de map e reduce em [JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript).

<!--more-->

Para exemplificar, vamos considerar uma lista inicial com 20 elementos randômicos:

```javascript
const base = Array.from({length: 20}, () => Math.random().toString(32));
```

O objetivo é gerar a partir da **lista base** grupos menores com até 3 elementos cada. 

Uma maneira é usar um **for loop** para criar um novo **array** com um índice incrementado a cada 3 registros.

{{< gist rafaelbeecker 8f65e9a97252fdb13c57672cd28c90b0 "group-with-for-loop.js" >}}

* `max` representa o número máximo de elementos que cada grupo pode receber.
* `k` irá controlar o incremental que representa um novo grupo criado.
* `data` irá receber os elementos agrupados a partir da lista base. 

Fazendo uma chamada ao método definido acima temos um resultado do tipo:

```javascript
console.log(group(base, 3));

[
    ['0.vhn46inq5lg', '0.iburdhmc3dg', '0.rujpeoj8lc']
    ['0.erfe4to9pa8', '0.n74i08b00cg', '0.4ft9jmeqf18']
    ['0.jcva00gql78', '0.u0b7t4d46o8', '0.3o5ln7plk3g']
    ['0.82k8q0nk7ro', '0.cpjl0sc9ad8', '0.trct341c7so']
    ['0.sljmhmtjbao', '0.08h4g4ppt5o', '0.epg5i8ia2i8']
    ['0.khq5r83ctl8', '0.he575cps7og', '0.d672p37052']
    ['0.sgg6g328hp8', '0.bbe4fbn4he']
]
``` 

Mesmo já tendo atingido o nosso objetivo, podemos ir um pouco mais longe e deixar o nosso algoritmo **mais legal** e **menos legível** ao mesmo tempo :grimacing:

É possível mplementar a lógica de agrupamento usando [array reduce](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce) e compactar a lógica do **for loop** em apenas uma linha.  

{{< gist rafaelbeecker 8f65e9a97252fdb13c57672cd28c90b0 "group-with-reduce.js" >}}

* O reduce é inicializado por um objeto `{k:0, v: []}`
* `k` irá controlar o incremental que representa um novo grupo criado.
* `v` irá receber os elementos agrupados a partir da lista base. 

Executando o processo de novo agora considerando como o resultado sendo um objeto e a lista contida na propriedade `v`:

```javascript
const res = group(base, 3);
console.log(res.v);

[
    ['0.vhn46inq5lg', '0.iburdhmc3dg', '0.rujpeoj8lc']
    ['0.erfe4to9pa8', '0.n74i08b00cg', '0.4ft9jmeqf18']
    ['0.jcva00gql78', '0.u0b7t4d46o8', '0.3o5ln7plk3g']
    ['0.82k8q0nk7ro', '0.cpjl0sc9ad8', '0.trct341c7so']
    ['0.sljmhmtjbao', '0.08h4g4ppt5o', '0.epg5i8ia2i8']
    ['0.khq5r83ctl8', '0.he575cps7og', '0.d672p37052']
    ['0.sgg6g328hp8', '0.bbe4fbn4he']
]
``` 

Perde um pouquinho na legibilidade, e muito na manutenibilidade, mas mesmo assim é uma maneira legal de chegar no mesmo resultado :fire: