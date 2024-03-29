
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

À medida que _n_ cresce, assumimos que o resultado final vai crescer. Portanto, não vamos nos preocupar com esse espaço, vamos nos preocupar com as repercussões que têm dentro do algoritmo, o que acontece dentro do algoritmo.

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

### Logs

Vimos até aqui algumas complexidades comuns: O(1), O(_n_) e O(_n²_). Entretanto, algumas vezes expressões big O envolvem expressões matemáticas mais complexas. Uma das que aparecem com muita frequência é o logaritmo.

Em vez da complexidade do tempo desses algoritmos terminar em O(_n_), eles podem terminar em O(log _n_).

#### O que é logaritmo?

Assim como divisão e multiplicação são um par, logaritmo e exponenciação são também um par. O logaritmo é o inverso da exponenciação.

Exemplo:

<code>Log2(8) = 3</code>

A leitura é feita como logaritmo de 8 na base 2 é igual a 3. E o que estamos calculando é que se elevarmos 2 a algo, que algo é esse que nos dará 8?

A resposta é 3. Se elevarmos 2 ao cubo, obteremos 8 (2³ = 8). Logo:

<code>log2(valor) = expoente</code> É respondido por <code>2^expoente = valor</code>.

> 💡 A base do logaritmo nem sempre é 2. Podemos ter logaritmos na base 10, na base 3, na base 5, etc. Mas a base 2 é a mais comum. Podemos omitir o 2 da fórmula, já que é a base mais comum, então podemos escrever apenas <code>log</code>.

> 💡 O logaritmo de um numero aproximadamente mede o número de vezes que você pode dividir esse número por 2 **antes de chegar a um valor que é menor ou igual a 1**.

Então, se tivermos um 8, dividiremos por 2 e ainda será maior que 1 (4). Se dividirmos de novo, continuará maior que 1 (2). Então alcançamos o valor 1, e não podemos dividir mais. Então, o logaritmo de 8 é 3.

Vejamos melhor o exemplo:

<div align="left">
    <img src=".github/02-log.png" width="500"/>
</div>

Entretanto, o cálculo exato não é tão importante. O que importa é que, se olharmos para o gráfico anteriormente mostrado aqui, podemos perceber que a complexidade de tempo logarítmica é ótima! Depois da constante O(1), é a melhor complexidade de tempo que podemos ter.

#### Por que isso importa?

- Certos algoritmos têm complexidade de tempo logarítmica;
- Algoritmos de ordenação eficientes envolvem logaritmos;
- Recursão às vezes envolve complexidade de espaço logarítmica.

### 📌 Recapitulação Notação Big O

- Para analisar o desempenho de um algoritmo, nós utilizamos Notação Big O;
  - _Queremos saber como o tempo muda ou como a complexidade do espaço muda à medida que o tamanho da entrada aumenta._
- Big O pode nos dar um entendimento de alto nível de complexidade de tempo ou espaço de um algoritmo;
- Notação Big O não liga para precisão, apenas para tendências gerais (linear? quadrática? constante?);
- A complexidade do espaço ou tempo, medida pelo Big O, depende apenas do algoritmo e não do hardware que utilizamos para executá-lo;
- Big O está em todo lugar e precisamos praticar.

# Seção 2: Análise de performance de arrays e objetos

Agora que já vimos Big O, vamos analisar coisas básicas que fazemos o tempo inteiro em JS: arrays, objetos e métodos built-in. Como é a performance? Qual método pode ser mais lento? Quais são as coisas mais rápidas que podemos fazer com um array?

Objetivos desta seção:

- Entender como objetos e arrays trabalham, através das lentes do Big O;
- Explicar por que adicionar elementos ao início de um array é custoso;
- Comparar e contrastra o tempo de execução de arrays e objetos, assim como métodos built-in (como forEach e Object.keys()...).

### The Big O de objetos

