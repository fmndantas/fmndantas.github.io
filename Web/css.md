[TOC]

# css cheatsheet

## inline styling

```html
<p style="color: red; font-size: 20px;">esse eh um paragrafo com formatacao inline</p>
```

## estilização dentro da tag head

```html
<head>
    <style>
        p {
            color: red;
            font-size: 20px;
        }
    </style>
</head>
```

## estilização com os dois arquivos separados

- o nome do arquivo de formatação é `style.css` e ele está no mesmo diretório que o arquivo html

```html
<head>
    <link href="./style.css" type="text/css" rel="stylesheet">
</head>
```

## seletores

### pelo nome da tag

```css
p { }
h1 { }
```

### pela classe da tag

```html
<p class="brand">this is the brand</p>
```

```css
.brand {
    
}
```

### multiplas classes

```html
<p class="green bold">green and bold text</p>
```

```css
.green {
	color: green;
}

.bold {
	font-weight: bold;
}
```

### pelo id

```html
<p id="large">large text</p>
```

```css
#large {
	font-size: 60px;
}
```

### chaining


```css
/* seleciona as tags h1 com class=special */
h1.special { }

/* seleciona os elementos li que estão em algum outro elemento com class=main-list */
.main-list li { }

/* seleciona os elementos li que estão dentro de uma tag nav */
nav li { }

/* seleciona os elementos com as classes class1 e class2 ao mesmo tempo */
.class1.class2 {}
```

### entidades com mesmo pai e vizinhas no html

```css
/* seleciona os elementos p que sucedem um h1 no html e cujo parente é o mesmo que h1 */
h1 + p { }
```

### múltiplos seletores pra evitar repetição

```css
h1, .menu, p {
    font-family: Georgia;
}
```

###  hierarquia dos seletores

- `id` > `class` > `tag` (`id` sobrepõe `class` que sobrepõe `tag`)
- tentar sempre usar os seletores no sentido `tag` => `id`, combinando as classes criadas

## rulesets comuns (importantes)

```css
h1 {
    font-family: "Courier New";   /* família da fonte */
    font-size: 18px;              /* tamanho da fonte */
    font-weight: bold;            /* quão grossa ou fina a fonte aparenta ser */
    text-align: right;            /* alinhamento do texto com relação ao parente */
    color: red;                   /* cor do texto da tag */
    background-color: blue;       /* cor de fundo da tag */
    opacity: 0.5;                 /* 1 -> opaco, 0 -> transparente */
    background-image: url("path") /* adiciona imagem de fundo */
}
```

###  !important

```css
/* não importa a hierarquia: o que está marcado em !important sempre se sobreporá */
p {
    color: blue !important;
}
```

## box model

![image-20210219195531466](/home/fernando/.config/Typora/typora-user-images/image-20210219195531466.png)

### unidades de medida

```css
/* px -> pixel, é mostrado da mesma forma em todas as telas
    % -> tamanho relativo ao parente */

p {
    width: 10px;
    height: 20%;
}
```



### reset do espaçamento padrão

```css
/* remove margem e padding padrões de todos os elementos html */
* {
    margin: 0;
    padding: 0;
}

/* remove margem e padding padrões de todos os elementos html */
body {
    margin: 0;
    padding: 0;
}
```

### height, width e border

```css
p {
    height: 100px;            /* se ausente, é setado como valor do parente */  
    width: 100px;             /* o mesmo que height */
    min-width: 50px;          /* largura mínima do container */
    max-width: 150px;         /* largura máxima do container */
    min-height: 50px;         /* altura mínima do container */
    max-height: 150px;        /* altura máxima do container */
    border: 10px solid white; /* espessura, estilo e cor */
    border-radius: 5px;       /* raio da borda */
}
```

### padding

```css
/* usado geralmente expandir a cor de background e dar a sensação que o conteúdo não está achatado */
p {
    padding: 20px;                /* todos os lados */
    padding: 20px 20px;           /* cima+baixo e esquerda+direita */
    padding: 20px 20px 20px 20px; /* sentido horário */
}
```

