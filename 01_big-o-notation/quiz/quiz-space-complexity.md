### Pergunta 1:

Determine the space complexity for the following function

```js
function logUpTo(n) {
  for (var i = 1; i <= n; i++) {
    console.log(i);
  }
}
```

- <span style="color:green">0(1)</span>
- 0(n)
- 0(n log n)

### Pergunta 2:

Determine the space complexity for the following function

```js
function logAtMost10(n) {
  for (var i = 1; i <= Math.min(n, 10); i++) {
    console.log(i);
  }
}
```

- <span style="color:green">0(1)</span>
- 0(n)
- 0(n log n)

### Pergunta 3:

Determine the space complexity for the following function

```js
function logAtMost10(n) {
  for (var i = 1; i <= Math.min(n, 10); i++) {
    console.log(i);
  }
}
```

- <span style="color:green">0(1)</span>
- 0(n)
- 0(n log n)

### Pergunta 4:

Determine the space complexity for the following function

```js
function onlyElementsAtEvenIndex(array) {
  var newArray = Array(Math.ceil(array.length / 2));
  for (var i = 0; i < array.length; i++) {
    if (i % 2 === 0) {
      newArray[i / 2] = array[i];
    }
  }
  return newArray;
}
```

- <span style="color:green">0(n)</span>
- 0(n log n)
- 0(n^2)

### Pergunta 5:

Determine the space complexity for the following function

```js
function subtotals(array) {
  var subtotalArray = Array(array.length);
  for (var i = 0; i < array.length; i++) {
    var subtotal = 0;
    for (var j = 0; j <= i; j++) {
      subtotal += array[j];
    }
    subtotalArray[i] = subtotal;
  }
  return subtotalArray;
}
```

- 0(n)
- 0(n^2)
- <span style="color:green">0(n)</span>