Objetos são estruturas de dados não ordenadas e tudo é armazenado em pares de valores-chave. Exemplo:

```js
let instructor = {
  firstName: "Kelly",
  isInstructor: true,
  favoriteNumbers: [1, 2, 3, 4],
};
```

#### Quando utilizar objetos:

- Quando não precisamos de ordem, objetos são uma escolha excelente;
- Quando precisamos de rápido acesso / inserção e remoção.

Quando falamos em rapidez, estamos falando de tempo constante para quase todas as ações:

- Inserção: O(1);
- Remoção: O(1);
- Busca: O(N);
- Acesso: O(1).

O tempo de busca é O(N) porque, para buscar um valor, precisamos percorrer todo o objeto para ver se aquele valor existe. E se potencialmente o número de propriedades cresce à medida que N cresce, logo cresce a quantidade de tempo que leva para fazer essa busca. Entretanto, se quisermos acessar um valor, o tempo de acesso é O(1), pois não precisamos percorrer todo o objeto para encontrar aquele valor.

#### Big O de métodos de objetos

- Object.keys: O(N);
  - _Retorna todas as chaves de um objeto. O(N) porque precisamos percorrer todo o objeto para encontrar todas as chaves._
- Object.values: O(N);
  - _Retorna todos os valores de um objeto. O(N) porque precisamos percorrer todo o objeto para encontrar todos os valores._
- Object.entries: O(N);
  - _Retorna um array de arrays contendo todas as chaves e valores de um objeto. O(N) porque precisamos percorrer todo o objeto para encontrar todas as chaves e valores, o que torna esse método mais trabalhoso._
- hasOwnProperty: O(1).
  - _Verifica se um objeto possui uma determinada chave. O(1) porque não precisamos percorrer todo o objeto para encontrar a chave._

### Arrays através das lentes do Big O

O grande ponto dos arrays é que elas são ordenadas, diferentemente dos objetos, que não são. Isso é muito útil, mas pode ter custos para algumas das operações.

Quando utilizar arrays:

- Quando precisamos de ordem, arrays são uma escolha excelente;
- Quando precisamos de acesso rápido / inserção e remoção (em certas situações).

#### Big O de arrays

- Inserção: depende;
  - _Se inserirmos um elemento no final do array, o tempo de inserção é O(1). Mas se inserirmos um elemento no início do array, o tempo de inserção é O(N), pois tem relação com a quantidade de índices, que precisarão ser reindexados. Exemplo: let names = ["Michael", "Ana", "Eric"]. Se eu inserir "Gustavo" no início, os outros nomes não ocuparão mais os índices 0, 1 e 2, respectivamente, precisando ser reindexados._
- Remoção: depende;
  - _Se removermos um elemento do final do array, o tempo de remoção é O(1). Mas se removermos um elemento do início do array, o tempo de remoção é O(N), pois os índices precisarão ser reindexados._
- Busca: O(N);
  - _Para buscar um elemento em um array, precisamos percorrer todo o array para encontrar aquele elemento. E se potencialmente o número de elementos cresce à medida que N cresce, logo cresce a quantidade de tempo que leva para fazer essa busca._
- Acesso: O(1).
  - _Para acessar um elemento em um array, o tempo de acesso é O(1), pois não precisamos percorrer todo o array para encontrar aquele elemento, podemos pular imediatamente para o index, independentemente do tamanho do array._

> 💡 push() e pop() são métodos que adicionam e removem elementos do final do array, respectivamente, e são mais rápidos que shift() e unshift(), métodos que adicionam e removem elementos do início do array, respectivamente.

#### Big O de métodos de arrays

- push: O(1);
  - _Adiciona um elemento ao final do array. O(1) porque não precisamos percorrer todo o array para encontrar o final, podemos pular imediatamente para o último index, independentemente do tamanho do array._
