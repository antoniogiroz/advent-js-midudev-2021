# Día 23 - ¿Puedes reconfigurar las fábricas para no parar de crear regalos?

> Santa Claus quiere las máquinas funcionando las 24 horas, como si esto fuera una rave de Pocholo. Chiki pun chiki pun. ¡Ayúdale a conseguirlo!

Dificultad: Muy difícil

## Enunciado

Estamos en la fábrica de Santa Claus 🎅 creando regalos como si no hubiera un mañana.

Pensábamos que no íbamos a llegar pero **Jelf Bezos** ha tenido una idea genial para aprovechar las máquinas y optimizar al máximo la creación de regalos. 🎁

La configuración de las máquinas es un **string**. Podemos reconfigurarla para que haga otro regalo y, para ello, podemos cambiar cada carácter por otro.

Pero **tiene limitaciones** 🥲: al reemplazar el carácter se debe mantener el orden, no se puede asignar al mismo carácter a dos letras distintas (pero sí a si mismo) y, claro, la longitud del string debe ser el mismo.

Necesitamos **una función que nos diga si podemos reconfigurar una máquina para que de un regalo pueda pasar a fabricar otro según las reglas** mencionadas. Lo mejor es que veamos un ejemplo:

```js
const from = 'BAL'
const to   = 'LIB'
const canReconfigure(from, to) // true
/* la transformación sería así:
B -> L
A -> I
L -> B
*/

const from = 'CON'
const to   = 'JUU'
const canReconfigure(from, to) // false
/* no se puede hacer la transformación:
C -> J
O -> U
N -> FALLO
*/

const from = 'XBOX'
const to   = 'XXBO'
const canReconfigure(from, to) // false
/* no se puede hacer la transformación:
X -> X
```

## Solución

```js
function hasOnlyOneAsignPerChar(origin, dest) {
  const charCounters = {};

  origin.forEach((char, index) => {
    charCounters[char] ||= new Set();
    charCounters[char].add(dest[index]);
  });
  
  return Object.values(charCounters).every(counter => counter.size === 1);
}

function canReconfigure(from, to) {
  if (from.length !== to.length) {
    return false;
  }

  const fromChars = from.split('');
  const toChars = to.split('');
  
  return hasOnlyOneAsignPerChar(fromChars, toChars) && hasOnlyOneAsignPerChar(toChars, fromChars);
}
```