### margin

- `margin` entre elementos verticais consecutivos colapsa (o maior é que dita o espaçamento)
- `margin` entre elementos horizontais consecutivos é somada (a distância entre eles é a soma das margens)

```css
/* usado pra ajustar o tamanho dos containers 
afasta todos os elementos do elemento selecionado */
p {
    margin: 20px;                /* todos os lados */
    margin: 20px 20px;           /* cima+baixo e esquerda+direita */
    margin: 20px 20px 20px 20px; /* sentido horário */
    
    margin: 0 auto;              /* centra elemento no parente */
    width: 200px;                /* mas eh preciso setar a largura */
}
```

### diferença entre padding e margin

com background,

- `padding` aparece (porque é o espaço até a **borda**)
- `margin` não aparece

### overflow

- ocorre quando as dimensões horizontais e verticais de um elementos são maiores que as dimensões de seu parente
- **setado no parente pra fazer efeito nos filhos**

```css
p {
    overflow: hidden|scroll|visible
}
```

### visibilidade

  ```css
p {
    display: none;      /* remove a tag completamente da página */
    visibility: hidden; /* torna a tag invisível, mas mantém o espaço reservado */
}
  ```

### tipos de box model

- `box-sizing` controla qual tipo de box model está sendo usado 

  - `content-box`: `margin`, `padding` e `border` alteram as dimensões de maneira indesejada

  - `border-box`: evita os erros de dimensão que ocorrem com `content-box`
  - as laguras e alturas se mantém constantes
    - `margin`, `padding` e `border` são incluídos de maneira a manterem verdade o ponto anterior

    ```css
    *  {
    box-sizing: border-box; /* default: content-box */
    }
    ```

## posicionamento de elementos no browser

### position

- `static` (default)
- `relative`: especifica a posição do elemento com relação a sua posição `static`
  - usa offset
    - `top`: move elemento para baixo
    - `bottom`: move elemento para cima
    - `left`: move elemento para direita
    - `right`: move elemento para esquerda
- `absolute`: os outros elementos ignoram a presença do elemento absolute e a posição é setada com relação ao parente do elemento
- `fixed`: fixa elemento na página, independentemente da rolagem. útil pra usar com navbar

### z-index

- determina a sensação de profundidade dos elementos na página
- não funciona com `position: absolute`
- usado, por exemplo, pra fazer com que um elemento `position: fixed` cubra todos os outros, quando a rolagem da página acontecer

```css
/* h1 aparece na frente de p, porque seu z-index é maior */
p {
    position: relative;
    z-index: 1;
}

h1 {
    position: relative;
    z-indez: 2;
}
```

### display

- `inline`: box apertado, que só ocupa o espaço necessário. O conteúdo ao redor ocupa a mesma linha que o elemento `inline`. não pode ser modificado pelo css (ex.: `width` e `height` não têm efeito). tags `inline` aparecem lado a lado
- `block`: box com altura necessária para conteúdo, mas com largura igual a todo espaço horizontal disponível. Altura e largura podem ser modificadas
  - `h1` a `h6`, `p`, `div` e `footer` são alguns exemplos

- `inline-block`: combina `inline` com `block`: os elementos podem aparecer ao lado de outros e seus tamanhos são controláveis via css

### float

- afasta o elemento o máximo possível para direita ou para esquerda
- tem que ter largura especificada, ou então se assume 100% de largura e o `float` não funciona
- funciona pra `static` e `relative`

### clear

- determina como um elemento deve se comportar quando ele toca em outro elemento no mesmo container
  - `left`: a borda esquerda não deve tocar em nenhum outro elemento
  - `right`: a borda direita não deve tocar em nenhum outro elemento
  - `both`: as duas bordas não devem tocar em nenhum outro elemento
  - `none`: as duas bordas podem tocar em outros elementos