- pop: O(1);
  - _Remove um elemento do final do array. O(1) porque não precisamos percorrer todo o array para encontrar o final, podemos pular imediatamente para o último index, independentemente do tamanho do array._
- shift: O(N);
  - _Remove um elemento do início do array. O(N) porque os índices precisarão ser reindexados._
- unshift: O(N);
  - _Adiciona um elemento ao início do array. O(N) porque os índices precisarão ser reindexados._
- concat: O(N);
  - _Concatena dois arrays. O(N) porque à medida que os arrays crescem, o tempo vai demorar e crescer proporcionalmente ao tamanho total do novo array. Tecnicamente, poderíamos argumentar que a complexidade deveria ser O(N + m), onde m é o tamanho do novo array, mas O(N) já serve._
- slice: O(N);
  - _Retorna uma cópia de uma parte de um array. O(N) porque se tentarmos copiar 10 elementos vs 1000 elementos de um array, a quantidade de tempo irá aumentar proporcionalmente ao tamanho da cópia ou de quantos elementos estamos tentando copiar._
- splice: O(N);
  - _Remove e/ou adiciona elementos de um array e, opcionalmente, os substitui por outros elementos. O(N) porque vai ser preciso reindexar os elementos._
- sort: O(N \* log N);
  - _Ordena os elementos de um array. O(N \* log N) porque o algoritmo de ordenação é baseado em comparações, e o tempo de comparação é O(log N)._
- forEach/map/filter/reduce/etc: O(N);
  - _Esses métodos iteram sobre cada elemento de um array. O(N) porque eles estão fazendo looping sobre cada elemento ou fazendo algo para cada elemento, seja um teste booleano ou apenas imprimindo o que estamos fazendo, isso envolve atuar em cada elemento ou com cada elemento. Assim, à medida que o tamanho do array aumenta, aumenta a quantidade de tempo que leva para percorrê-lo._

### 📌 Recapitulação Arrays e Objetos

- Quase tudo o que podemos fazer com arrays, todos os métodos incorporados, tem complexidade O(N);
- Ordenação é o mais lento, O(N \* log N);
- Os métodos push e pop são costantes, O(1), super rápidos;
- Objetos são rápidos em praticamente tudo, mas não há ordem para os arrays, que são ótimos quando você precisa de ordenação;
- Arrays são ótimos para ordenação, mas lembre-se que é melhor se você puder fazer adições e remoções no final do array, pois é mais rápido do que no início;
- Adicionar/remover algo tanto no começo quanto no meio de um array causa um efeito cascata de reindexação.

# Seção 3: Abordagem de Resolução de Problemas

> 💡 Muitas das estratégias que vamos discutir são baseadas no livro **_How To Solve It_**, de George Polya.

Quando encaramos um problema de código para resolver, é importante que tenhamos uma abordagem para resolver esse problema. Que passos podemos seguir para torná-lo resolvido?

_Esta primeira seção é mais sobre a abordagem básica para resolver um problema que você não sabe resolver. Passos que você pode dar, etapas para torná-lo mais fácil. A segunda seção que vem depois dessa é mais focada em código e é sobre projetos específicos e pequenas estratégias para resolver problemas._

Objetos da seção:

- Definição de algoritmo;
- Elaborar um plano para resolver algoritmos;
- Comparar e contrastar padrões de resoluções de problemas, incluindo contadores de frequência, dividir e conquistar e técnica two pointers.

### O que é um algoritmo?

Um **processo** ou um **conjunto de etapas** para realizar uma determinada tarefa.

Por que é importante saber disso?

- Quase tudo o que você faz em programação envolve algum tipo de algoritmo, sejam coisas super básicas ou um aplicativo complexo;
- É o fundamento para ser um solucionador de problemas de sucesso e um bom programador.

Como melhorar suas habilidades?

- Estabeleça um plano para resolver problemas;
- Domine os padrões comuns de resolução de problemas.

### Estratégias de resolução de problemas

