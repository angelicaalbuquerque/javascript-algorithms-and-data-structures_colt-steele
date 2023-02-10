### Pergunta 1:

Simplify the big O expression as much as possible - O(n + 10)

- <span style="color:green">O(n)</span>
- O(n^2)
- O(n log n)

### Pergunta 2:

Simplify the big O expression as much as possible - O(100 \* n)

- O(n2)
- O(1)
- <span style="color:green">O(n)</span>

### Pergunta 3:

Simply the following big O expression as much as possible - O(25)

- O(n)
- O(n!)
- <span style="color:green">O(1)</span>

### Pergunta 4:

Simply the following big O expression as much as possible - O(n^2 + n^3)

- <span style="color:green">O(n^3)</span>
- O(n)
- O(n^2)

### Pergunta 5:

Simply the following big O expression as much as possible - O(n + n + n + n)

- O(4n)
- <span style="color:green">O(n)</span>
- O(n^2)

### Pergunta 6:

Determine the time complexity for the following function

```js
function logUpTo(n) {
  for (var i = 1; i <= n; i++) {
    console.log(i);
  }
}
```

- <span style="color:green">O(n)</span>
- O(n^2)
- O(n log n)

### Pergunta 7:

Determine the time complexity for the following function

```js
function logAtMost10(n) {
  for (var i = 1; i <= Math.min(n, 10); i++) {
    console.log(i);
  }
}
```

- <span style="color:green">O(1)</span>
- O(n)
- O(n^2)

### Pergunta 8:

Determine the time complexity for the following function

```js
function logAtLeast10(n) {
  for (var i = 1; i <= Math.max(n, 10); i++) {
    console.log(i);
  }
}
```

- <span style="color:green">O(n)</span>
- O(1)
- O(n log n)

### Pergunta 9:

Determine the time complexity for the following function

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

- <span style="color:green">1 | 0(n)</span>
- 1 | 0(1)
- 1 | 0(n^2)

### Pergunta 10:

Determine the time complexity for the following function

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
- 0(1)
- <span style="color:green">0(n^2)</span>
