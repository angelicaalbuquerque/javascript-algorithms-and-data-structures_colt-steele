# Seção 1: Big O Notation

> 💡 Performance importa.

Assuntos abordados nesta seção:

- Necessidade da Notação Big O;
- O que é Big O Notation;
- Simplificar a Notação Big O;
- Definir "complexidade de tempo" e "complexidade de espaço";
- Avaliar a "complexidade de tempo" e "complexidade de espaço" de um algoritmo usando a Notação Big O;
- Descrever o que é logaritmo.

### Necessidade da Notação Big O

Há diversas implementações que são válidas para um mesmo problema. Elas são diferentes, não apenas em nomes e variáveis, mas em abordagens também. Mas como julgar qual delas é a melhor? É disso que trata o Big O.

É um sistema, é uma maneira de generalizar o código, falar sobre ele e comparar o código e seu desempenho com outras partes do código. É como se fosse uma tabela de classificação, com rótulos como "ótimo", "muito bom", "apenas ok", "eh..." e "terrível". Entretanto, essa classificação é feita de forma numérica.

Mas por que isso importa? Porque performance importa. Uma implementação de algoritmo pode economizar uma hora toda vez que é executada em comparação com outra implementação. Isso pode ser muito importante para um sistema que é executado milhões de vezes por dia.

Outros motivos da importância da notação Big O:

- Ajuda você a falar melhor sobre seu código;
- É importante ter um vocabulário preciso para falar sobre o desempenho do nosso código (é útil entender como sua solução se compara em desempenho com outras);
- É bom para discutir vantagens e desvantagens entre diferentes abordagens;
- Ao debugar o código, ajuda a entender as coisas que estão diminuindo a velocidade, não apenas procurar erros, ajudando identificar pontos ineficientes;
- Aparece bastante em entrevistas de emprego.

### Cronometrando nosso código

Vamos comparar a eficiência dos códigos abaixo. Ambos escrevem uma função que calcula a soma de todos os números de 1 até (e incluindo) algum número n.

```js
function addUpTo(n) {
  let total = 0;
  for (let i = 1; i <= n; i++) {
    total += i;
  }
  return total;
}
```

```js
function addUpTo(n) {
  return (n * (n + 1)) / 2;
}
```

Qual é a melhor? E o que "ser melhor" quer dizer? É rapidez? É quanto de memória é usada para guardar os dados cada vez que essa função é chamada? Legibilidade?

Geralmente, ser rápido e ocupar menos memória é o que costuma ser mais importante, mas costuma também prejudicar na legibilidade do código.

> 💡 É necessário ter um equilíbrio entre escrever um bom código e escrever um código eficiente que não consome muita memória e que também é legível.

Como eu rotulo o que é melhor? É baseado em quê?

#### O problema com o tempo

Mesmo testando a performance dos algoritmos, é preciso saber que:

- _Diferentes_ máquinas executam os códigos de forma diferente - as margens podem mudar, as medições reais podem ser diferentes e é quase garantido que haverá tempos diferentes;
- A _mesma_ máquina executará os códigos de forma diferente - o navegador e o sistema operacional podem afetar a velocidade;
- Para algoritmos rápidos, as medidas de velocidade podem não ser precisas o suficiente.

Então, como falamos qual código melhor, em termos gerais, sem ter que cronometrá-lo? Não quero fazer um teste para descobrir apenas qual é o melhor, quero saber qual é o melhor em termos gerais. E é aí que entra a Notação Big O.

#### Contando operações

> 💡 O tempo sempre será determinado pelo número de operações.

Em vez de contar os segundos exatos necessários para a execução do código, que podem mudar tanto, o que podemos fazer é contar várias operações simples que um computador precisa executar, porque isso permanece constante, independentemente de qual computador estamos.

No código abaixo, existem apenas três operações: multiplicação, adição e divisão, sem importar o tamanho do número _n_.

```js
function addUpTo(n) {
  return (n * (n + 1)) / 2;
}
```

Nesta outra solução, existem um pouco mais de operações. Além disso, tem uma variável _total_ que é criada e que é incrementada a cada iteração do loop.

```js
function addUpTo(n) {
  let total = 0;
  for (let i = 1; i <= n; i++) {
    total += i;
  }
  return total;
}
```

Então, a quantidade de operações é proporcional ao tamanho do número _n_. Se _n_ for 20, haverão 20 operações. Se _n_ for 100, haverão 100 operações. Não são apenas 3 operações, são _n_ adições.

Detalhando melhor o número de cálculos:

<code>total = 0</code>: apenas uma operação;
<code>let i = 1</code>: apenas uma operação;
<code>i <= n</code>: _n_ operações de <code><</code> e _n_ operações de <code>==</code>, totalizando _2n_ operações de comparação;
<code>i++</code>: _n_ adições e operações.

Nesse caso, a complexidade é de 5n+2 (5 operações de n + 2 que estão fora do loop), que é a mesma coisa que dizer que o número de operações cresce proporcionalmente ao número _n_.

Portanto, se _n_ for 10, haverão 52 operações. Se _n_ for 100, haverão 502 operações. Se _n_ for 1000, haverão 5002 operações.

> 💡 A ferramenta [Performance Tracker](https://rithmschool.github.io/function-timer-demo/) ajuda a entender ou traçar o tempo que as funções levam para serem executadas e obter um gráfico de desempenho.

### Introdução oficial à Notação Big O

Big O nos permite falar de uma maneira muito formal sobre como o tempo de execução de um algoritmo cresce à medida que as entradas aumentam.

É uma maneira de descrever o relacionamento entre a entrada para uma função ou à medida que ela cresce e como isso altera o tempo de execução dessa função; a relação entre o tamanho da entrada e, em seguida, o tempo relativo a essa entrada.

> 💡 Dizemos que um algoritmo é _O(f(n))_ se o número de operações simples a serem executadas for eventualmente menor que uma constante vezes _f(n)_, enquanto _n_ cresce.

Relacionamento de um input de _n_ com o tempo de execução:

- f(n) pode ser linear (f(n) = n) _enquanto n cresce, o tempo de execução cresce linearmente_;
- f(n) pode ser quadrática (f(n) = n²) _enquanto n cresce, o tempo de execução cresce quadraticamente_;
- f(n) pode ser constante (f(n) = 1) _enquanto n cresce, o tempo de execução não cresce e não é impactado, pois é sempre constante_;
- f(n) pode ser algo totalmente diferente!

Sendo assim, enquanto _n_ cresce, como isso muda para refletir no tempo de execução?

Exemplos:

1. **Sempre 3 operações: O(1)** - enquanto _n_ cresce à medida que a entrada para essa função cresce, isso não reflete no tempo de execução.

```js
function addUpTo(n) {
  return (n * (n + 1)) / 2;
}
```

2. **Número de operações limitada por múltiplo de _n_: O(_n_)** - É uma constante. Enquanto _n_ cresce, o tempo de execução cresce basicamente em proporção 1:1 e o número de operações é (eventualmente) limitado por um múltiplo de _n_. Não importa se é 1n, 5n, 10n... porque no final isso é simplificado para apenas O(n), pois estamos preocupados apenas com a ordem de magnitude.

```js
function addUpTo(n) {
  let total = 0;
  for (let i = 1; i <= n; i++) {
    total += i;
  }
  return total;
}
```

3. **0(n)** - Na parte "Going up!" do código, enquanto o _n_ cresce o loop cresce,então temos 0(n). O mesmo para a parte "At the top!", que também é 0(n). Sendo assim, é uma constante e se _n_ triplicar, o templo de execução também triplicará. Lembrando que não nos preocupamos com quantos _n_ temos, mas sim com o cenário.

```js
function countUpAndDown(n) {
  console.log("Going up!");
  for (var i = 0; i < n; i++) {
    console.log(i);
  }
  console.log("At the top!\nGoing down...");
  for (var j = n - 1; j >= 0; j--) {
    console.log(j);
  }
  console.log("Back down. Bye!");
}
```

4. **Operação O(n) dentro de uma operação O(n): 0(n²)** - Temos um loop aninhado. O primeiro loop é O(n), pois enquanto _n_ cresce, terá um número _n_ de operações. O segundo loop é também O(n). Nesse exemplo, não podemos simplificar tudo como O(n) porque os loops estão aninhados. Como essa operação é O(n\*n)- podemos simplificar para O(n²) -, significa que à medida que _n_ cresce, o tempo de execução cresce proporcionalmente na taxa n². É uma quadrática.

```js
function printAllPairs(n) {
  for (var i = 0; i < n; i++) {
    for (var j = 0; j < n; j++) {
      console.log(i, j);
    }
  }
}
```

### Simplificando Expressões Big O

Conforme vimos em exemplos anteriores, contar operações diferentes pode ser complicado e que a contagem exata realmente não importa, o que importante é a tendência geral.

Por exemplo, podemos simplificar numa operação **5n + n** por apenas **n**, já que à medida que **n** cresce, o tempo de execução cresce proporcionalmente e não importa se são duas, três, dez, vinte, cinquenta vezes.

Existem algumas regras para simplificar expressões Big O, que são consequências da definição de Big O.

- Constantes não importam;

  - Se temos algo como _O(2n)_, simplificamos para _O(n)_.
  - Se temos algo como _O)(500)_, simplificamos para _O(1)_.
  - Se temos algo como _O(13n²)_, simplificamos para _O(n²)_.