- 1. Entenda o problema;
- 2. Explore exemplos concretos;
- 3. Quebre-o em partes menores;
- 4. Resolva/simplifique o problema;
- 5. Olha para trás, refatore e melhore o código.

Nesta seção, vamos explorar cada uma dessas etapas em detalhes.

## Passo 1) Entenda o problema

_Você pode criar um aplicativo copiando um passo a passo e copiar o código de outras pessoas. Mas quando se trata de resolver problemas novos e novos desafios, a coisa fica mais difícil._

_Você melhora isso com o tempo, independentemente das tecnologias que você usa, da linguagem em que está trabalhando, é realmente importante ter um forte conjunto de habilidades para resolver problemas. E muito disso virá naturalmente com o tempo, mas vale a pena ser deliberado, vale a pena ter um plano. Esse plano não vai resolver seus problemas, mas vai ajudá-lo a pensar para resolvê-lo e ajudar as soluções surgirem de maneira mais natural._

Antes de começar a sair codando ou tentar resolver o problema, é importante dar um passo atrás e garantir que você entende a tarefa que está à sua frente. O que você está tentando resolver? O que você está tentando fazer? O que você está tentando construir?

Tem diversas perguntas que você pode fazer para ajudar a garantir que você entenda o problema:

1. Você pode reafirmar o problema com suas próprias palavras?
   - _Apenas certifique-se de que você pode reformular novamente a pergunta. Mude um pouco, com suas próprias palavras, para garantir que você realmente entenda a pergunta._
2. Quais são as entradas que o problema requer?
   - _Quais são os dados que você precisa para resolver o problema._
3. Quais são as saídas que devem vir da solução do problema?
   - _Quais são os resultados que você precisa gerar ao resolver o problema._
4. As saídas podem ser determinadas a partir das entradas? Em outras palavras, você tem todas as informações necessárias para resolver o problema?
5. Como devo rotular as peças importantes de dados que são parte do problema?
   - _Qual a terminologia que você deve usar._

#### Exemplo: Escreva uma função que pega dois números e retorna a soma deles.

_1) Posso reafirmar o problema com minhas próprias palavras?_
Implementar adição.

_2) Quais são as entradas que o problema requer?_
Não são simplesmente dois números. Serão inteiros? Floats? O que dizer sobre string para números maiores?

_3) Quais são as saídas que devem vir da solução do problema?_
Não é simplesmente o resultado. Serão inteiro? Float? String?

_4) As saídas podem ser determinadas a partir das entradas? Em outras palavras, você tem todas as informações necessárias para resolver o problema?_
Se alguém não passar um número, retornamos um null? adicionamos um 0? o que faremos?

_5) Como devo rotular as peças importantes de dados que são parte do problema?_
Talvez o nome da função seja _add_, e os parâmetros sejam _num1_ e _num2_, e _sum_ seja o resultado.

## Passo 2) Explore exemplos concretos

Depois de entender o problema, garantindo que sabemos todas as entradas/saídas e o que estamos resolvendo, agora é a vez de surgir com exemplos que podem ajudar a entender melhor o problema.

Exemplos também fornecem as verificações para que sua solução eventual, se você tiver uma, funcione como esperado.

Portanto, se você tiver exemplos, poderá verificar se sua solução funciona, e também poderá obter mais informações executando esses exemplos.

Isso se aplica em uma escala maior, como User Stories e Testes Unitários, mas é importante ter exemplos concretos para ajudar a entender o problema.

#### Passos para explorar exemplos concretos:

1. Comece com exemplos simples;
   - Agora, anote dois ou três exemplos simples com uma entrada e depois a saída. Exemplos mais simples, os que devem fazer você conhecer os casos de uso mais fáceis, progridem.
2. Progrida para exemplos mais complexos;
3. Explore exemplos com entradas vazias;
   - Isso deve dar insights de como o problema deve funcionar.
