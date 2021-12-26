# Día 4 - ¡Es hora de poner la navidad en casa!

> Creo que ya podemos sacar el gorro navideño, el turrón... ¡Y el árbol de navidad! 🎄 Vamos a montarlo con JavaScript.

Dificultad: Normal

## Enunciado

¡Es hora de poner el árbol de navidad en casa! 🎄

Para ello vamos a crear una función que recibe la altura del árbol, que será un entero positivo del 1 a, como máximo, 100.

Si le pasamos el argumento `5`, se pintaría esto:

```js
____*____
___***___
__*****__
_*******_
*********
____#____
____#____
```

Creamos un triángulo de asteriscos `*` con la altura proporcionada y, a los lados, usamos el guión bajo `_` para los espacios. Es muy importante que nuestro árbol siempre tenga la misma longitud por cada lado.
Todos los árboles, por pequeños o grandes que sean, tienen un tronco de dos líneas de `#`.

Otro ejemplo con un árbol de altura `3`:

```js
__*__
_***_
*****
__#__
__#__
```

Ten en cuenta que el árbol es un string y necesitas los saltos de línea `\n` para cada línea para que se forme bien el árbol.

## Solución

```js
function createXmasTree(height) {
  const SYMBOL = {
    LEAF: '*',
    GAP: '_',
    TRUNK: '#',
  }
  const tree = [];
  let width = 1;
  let emptyChars = height - 1;  
  let gap = SYMBOL.GAP.repeat(emptyChars);
  const trunk = gap + SYMBOL.TRUNK + gap;
  
  for (let i = 1; i <= height; i++) {
    let leafs = SYMBOL.LEAF.repeat(width);
    gap = SYMBOL.GAP.repeat(emptyChars);
    tree.push(gap + leafs + gap);
    width += 2;
    emptyChars--;
  }
  tree.push(trunk);
  tree.push(trunk);  
  
  return tree.join('\n');
}
```
