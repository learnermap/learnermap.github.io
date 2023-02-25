---
layout: post
title: "Lógica de Programação"
categories: programming
author:
- Luciano
published: true
---

- [Aprendendo Lógica de Programação](#aprendendo-lógica-de-programação)
- [Meu repositório](#meu-repositório)
- [Scripts](#scripts)
  - [Tags e sintaxe](#tags-e-sintaxe)
  - [Saída e concatenação](#saída-e-concatenação)
- [Referências](#referências)

## Aprendendo Lógica de Programação

Lógica de programação é a aplicação do conceito da 
[lógica](https://en.wikipedia.org/wiki/Logic) no desenvolvimento de sistemas.

Por esse motivo, esse é o ponto de partida para quem deseja estudar programação,
pois é a partir do raciocínio lógico que será possível desenvolver sistemas para 
qualquer ambiente, utilizando qualquer linguagem de programação.

São inúmeras as abordagem utilizadas nos cursos de linguagem de programação, mas
geralmente todas possuem alguns tópicos em comum, sendo eles:

- Conceitos sobre algoritmos;
  - Variáveis;
  - Operadores;
  - Estruturas de Controle;
    - Decisão e Repetição;
- Estruturas de Dados;
  - Vetores, Listas, Filas, Pilhas e Árvores.

Alguns cursos, percorrem esse caminho utilizando uma linguagem de programação
específica, outros utilizam algo mais genérico como um 
[pseudocódigo](https://pt.wikipedia.org/wiki/Pseudoc%C3%B3digo).

## Meu repositório

Estou subindo minhas notas de estudos e códigos no repositório 
[learning-logic](https://github.com/learnermap/learning-logic).

Como não estou obedecendo uma sequência rígida no meu roadmap, estarei 
atualizando os códigos com um certo espaço de tempo.

É isso.

## Scripts

Em meus estudos, estou tentando escrever um script para cada conceito estudado, a fim de aplicar a teoria em algo mais prático.

### Tags e sintaxe

Para iniciar os estudos de lógica de programação, não é necessário programas complexos. Um computador com um navegador já tem tudo que é preciso.

Em meus exemplos, utilizarei Javascript (JS) para codificar os conceitos básicos. Desta forma, não será preciso um ambiente de desenvolvimento complexo.

Nesse primeiro exemplo, teste o início do desenvolvimento de scritps utilizando HTML/JS. _Não vou chamar de programa por razões práticas_.

Começamos por entender que uma linguagem de programação deve seguir uma sintaxe previamente definida. No caso do HTML, uma linguagem de marcação, é a mesma ideia. 

O HTML possui tags que irão envolver o texto puro, traduzindo ao navegador a estrutura que desejamos. 

O JS, manipula essa tags, incorporando ação ao texto inicialmente estático.

O HTML abaixo, escreve um título na tela e o script JS exibe uma caixa de alerta quando a página é carregada.

```html
<!-- marcação html -->
<html>
  <head>
    <meta charset="UTF-8">
    <link rel="icon" href="data:,">
  </head>
  <body>
      <h1>Learning Logic with JS</h1>
      <!-- Script JS -->    
      <script type="text/javascript">
          alert("Lorem ipsum dolor, sit amet consectetur adipisicing elit.");
      </script>
  </body>
</html>
```

> [Tags & Syntax](https://learnermap.github.io/learning-logic/logic-01/codes/01_tags_syntax.html)

### Saída e concatenação

Um sistema computacional é composto basicamente por entrada + processamento + saída. Ou seja, 
independente da forma, a saída dos dados é uma etapa muito importante.

Nesse exemplo, demonstro uma forma de saída dos dados utilizando JS, utilizando o método `write` do objeto
`document`.

Em seguida, um exemplo de concatenação em JS. Veja que a ordem dos operadores influencia no resultado.


```html
<html>
    <meta charset="UTF-8">
    <link rel="icon" href="data:,">
<body>
    <h1>Learning Logic with JS</h1> 
    <p>
        Ways of display data to user.
        <ul>
            <li>alert</li>
            <li>console</li>
            <li>write</li>
        </ul>
    </p>
    <script type="text/javascript">
        alert("Lorem ipsum dolor, sit amet consectetur adipisicing elit.");
        console.log("Lorem ipsum dolor, sit amet consectetur adipisicing elit.");
        document.write("Lorem ipsum dolor, sit amet consectetur adipisicing elit.");

        document.write("<br>")
        document.write("<br>")
        document.write("Total: " + 2 + 3);
        document.write("<br>")
        document.write("Total: " + (2 + 3));
        document.write("<br>")
        document.write("Total: " + (2 + 3 * 5));
        document.write("<br>")
        document.write("Total: " + ((2 + 3) * 5));
        document.write("<br>")
    </script>
</body>
</html>
``` 

> [Output & Concatenation](https://learnermap.github.io/learning-logic/logic-01/codes/02_outputs_concatenation.html)

## Referências

Para ser objetivo e tentar manter o foco, reduzi drasticamente a quantidade de 
referências. Porém, cada uma delas tem bastante conteúdo e em muitos momentos se
sobrepõem. 
Desta forma, podem ser consultadas de maneira complementar, utilizando-as para
compor seu roadmap.

- **Lógica de Programação e Estruturas de Dados**: livro dos autores Sandra Puga
e Gerson Risseti, que aborda todos os temas citados acima, demonstrando soluções
com pseudocódigo e Java.

- **Trilha de Lógica de Programação na Alura**: grupo de cursos de Lógica de 
Programação, utilizando Javascript (JS).

- **Algoritmos em Javascript e Estruturas de Dados**: Esse curso já tem um foco 
maior em JS mas também em lógica de programação, abordando temas importantes 
como estruturas de dados e algoritmos, além de outros pontos mais avançados da 
linguagem.

O livro é uma referência importante pois traz scripts em pseudocódigo, o que 
permite transpor soluções para quaisquer outras linguagens. 

Os cursos, utilizam JS como base para o ensino dos conceitos. Isso facilita o 
aprendizado ao iniciante, pois não é preciso configurar ambiente algum, já que 
para rodar JS é necessário somente um navegador web.