4. Explore exemplos com entradas inválidas;
   - O que acontece se o usuário inserir algo inválido?

#### Exemplo: Escreva uma função que pega uma string e retorna a contagem de cada caractere nessa string.

Depois de fazer todos os passos da seção anterior, de reafirmar o problema/ver entradas e saídas/como rotular as terminologias, vamos começar a coletar os exemplos concretos pra solucionar esse problema acima.

**1. Comece com exemplos simples;**

- _"a" -> {a: 1}_
- _"aa" -> {a: 2}_

Exemplo 1:

```js
charCount("aaaa"); // deve retornar {a: 4}
```

Exemplo 2:

```js
charCount("hello"); // deve retornar {h: 1, e: 1, l: 2, o: 1}
```

Exemplo 3:

```js
charCount("aaaa"); // deve retornar {a: 4, b: 0, c: 0, d: 0}
```

**2. Progrida para exemplos mais complexos;**

- _"my phone number is 182763"_ - Se isso fosse um input, o que esperamos de retorno? Vamos contar os espaços? E caracteres especiais? E números? Tudo isso seria contado?

- _"Hello hi"_ - Armazenamos uma letra H maiúscula e uma H minúscula? Ou apenas uma delas?

Esses exemplos são realmente apenas outra forma de entender melhor o problema antes de resolvê-lo. Então, isso se vincula muito ao vídeo anterior, compreendendo a pergunta.

**3. Explore exemplos com entradas vazias;**

```js
charCount("");
```

Devemos retornar um objeto vazio ({}) no final? Ou devemos retornar null, false ou undefined? Ou devemos retornar um erro?

E isso está atrelado ao próximo passo, que é explorar exemplos com entradas inválidas.

**4. Explore exemplos com entradas inválidas;**

E se a pessoa passar algo que não é uma string?

## Passo 3) Quebre o problema em partes

Tome as medidas reais do problema e anote-as. Não precisa do pseudo-código completo, não precisa ser válido, você conhece a sintaxe. Faça apenas alguns comentários como um guia para as etapas que eles precisam seguir.

Especialmente em ambientes de entrevista, é importante que você comunique o que está fazendo, eles não querem que você apenas comece a digitar ou escreva código em silêncio. É melhor você sempre informar "Beleza, esses são os passos que eu vou seguir. Você acha que isso pode funcionar?".

Portanto, quebrar o problema é muito importante e **escreva explicitamente os passos que você precisa seguir.**

> 💡 Não precisa ser uma tonelada de detalhes, nem uma linha por linha, toda linha que você precisa para escrever. Apenas os componentes básicos da solução.

> 💡 Isso força você a pensar sobre o código que você irá escrever antes de escrevê-lo, e ajuda você a capturar ou descobrir algumas dúvidas remanescentes ou a conhecer partes que você tem medo e que não entende.

Isso tudo ajuda você a definir as etapas, a manter o foco e a destacar os problemas dos quais você ainda não está confiante sobre. Então, você pode mergulhar e começar a escrever o código.

#### Exemplo: Escreva uma função que pega uma string e retorna a contagem de cada caractere nessa string.

Depois de ter os exemplos, comece a digitar o esqueleto da função, e anote os passos que você precisa seguir.

```js
function charCount(str) {
  // fazer algo
  // retornar algo - um objeto com chaves que são caracteres alfanuméricos minúsculos na string; 
  //valores devem ser a contagem para cada caractere
}
```

```js
function charCount("Your PIN number is 1234!") {
  /*
    1: 1,
    2: 1,
    3: 1,
    4: 1,
    b: 1,
    e: 1,
    i: 2,
    m: 1,
    n: 2,
    o: 1,
    p: 1,
    r: 2,
    s: 1,
    u: 2,
    y: 1
  */
}
```

Expandindo o pensamento, precisamos fazer algo uma vez para cada caractere na string. Também precisamos criar um objeto que retorna no final. Mas a maior parte da lógica envolve repetir todos os caracteres da string e fazer algo.