## layout com flexbox

- não recomendado para fazer o layout de páginas inteiras, mas de elementos individuais ou grupo de elementos

- containers importantes: flex container e flex items

  - todos as tags filhos de um flex container são flex items
  - algumas propriedades são para flex containers, enquanto outras para flex items

- para que um container seja um flex container

  ```css
  p {
      display: flex|inline-flex;
  }
  ```

  - só flex faz o elemento continuar `block` (toma todo espaço horizontal). Os flex items se tornam `inline`
  - `inline-flex` permite que o container se torne `inline`, ou seja, apareça numa mesma linha com outros elementos


### justify-content (main axis)

- alinhamento no main axis dos elementos que compõem uma linha do container
  - `flex-start`: elementos empurrados pra esquerda
  - `flex-end`: elementos empurrados pra direita
  - `center`: elementos se mantém no centro
  - `space-around`: elementos se distribuem pela linha com espaços iguais antes e depois (elementos do meio aparentam estar com dobro de espaço, porque os espaços horizontais se somam)
  - `space-between`: elementos se distribuem pela linha com espaços entre eles iguais, mas SEM espaços antes do primeiro e depois do último 

### align-items (cross axis)

- alinhamento no cross axis dos elementos que compõem uma linha do container
  - `flex-start`: elementos posicionados no topo do parente
  - `flex-end`: elementos posisionados no chão do parente
  - `enter`: elementos posicionados no meio do caminho entre topo e chão
  - `baseline`: o chão de todo conteúdo do container fica alinhado entre si
  - `stretch`: se os elementos não tiverem altura definida, serão esticados do topo ao chão do container

### align-content (cross axis)

- alinhamento (espaçamento) no cross axis ENTRE linhas de um container
- só funciona quando `flex-wrap: wrap`
- aceita mesmos valores que `justify-content`, mais o valor `stretch`, que distribui as linhas de forma que elas tomem todo o espaço disponível do parente

### flex-grow e flex-shrink

- quando o container é esticado e contém mais espaço que o necessário para os flex items, flex-grow especifica se os itens devem crescer para preencher o container e se alguns itens devem crescer proporcionalmente mais que outros

- default é `flex-grow: 0; flex-shrink: 1;`

  ```css
  .cresce-o-dobro {
  	flex-grow: 2;
  }
  
  .cresce-normal {
  	flex-grow: 1;
  }
  
  .nao-cresce {
  	(flex-grow: 0;)
  }
  ```

- `flex-shrink` diz como os elementos devem ser reduzidos

- quanto maior, mais o elemento é reduzido proporcionalmente a outros com `flex-shrink` menor

- default é `flex-shrink: 1` (os elementos são automaticamente reduzidos, por padrão)

### flex-basis

- determina o limiar da atuação de `flex-grow` e `flex-shrink`
- também determina a largura inicial do elemento, quando o container não estiver nem esticado nem diminuído

### flex

- declara `flex-grow`, `flex-shrink` e `flex-basis` ao mesmo tempo

  ```css
  p {
    flex-grow: 1;
    flex-shrink: 2;
    flex-basis: 100px;
  }
  
  /* equivalente a */
  p {
      flex: 1 2 100px;
  }
  ```

### flex-wrap

- usado quando não se quer que um elemento seja diminuído quando falta espaço, mas que ele vá pra próxima linha do container
  - `wrap`: os itens vão pra próxima linha
  - `wrap-reverse`: itens vão pra linha anterior
  - `nowrap`: itens não se movem pra outra linha (default)

### flex-direction

- distribui os elementos em linha ou coluna (**seta main axis**)
  - `row`: esquerda pra direita, alinhado com TL
  - `row-reverse`: direita pra esquerda, alinhado com TR
  - `column`: cima pra baixo, alinhado com TL
  - `column-reverse`: baixo pra cima, alinhado com BL

### flex-flow

- declara `flex-direction` e `flex-wrap`, respectivamente