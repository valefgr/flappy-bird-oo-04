# Flappy Bird Parte 4

## Introducción

En el lab anterior lograste que `bird` se mueva al presionar una tecla. En este lab vamos a agregar más código JavaScript para que cuando `bird` tenga una colisión con el suelo, el juego se termine y los efectos del juego paren.

## Instrucciones

Agrega los siguientes métodos dentro de `script.js`. Las descripciones para los métodos y propiedades del objeto bird y juego se encuentran más abajo en este README.

1. Agrega el método `bird.colision`
2. Agrega el método `juego.verificaColision `
3. Llama al método `juego.verificaColision()` dentro del método juego.loop
4. Agrega el método `juego.mostrarGameover`
5. Agrega el método `juego.pararEfectos`
6. Agrega el método `juego.terminar`


## El objeto juego

### Propiedades:
1. `timerId`
- **¿Qué valor tiene?**: `juego.timerId` tiene como valor el numero `0` (para iniciar)
- **¿Dónde se utiliza?**: `juego.timerId` se utilizará dentro de `juego.inicar()` para guardar un timer que llame cada 20 milisegundos a `juego.loop`

2. `gravedad`
- **¿Qué valor tiene?**: `juego.gravedad` tiene como valor el numero `2`
- **¿Dónde se utiliza?**: La variable `gravedad` representa el numero de pixeles que se restarán a `bird.bottom` cuando se aplique el método `bird.efectoGravedad()`


### Métodos:
1. `aleatorio()` 
- **¿Qué hace?**: Devuelve un numero aleatorio entre un minimo y máximo dado
- **¿Dónde se utiliza?**: `bird.bottom` llamará a `juego.aleatorio()` para calcular un numero aleatorio entre `10` y `570`


2. `verificaColision()`
- **¿Qué hace?**: Llama a `bird.colision()` para revisar si `bird` tuvo una colision. Si `bird.colision()` devuelve el valor `true`, llama a `juego.terminar()` para terminar el juego.
- **¿Dónde se utiliza?**:  `juego.loop()` llamará a `juego.verificaColision()` para revisar constantemente si hubo una colisión.  


3. `loop()`
- **¿Qué hace?** :Llama a `bird.efectoGravedad()`, `bird.dibujar()` y `juego.verificaColision()`
- **¿Dónde se utiliza?**: `juego.iniciar()` inicia un `setInterval()` que llama a `juego.loop()` cada 20 milisegundos. De ésta manera cada 20 milisegundos se aplicará el efecto de gravedad a bird, se dibujará bird en su nueva posicion, y se verificará si hubo una colisión


4. `iniciar()`
- **¿Qué hace?** : Agrega un eventListener de tal forma que cada que se pulse una tecla, se llame a `bird.move`. También asigna a `juego.timerId` un `setInterval()` que llame a `juego.loop()` cada 20 milisegundos. 
- **¿Dónde se utiliza?**: `juego.iniciar()` se tiene que llamar para iniciar el juego. A través del `setInterval()` cada 20 milisegundos se aplicará el efecto de gravedad a `bird`, se dibujará `bird` en su nueva posicion, y se verificará si hubo una colisión. A través del eventListener, se puede mover `bird`

5. `terminar()`
- **¿Qué hace?**: Limpia el timer guardado dentro de `game.timerId` (el que llama cada 20 milisegundos a `game.loop`). También, llama a `juego.mostrarGameOver()` y `juego.pararEfectos()`. 
- **¿Dónde se utiliza?**: El metodo `juego.terminar()` se llama cuando hay una colision


6.  `mostrarGameover()`
- **¿Qué hace?**:  Agrega el id "game-over" al elemento html con clase `.message`
- **¿Dónde se utiliza?**: `juego.terminar()` llama a `juego.mostrarGameOver` para mostrar el mensaje "Game Over" cuando el juego termina

7. `pararEfectos()`
- **¿Qué hace?**: quita el id al elemento con clase `.ground`. También agrega el id "fall" al div con clase `.bird`
- **¿Dónde se utiliza?**: `juego.terminar()` llama a `juego.pararEfectos()` para que bird deje de aleatear y el suelo deje de moverse 


## El objeto bird:

### Propiedades
1. `div`
- **¿Qué valor tiene?**: `bird.div` tiene como valor el elemento html con clase `.bird`
- **¿Dónde se utiliza?**: `bird.div` se utiliza dentro del método `bird.dibujar` de tal forma que se pueda dibujar el elemento en posiciones determinadas

2. `bottom`
- **¿Qué valor tiene?**: `bird.bottom` tiene un valor aleatorio entre `10` y `570`. Para calcular este valor aleatorio `bird.bottom` utiliza el método `juego.aleatorio()`
- **¿Dónde se utiliza?**:  El valor de `bird.bottom` basicamente determina en donde se va a posicionar el elemento `bird`. Por lo tanto `bird.bottom` se utiliza en los metodos `bird.efectoGravedad()`, `bird.dibujar()`, `bird.mover()` y `bird.colision()`

3. `left`
- **¿Qué valor tiene?**: `bird.left` tiene como valor el numero `250`
- **¿Dónde se utiliza?**: `bird.left` se utiliza dentro de `bird.dibujar()`. El valor de bird.left basicamente determinará el numero de pixeles a la izquierda del elemento con clas `.bird`

4. `width`
- **¿Qué valor tiene?**: `bird.width` tiene como valor el numero `60`
- **¿Dónde se utiliza?**: El valor de de `bird.width` se utilizará más adelante para determinar si hubo una colision entre `bird` y los `obstaculos`

5. `height`
- **¿Qué valor tiene?**: `bird.height` tiene como valor numero `45`
- **¿Dónde se utiliza?**: El valor de de `bird.height` se utilizará más adelante para determinar si hubo una colision entre `bird` y los `obstaculos`

### Métodos:

1. `efectoGravedad()`
- **¿Qué hace?**: `bird.efectoGravedad()` disminuye la propiedad `bird.bottom` por el valor de `juego.gravedad`
- **¿Dónde se utiliza?**: `juego.loop()` llama a `bird.efectoGravedad()`. Recuerda que `juego.loop()` se llama cada 20 milisegundos a través de `juego.iniciar()`. 

2. `dibujar()`
- **¿Qué hace?**: `bird.dibujar()` asigna a la propiedad bottom de `bird.div` (el elemento html con clas bird) el valor en pixeles de la propiedad `bird.bottom`
- **¿Dónde se utiliza?**: `juego.loop()` llama a `bird.dibujar()`. Recuerda que `juego.loop()` se llama cada 20 milisegundos a través de `juego.iniciar()`. 

3. `mover()`
- **¿Qué hace?**: `bird.mover()` agrega `40` a `bird.bottom`
- **¿Dónde se utiliza?**: `juego.iniciar()` agrega un eventListener de tal forma que cuando se pulse una tecla, se llame a `bird.mover()`

4. `colision()`
- **¿Qué hace?**: `bird.colision()` revisa si `bird.bottom` es menor a `0`. Si eseto es verdad, devuelve el valor `true`
- **¿Dónde se utiliza?**: `juego.verificaColision()` llama a `bird.colision()` para verificar si hubo una colision.