```js
function charCount(str) {
  // fazer objeto retornar no final
  // loop na string, para cada caractere...
  // se o char é um número/uma letra E uma chave no objeto, adicione um a ela
  //se o char é um número/uma letra E não estiver no objeto, adicione-o e defina seu valor como 1
  //Se o caractere for qualquer outra coisa (espaço, ponto, vírgula, etc.), não faça nada
  // ---
  // retornar objeto no final
  
}
```

Agora com esses passos básicos, podemos preencher os espaços em branco. Para problemas mais complicados, isso realmente pode ser um salva-vidas.

> 💡 Em uma entrevista, se você escreve as etapas que você precisa fazer, mesmo que não tenha certeza de como fazer, demonstra que você pelo menos formulou uma abordagem e se ficar sem tempo e só chegar na metade do caminho, você pelo menos tem o layout do que iria fazer.

## Passo 4) Resolva e simplifique

Às vezes, você pode não estar pronto para resolver um problema inteiro de uma vez. Você pode se sentir bem em cerca de 80%, mas se há algo desafiador ou que você não tem certeza de como fazer, então é aí que a simplificação vem.

> 💡 Tente ignorar a parte que está lhe dando muito trabalho e foque em outra coisa que você consiga fazer, em vez de ficar preso em uma parte difícil de um problema e não ter nenhum progresso. É muito melhor começar a escrever código para fazer as coisas que você sabe fazer em vez de ficar travando a tarefa.  

Então, como vantagens da resolução/simplificação, podemos dizer que: 
- É muito melhor começar a escrever código para fazer as coisas que você sabe fazer, lembrando que você precisa incorporar essa parte mais difícil depois.
- É bastante comum que, ao simplificar um problema, você obtenha informações sobre a solução real.

Então, se você ficar preso em alguma coisa, mas sabe por onde começar ou conhece um lugar para começar, você deve fazer isso. Óbvio, depois de ter entendido o problema, feito exemplos concretos e dividiu o problema em passos.

#### Quanto à simplificação:

- Encontre a principal dificuldade no que está tentando fazer;
- Ignore temporariamente essa dificuldade;
- Escreva uma solução simplificada;
- Então incorpore essa dificuldade de volta.

#### Exemplo: Escreva uma função que pega uma string e retorna a contagem de cada caractere nessa string

```js
function charCount(str) {
  // fazer objeto retornar no final
  // loop na string, para cada caractere...
  // se o char é um número/uma letra E uma chave no objeto, adicione um a ela
  //se o char é um número/uma letra E não estiver no objeto, adicione-o e defina seu valor como 1
  //Se o caractere for qualquer outra coisa (espaço, ponto, vírgula, etc.), não faça nada
  // ---
  // retornar objeto no final
  
}
```

Tem muitas coisas que podem ser problemáticas aqui. Por exemplo, se alguém tiver problema com loop, poderia começar criando um objeto e trabalhando com o primeiro caractere de uma string. E uma vez que você descobrir como lidar com uma string, você passa para letras minúsculas, adicionada a letra ao objeto etc.

Se a pessoa não souber trabalhar com objeto chave/valor, poderia começar com o loop para cada caracteres dessa string e imprimí-los.

Ou você pode não se lembrar o metodo que transforma uma palavra em maiúscula ou minúscula, então poderia ignorar isso e começar com a lógica principal.

No exemplo abaixo, começamos criando o objeto, fazendo o loop ignorando a parte da alfanumérica, verificando apenas se o caractere está no objeto.