- Termos menores também não importam.
  - Se temos algo como _O(n + 10)_, simplificamos para _O(n)_.
  - Se temos algo como _O(1000n + 50)_, simplificamos para _O(n)_, não precisamos da constante 1000*n* e nem do termo 50.
  - Se temos algo como _O(n² + 5n + 8)_, simplificamos para _O(n²)_.

### Big O shorthand

- Analisar a complexidade com Big O pode ser complicado;
- Tem regras práticas que podem ajudar;
- Essas regras nem sempre irão funcionar, mas são boas para a maioria dos casos.

1. Operações aritméticas são constantes;
   - Não importa o tamanho do número a ser processado, seu computador leva aproximadamente o mesmo tempo para executar uma operação aritmética, seja 2 + 2 ou 1 milhão + 2.
2. Atribuição de variável também é constante;
   - O computador leva o mesmo tempo para criar uma variável que você sabe que X é igual a 5, ou que X é igual a 1 milhão.
3. Acessar elementos em um array (por index) ou objeto (por chave) é uma operação constante;
   - O computador leva o mesmo tempo para acessar o primeiro elemento de um array ou o último elemento de um array.
4. Em um loop, a complexidade é a duração do loop vezes a complexidade de qualquer operação que aconteça dentro do loop;
   - Se você tem um loop aninhado, e o loop externo tem complexidade O(n) e o loop interno tem complexidade O(n²), então o loop externo é O(n²).

No gráfico abaixo, vemos com clareza a diferença entre as complexidades. Perceba que O(1) é sempre uma constante em linha reta, enquanto O(n) cresce de acordo com o tamanho do _n_.

<div align="left">
    <img src=".github/01-general-trend.png" width="500"/>
</div>

### Complexidade de Espaço

> 💡 Complexidade de Espaço é o espaço sobre a quantidade de memória que um algoritmo usa.

Até agora, nos preocupamos apenas com a complexidade do tempo, sobre a rapidez com que os algoritmos são executados com o tempo de execução — Analisamos o tempo de execução de um algoritmo conforme o tamanho da entrada aumenta.

Mas também podemos nos preocupar com a complexidade do espaço, que é o que acontece com o espaço que um algoritmo ocupa à medida que o tamanho da entrada aumenta. Quanto de memória adicional precisamos alocar para executar o código em nosso algoritmo?

à medida que _n_ cresce, assumimos que o resultado final vai crescer Portanto, não vamos nos preocupar com esse espaço, vamos nos preocupar com as repercussões que têm dentro do algoritmo, o que acontece dentro do algoritmo.

**Regras básicas**:

- A maioria dos primitivos (booleans, numbers, undefined, null) são constantes, ou seja, ocupam um espaço fixo na memória;
- Strings ocupam um espaço de memória proporcional ao tamanho da string, sendo assim, requerem um espaço O(_n_), onde _n_ é o tamanho da string;
- Tipos de referência são, geralmente, O(_n_), onde _n_ é o tamanho do array (para arrays) ou o número de chaves (no objeto).

Observando um exemplo para analisar a complexidade de espaço:

```js
function sum(arr) {
  let total = 0;
  for (let i = 0; i < arr.length; i++) {
    total += arr[i];
  }
  return total;
}
```

Bem, não importa qual seja o comprimento do array, temos uma variável chamada _total_ (1 número) e então estamos fazendo um _loop_, que tem uma segunda declaração dentro dele (outro número).

Essa função só tem duas variáveis e não estamos adicionando novas variáveis com base no comprimento do array. Isso significa que temos um espaço constante, ou seja, O(1).

Outro exemplo:

```js
function double(arr) {
  let newArr = [];
  for (let i = 0; i < arr.length; i++) {
    newArr.push(2 * arr[i]);
  }
  return newArr;
}
```

À medida que o comprimento do array cresce, o comprimento do novo array (uma matriz) também cresce. Na linha <code>let newArr = [] </code> vamos criar uma nova matriz, mas isso não é tão significativo quanto <code>newArr.push(2 \* arr[i]);</code>, onde temos essa nova matriz e ela está ficando cada vez mais longa diretamente na proporção do comprimento da entrada. Logo, se a matriz tiver 10 itens, estamos armazenando 10 itens em uma nova matriz.

Sendo assim, o espaço ocupado será diretamente proporcional ao tamanho da entrada, ou seja, O(_n_).

<!-- ### Logs e Recapitulação -->
