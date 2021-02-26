[TOC]

# html cheatsheet

## estrutura básica

```html
<!DOCTYPE html>
<html>
<head>
    <title>titulo</title>
    <meta charset="utf-8">
</head>
<body>
    
</body>
</html>
```

## tags comuns

###  span vs. p

- `p` contém longos blocos de plain-text
- `span` contém trechos curtos de texto, separando tais trechos do resto do parágrafo. Ideal usar quando o texto está `inline`, ou seja, dentro do parágrafo

###  strong e em

- enfatizam o texto. No estilo padrão de HTML,
  - `strong` => negrito
  - `em` => itálico

###  br

- quebra o texto, iniciando uma nova linha

###  ul e ol

- `ul` é pra listas sem ordenação
- `ol` é pra listas com ordenação

###  img

```html
<img src="img-path.jpg" alt="legenda quando imagem não carrega"/>
```
- `alt` é lido por mecanismos de leitura por voz
  - auxilia motores de buscas a pescarem o site
  - o texto é renderizado pelo navegador como o texto `alt` quando a imagem não é carregada corretamente

###  video
```html
<video src="video-path.mp4" width="320" height="240" controls>
	legenda quando video não carrega
</video>
```

###  a
```html
<a href="link">descricao</a>

<a href="link" target="_blank">_blank abre link em outra pagina</a>

<a ...>
	<img ... alt="imagem que eh um link">
    </img>
</a>

<a href="#paragrafo-importante">link pro paragrafo importante</a>
<p id="paragrafo-importante"></p>
```

### comentário
```html
<!-- isso eh um comentario -->
```

### section

### hr

## tabelas

```html
<table>
  <thead>
    <tr>
      <th></th>
      <th scope="col">Saturday</th>
      <th scope="col">Sunday</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">Morning</th>
      <td rowspan="2">Work</td>
      <td rowspan="3">Relax</td>
    </tr>
    <tr>
     <th scope="row">Afternoon</th>
    </tr>
    <tr>
      <th scope="row">Evening</th>
      <td>Dinner</td>
    </tr>
  </tbody>
</table>
```

- `tbody`, `thead` e `tfooter` são usados pra particionar tabelas com grandes volumes de dados
  - `thead` é onde se coloca o cabeçalho (`th` com escopo de coluna)
  - `tbody` é onde se coloca os dados (`td`, `th` com escopo de linha)
  - `tfoot` é pra última linha da tabela
- `tr` significa linha da tabela e é usada em todo lugar
- `scope` é usado pra determinar se a tag `th` está tem papel de coluna ou de linha
- `rowspan="X"` e `colspan="Y"` fazem com que o elemento se extenda por X linhas e Y colunas, respectivamente 

## form

```html
<form action="/example.html" method="POST">
	<h1>Form</h1>
    <p>Example of form</p>
    <label for="label-id">label text</label>
    <input id="label-id" type="text" name="text-field" value="default-text">
</form>
```

- `action` é pra onde os dados são enviados
- `method` descreve o método HTTP associado ao request produzido pelo form
- quando o `form` é submetido, a informação `text-field = valor` é enviado para a página definida por `action`
- se o user clicar em `label`, o `input` relacionado é iluminado

### inputs comuns

#### password

```html
<form>
    <input id="password" type="password" name="password">
</form>
```

#### numero

```html
<form>
	<input id="years" name="years" type="number" step="1">    
</form>
```

#### range (slider)

```html
<form>
	<input id="volume" name="volume" type="range" min="0" max="100" step="1">
</form>
```

#### checkbox

```html
<form>
  <p>Choose your pizza toppings:</p>
  <label for="cheese">Extra cheese</label>
  <input id="cheese" name="topping" type="checkbox" value="cheese">
  <br>
  <label for="pepperoni">Pepperoni</label>
  <input id="pepperoni" name="topping" type="checkbox" value="pepperoni">
  <br>
  <label for="anchovy">Anchovy</label>
  <input id="anchovy" name="topping" type="checkbox" value="anchovy">
</form>
```

- usar o mesmo name nos `checkbox`es os agrupam

#### radio

```html
<form>
  <p>What is sum of 1 + 1?</p>
  <input type="radio" id="two" name="answer" value="2">
  <label for="two">2</label>
  <br>
  <input type="radio" id="eleven" name="answer" value="11">
  <label for="eleven">11</label>
</form>
```

- permitem somente uma opção
- assim como com `checkbox`es, mesmo `name` agrupa em uma só estrutura

#### dropdown

```html
<form>
  <label for="lunch">What's for lunch?</label>
  <select id="lunch" name="lunch">
    <option value="pizza">Pizza</option>
    <option value="curry">Curry</option>
    <option value="salad">Salad</option>
    <option value="ramen">Ramen</option>
    <option value="tacos">Tacos</option>
  </select>
</form>
```

- a submissão do form envia `lunch = pizza`, se a primeira opção tiver sido selecionada

#### datalist

```html
<form>
  <label for="city">Ideal city to visit?</label>
  <input type="text" list="cities" id="city" name="city">
 
  <datalist id="cities">
    <option value="New York City"></option>
    <option value="Tokyo"></option>
    <option value="Barcelona"></option>
    <option value="Mexico City"></option>
    <option value="Melbourne"></option>
    <option value="Other"></option>  
  </datalist>
</form>
```

- permite o usuário digitar texto e selecionar algum possível match
- caso não exista match, o que o usuário digita é enviado no submit
- no submit, o que é enviado é `city = Tokyo`, caso o user digite Tokyo no `input` e/ou selecione a opção que aparece

#### textarea

```html
<form>
  <label for="blog">New Blog Post: </label>
  <br>
  <textarea id="blog" name="blog" rows="5" cols="30">
  </textarea>
    
  <textarea>texto padrão</textarea>
</form>
```

- para textos grandes
- `rows` e `cols` controlam o número de linhas e colunas

#### submissão

```html
<form>
  <input type="submit" value="Send">
</form>
```

- renderiza mais ou menos como um botão

![image-20210223153534701](/home/fernando/.config/Typora/typora-user-images/image-20210223153534701.png)

#### observações

- `placeholder` aparece como diga na tag e some quando o usuário clica

#### validação

- para forçar usuário a colocar algum valor 

  ```html
  <input ... required>
  ```
  
- em inputs numéricos, para forçar mínimo e máximo
	```html
	<input type="number" min="1" max="10">	
	```

- em inputs de texto, para forçar tamanho mínimo e máximo do texto

  ```html
  <input type="text" minLength="5" maxLength="250">
  ```

- `regex`

  ```html
  <input ... pattern="[a-zA-Z0-9]+"
  ```

  