```js
function charCount(str) {
  // fazer objeto retornar no final
  var result = {};
  // loop na string, para cada caractere...
  for (var i = 0; i < str.length; i++) {
    var char = str[i]
    // se o char é um número/uma letra E uma chave no objeto, adicione um a ela
    if(result[char] > 0) {
      result[char]++;
    //se o char é um número/uma letra E não estiver no objeto, adicione-o e defina seu valor como 1
    } else {
      result[char] = 1;
    }
  }
  //Se o caractere for qualquer outra coisa (espaço, ponto, vírgula, etc.), não faça nada
  // retornar objeto no final
  return result;
}
```

Agora que temos isso pronto, podemos descobrir como fazer as letras ficarem minúsculas ou maiúsculas.

```js
function charCount(str) {
  // fazer objeto retornar no final
  var result = {};
  // loop na string, para cada caractere...
  for (var i = 0; i < str.length; i++) {
    var char = str[i].toLowerCase()
    // se o char é um número/uma letra E uma chave no objeto, adicione um a ela
    if(result[char] > 0) {
      result[char]++;
    //se o char é um número/uma letra E não estiver no objeto, adicione-o e defina seu valor como 1
    } else {
      result[char] = 1;
    }
  }
  //Se o caractere for qualquer outra coisa (espaço, ponto, vírgula, etc.), não faça nada
  // retornar objeto no final
  return result;
}
```
No final do dia, mesmo que não esteja tudo perfeito, nós escrevemos o que conseguimos, acrescentamos coisas ao objeto, criamos condicionais e agora sabemos que precisamos de uma maneira para tentar trabalhar com os caracteres alfanuméricos.

Se você anda, demonstra que você sabe e demonstra sua capacidade de resolver problemas, em vez de apenas ficar fixado ao problema antes mesmo de começar.

> ❗ É muito melhor escrever algo racionalmente, não só colocar coisas na página e esperar que funcione. Mas coloque as peças certas no lugar para que, depois de descobrir a parte mais difícil, você possa conectá-la.

## Passo 5) É olhar para trás e refatorar

> Parabéns por ter resolvido o problema! Mas você ainda não acabou.

Provavelmente, este é o passo mais importante de quando se trata de se tornar um desenvolvedor melhor.

É importante tentar melhorar o código. É uma oportunidade perdida se você não reservar um tempo para analisar seu código, analisar e refletir sobre ele. E não só sobre como ele é eficiente, mas também como está a legibilidade.

Ao concluir uma tarefa, é importante se perguntas:

1. Você pode checar o resultado para garantir que o código funcione?
2. Você pode gerar o resultado de forma diferente?
3. Você pode usar o resultado ou o método para outro problema?
4. Você pode melhorar a performance da sua solução?
5. Você pode pensar em outros jeitos de refatorar?
6. Como outras pessoas resolveriam esse problema?

#### Continuando o exemplo anterior: Escreva uma função que pega uma string e retorna a contagem de cada caractere nessa string

```js
function charCount(str) {
  var obj = {};

  for (var i = 0; i < str.length; i++) {
    var char = str[i].toLowerCase();
    if(/[a-z0-9]/.test(char)) {
      if(obj[char] > 0) {
        obj[char]++;
      } else {
        obj[char] = 1;
      };
    }
  }
  return obj;
}
```

Começamos mudando o "for" para "for of", mais por estética. Assim, eliminamos a necessidade de fazer "str[i]", por só estarmos trabalhando com "char".

```js
function charCount(str) {
  var obj = {};

  for (var char of str) {
    char = char.toLowerCase();
    if(/[a-z0-9]/.test(char)) {
      if(obj[char] > 0) {
        obj[char]++;
      } else {
        obj[char] = 1;
      };
    }
  }
  return obj;
}
```

Nos "ifs", estamos adicionando um caractere a um valor se ele já existir ou inicializando com um valor 1 se não existir. Como é simples, podemos combinar, se possível, em uma única linha:

```js
function charCount(str) {
  var obj = {};

  for (var char of str) {
    char = char.toLowerCase();
    if(/[a-z0-9]/.test(char)) {
        obj[char] = ++obj[char] || 1;
      } 
    }
  return obj;
}
```

