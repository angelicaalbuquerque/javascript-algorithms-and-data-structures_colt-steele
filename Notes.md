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

> Dizemos que um algortimo é _O(f(n))_ se o número de operações simples a serem executadas for eventualmente menor que uma constante vezes _f(n)_, enquanto _n_ cresce.

Relacionamento de um input de _n_ com o tempo de execução:

- f(n) pode ser linear (f(n) = n) _enquanto n cresce, o tempo de execução cresce linearmente_;
- f(n) pode ser quadrática (f(n) = n²) _enquanto n cresce, o tempo de execução cresce quadráticamente_;
- f(n) pode ser constante (f(n) = 1) _enquanto n cresce, o tempo de execução não cresce e não é impactado, pois é sempre constante_;
- f(n) pode ser algo totalmente diferente!