Por último, podemos checar se usar uma expressão regular é a forma mais eficiente de fazer a checagem dos alfanuméricos. Existe algo melhor para checar se algo é uma letra ou um número?

[Após pesquisas, verifcamos que sim, ao utilizar "charCodeAt()"](https://stackoverflow.com/questions/4434076/best-way-to-alphanumeric-check-in-javascript) e comparações booleanas:

```js
function isAlphaNumeric(str) {
  var code, i, len;

  for (i = 0, len = str.length; i < len; i++) {
    code = str.charCodeAt(i);
    if (!(code > 47 && code < 58) && // numeric (0-9)
        !(code > 64 && code < 91) && // upper alpha (A-Z)
        !(code > 96 && code < 123)) { // lower alpha (a-z)
      return false;
    }
  }
  return true;
};
```

Retornando ao nosso código para essa modificação, criamos a função que faz essa checagem e substituimos (deixando ela separada, fica mais legível) a linha que antes era com expressão regular por "isAlphaNumeric(char)":

```js
function charCount(str) {
  var obj = {};

  for (var char of str) {
    char = char.toLowerCase();
    if(isAlphaNumeric(char)) {
        obj[char] = ++obj[char] || 1;
      } 
    }
  return obj;
}


function isAlphaNumeric(char) {
   var  code = char.charCodeAt(0);

    if (!(code > 47 && code < 58) && // numeric (0-9)
        !(code > 64 && code < 91) && // upper alpha (A-Z)
        !(code > 96 && code < 123)) { // lower alpha (a-z)
      return false;
    }
  return true;
};

charCodeAt(0);
```

Podemos também mudar a passagem das letras para minúsculas para ocorrer depois de checar se um caractere é alfanumérico:

```js
function charCount(str) {
  var obj = {};

  for (var char of str) {
    if(isAlphaNumeric(char)) {
      char = char.toLowerCase();
      obj[char] = ++obj[char] || 1;
      } 
    }
  return obj;
}


function isAlphaNumeric(char) {
   var  code = char.charCodeAt(0);

    if (!(code > 47 && code < 58) && // numeric (0-9)
        !(code > 64 && code < 91) && // upper alpha (A-Z)
        !(code > 96 && code < 123)) { // lower alpha (a-z)
      return false;
    }
  return true;
};

charCodeAt(0);
```

### 📌 Recapitulação de Abordagem de Resolução de Problemas

Seja para uma entrevista ou por conta própria, você é desafiado a descobrir como resolver um problema. Esses são os passos que deveriam ser seguidos:

1. **Certifique-se de entender o problema**
    - Faça perguntas ao entrevistador, clarifique o problema. Certifique que você também o entendeu para pensar em uma solução, como a aplicação deve operar, como deve se comportar em todos os cenários e que isso acompanha o próximo passo.
2. **Explore exemplos concretos** 
    - Ambos os primeiros pontos são sobre entender o problema. Saber quais são as entradas, as saídas, os casos extremos, como lidar com erros que acontecem quando o usuário digita algo inválido. Entender como tudo deve funcionar desde o início.
3. **Quebre o problema**  
    - Neste ponto, se você quiser escrever como pseudo-código totalmente perfeito, linha por linha, pode fazer isso ou apenas seguir algumas etapas para definir um plano para o código que você precisa implementar. **Ajuda a saber para onde está indo antes mesmo de começar a digitar o código**.
4. **Resolva/Simplique**    
    - Se você não conseguir resolver o problema imediatamente, resolva um problema que possa. Mesmo que seja mais simples, se você simplificar, removerá algum desafio da dificuldade principal e tentará resolver algo em que possa reincorporar essa dificuldade principal novamente.
5. **Olhe para trás e refatore** 
    - Na maioria das vezes, há espaço para refatorar, mesmo se você for um desenvolvedor totalmente experiente.

