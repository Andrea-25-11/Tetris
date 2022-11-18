# Tetris
EXPLICACIÓN TETRIS.JS

Para la realización de este tetris nos basamos en un repositorio previamente existente y le realizamos ciertas modificaciones que eran pertinentes para tener un código más entendible y prolijo, entre los primeros cambios del HTML realizamos los siguientes:

HEAD:
Eliminacion link de referencias a las librecias CSS de bootstrap
Cambio en el nombre del título
Insertamos link de fonts de google y un link para para que apareciera un icono en la pestaña
Linkeado del css creado posteriormente y linkeado de iconos de fontawesome. 

BODY   
En el MAIN realizamos cambios en el contenido del texto del h1y agregamos clases al h1 y al h2; En el FOOTER realizamos cambio en el contenido del texto y finalmente dentro de las etiquetas de SCRIPT eliminamos varios linkeados de scripts innecesarios que llamaban las librerías de sweetalert ya que traían un código compilado de difícil interpretación

Luego realizamos la creación de la hoja de styles.css, en ella aplicamos estilos para el color del fondo insertando una imagen, añadimos estilos a los botones para que tuvieran un espaciado entre ellos y los alineamos al lado derecho del tablero siempre y cuando la media query aplicada fuera en una pantalla mayor a 850px, de lo contrario posicionamos los botones de manera paralela al tablero.
Para hacer responsive manejamos dos rangos. El de celular que iría desde 0px a un máximo de 480 y el segundo de 481px a 850px. En dichos intervalos realizamos cambios en el tamaño de la letra y en el ancho y alto de los botones.

Respecto del archivo de Tetris.js analizamos que se encuentra estructurado en 4 grandes clases siendo éstas:

1.Class Game
2.Class Utils
3.Class Point
4.Class Tetromino

Cada una de ellas a su vez contiene diferentes elementos que permiten el correcto despliegue del juego tetris, usando métodos, static o constructores. Por medio del presente documento se pretende dar explicación a cada uno de dichos elementos para entender la funcionalidad que aportan al juego mediante el lenguaje de programación de JavaScript.

Para tales fines se separará la explicación según clase.

---------------------------------- CLASS GAME -------------------------------

----------------------------------- STATIC ---------------------------------

STATIC: La palabra clave static define un método estático para una clase
SQUARE_LENGHT =
Mediante éste método la medida del cuadrado depende del tamaño de la pantalla por ejemplo si la pantalla es mayor a 420px va a ser de 30px o si no de 20 px respectivamente, logrando así la adaptación del tablero.

COLUMNS = Número de columnas que tiene el canva, éste varía según el tamaño  de la pantalla donde se inicie el juego.

ROWS = Número de filas que conforman el tablero.

CANVAS_WIDTH y CANVAS_HEIGHT = Por medio de este código se determina el ancho y alto del tablero de tetris , teniendo en cuenta el ancho de la pantalla y el número de filas y columnas.

EMPTY_COLOR = Ésta variable indica el color del fondo del tablero.

BORDER_COLOR = Mediante ésta variable se establece el color de los bordes y las líneas que dividen el tablero en filas y columnas.

DELETED_ROW_COLOR = Ésta variable establece el color que toma la fila durante el juego, cuando el jugador complete una fila, toma éste color declarado antes de eliminarse y sumar los puntos correspondientes.

TIMEOUT_LOCK_PUT_NEXT_PIECE = Ésta variable determina el Tiempo en que se demora en aparecer la otra ficha, es establecido en microsegundos.

PIECE_SPEED = Indica la Velocidad en que baja la ficha entre menor sea el número , bajara mas rapido.

DELETE_ROW_ANIMATION  = Indica tiempo en el que se demora una fila en desaparecer cuando  se complete.

PER_SQUARE_SCORE = Guarda el valor del puntaje asignado por cada cuadro que se elimine.

COLORS = Éste array contiene la lista de los colores que dibujaran las piezas en el tablero, estos serán llamados de forma aleatoria igual que las piezas que conforman el juego.

-------------------------- CONSTRUCTOR -----------------------------------------

CONSTRUCTOR: El método constructor es un método especial para crear e inicializar un objeto creado a partir de una clase. Los objetos en JavaScript son colecciones dinámicas de pares clave-valor.
Mediante este constructor se crearon 11 objetos a los cuales se les asignó un valor, la funcionalidad de cada uno de ellos recae de la siguiente manera:
Se creó un constructor con el parámetro de canvadId el cual posee varias variables cuyo valor se ve reflejado en booleanos, arrays, números, null o métodos.

------------------------- MÉTODOS ----------------------------------------------

MÉTODO: Se manejaron 40 en la clase de Game

init(){};
Este método posee en su interior 6 métodos a ejecutar facilitando en primer medida un saludo de bienvenida, inicializar los elementos del DOM(Muestra los botones del juego), reproducir el sonido del juego, resetearlo si se quiere, permitir dibujar los tetriminos y el tablero del juego, permite el uso de los controles del juego como lo son las flechas y otros botones como pausa o rotar.
resetGame(){};
Posee 7 métodos en su interior junto con 3 variables con dato de tipo numérico.
En este método se asigna un valor de 0 al puntaje.
Se llama al valor de sound decretado en el constructor para que el sonido se ejecute al completar una línea o pausarlo si se desea y también para ejecutar el sonido de fondo del juego en general y pausarlo si así se desea.
Así mismo empiezan a aparecer las fichas en el tablero, elegir una figura aleatoria, restablece la posición inicial de las piezas en X y Y, limpia el tablero de las piezas que estaban con anterioridad, refresca el puntaje y se deja el juego en pausa para volver a iniciar.

showWelcome(){};
En este método se muestra una alerta de bienvenida con las instrucciones del juego 

initControls(){};
Permite añadirle un addEventListener de tipo keydown a los botones que se van a utilizar en el juego mediante el teclado, utilizando un arrow function en donde se utiliza una condicional de if junto con 5 switch cases.

Esta condición dice que la variable decretada en el constructor con el nombre de canPlay cambia su valor a true y que se llame al parámetro code que hace referencia a las direcciones que puede seguir la tecla.

De tal manera, indica que: Si estoy jugando y presiono la tecla a la derecha no es igual a pausar, en cambio solicita retornar lo señalado dentro del switch case respectivo por ejemplo attemptMoveRight. Este método tiene los mismos efectos utilizando las demás teclas al presionarlas. Al final se solicita ejecutar el método de syncExistingPiecesWithBoard explicado más abajo (Método 22)

Por otra parte, también se añade un addEventListener de tipo “click” el cual va a ejecutarse al clickear sobre los botones creados en pantalla mediante el HTML. De tal manera, aplica dicho evento sobre el botón identificado en el HTML con el Id respectivo, siendo llamado mediante una variable decretada en el JS dentro del método initDomElements, en donde se llama dicho botón mediante el document.querySelector. Ahora bien al darle click solicita ejecutar el método attemptMoveDown, attemptMoveRight entre otros según corresponda. Si se trata del botón de pausa o resume, solicita que se ejecute el mismo método alusivo a pauseOrResumeGame.


attemptMoveRight(){};
Inicialmente se decreta un método en el cual se aplica una condicional de if. En dicha condicional se llama otro método llamado figureCanMoveRight y se señala que si se cumple con lo decretado dentro de dicho método, se genere un incremento en 1 a la variable decretada en el constructor llamada globalX que inicialmente tenía valor de 0. Es entonces que la figura se moverá una casilla a la derecha.

attemptMoveLeft(){};
Inicialmente se decreta un método en el cual se aplica una condicional de if. En dicha condicional se llama otro método llamado figureCanMoveLeft y se señala que si se cumple con lo decretado dentro de dicho método, se genere un decremento en 1 a la variable decretada en el constructor llamada globalX que inicialmente tenía valor de 0. Es entonces que la figura se moverá una casilla a la izquierda.

attemptMoveDown(){};
Inicialmente se decreta un método en el cual se aplica una condicional de if. En dicha condicional se llama otro método llamado figureCanMoveDown y se señala que si se cumple con lo decretado dentro de dicho método, se genere un incremento en 1 a la variable declarada en el constructor llamada globalY que inicialmente tenía valor de 0. Es entonces que la figura se moverá una casilla hacia abajo.

attemptRotate(){};
Se decreta un método el cual solicita ejecutar el método de rotateFigure el cual será explicado más abajo (Método 39)

pauseOrResumeGame(){};
Se declara un método con un condicional de if junto con un else. Se dice que si el juego está corriendo, el botón de iniciar se esconde y el de pausar se muestra. De lo contrario, si el juego está pausado el botón de iniciar se muestra y el de pausa se oculta. 
Nota: hidden = false indica que no se esconda el elemento y el hidden = true indica que si se esconda el elemento.
 
pauseGame(){};
Declara un método donde se llaman 3 variables del constructor siendo que: el sonido del juego en sí se pausa, el juego también se pausa es decir se mantiene el valor de true y también se mantiene el valor de false en la variable del canPlay, para finalizar crea una función llamada clearInterval la cual llama a intervalId decretada en el constructor como parámetro. Este intervalId permite que la pieza vaya bajando pero en este caso como el juego se pausa el clearInterval limpia el intervalo para no permitir seguir bajando la pieza.

resumeGame(){};
Este método declara volver a retomar el sonido, se llama el método refreshScore el cual permite seguir mostrando el puntaje que se ha acumulado durante el juego y permitir que se sigan sumando más puntos durante el progreso del juego; A las variables declaradas en el constructor se les indica que a la pausa se le cambia el valor de true a false es decir el juego deja de estar pausado y el canPlay cambia su valor de false a true para que el juego tenga continuidad. Para finalizar la variable declarada en el constructor llamada intervalidId permite que el intervalo de tiempo en términos de velocidad (uno de los static declarados al principio con el nombre de PIECE_SPEED)en la que baja la ficha se mantenga constante.
 
moveFigureToExistingPieces(){};
Este metodo mantiene una posicion fija de la ficha al bajar tanto en y como en x, tiene el cuenta la posicion global del tablero. De igual manerala ficha al tocar el fondo mantiene el color que traía. Se llama al metodo restartGlobarXandY la cual indica que cuando la ficha toca el punto límite sale la nueva ficha.

playerLoses(){};
En esta función se define un bucle de tipo for, en donde cada vez que las piezas existentes en el tablero alcanzan la altura de la penúltima fila (y, 1) el jugador va a perder y el juego se va a reiniciar gracias al return que especifica finalizar la función.

getPointsToDelete(){};
Se crea una lista vacía con el nombre points y una variable let “y”en cero el cual es el contador. Se ejecuta un bucle for en el cual se evalúa que si la fila está llena, los puntos de la variable let en cero se van a aumentar en 1 cuya sentencia será retornar los puntos.
El every lo que hace es verificar si se está cumpliendo una condición o no 
El push envia los puntos a la lista vacía y va sumando de a 1 punto por cada casilla.
changeDeletedRowColor(){};
En este método llama al constructor existingPieces en las coordenadas en “y” permite que al eliminar la fila dicha fila adquiera un nuevo color que fue determinado en el static de DELETED_ROW_COLOR 

addScore(){};
Operador aritmético que al valor del score le suma 1 por fila con 
y se actualiza el puntaje.

removeRowsFromExistingPieces(){};
Se elimina la fila del todo y vuelve el color por defecto del tablero, y permite desplazar la siguiente fila del tetris,  si se pone true no quita la fila y no permite bajar el juego aunque se elimine en términos de coloración la fila eliminada.

verifyAndDeleteFullRows(){};
Se verifica si hay lugar a que se elimine una fila completa, si es asì reproduce el sonido de succes y la fila eliminada cambia de color de agregando así la animacion. Luego se pausa el sonido del success y se elimina la fila completada.Luego hace un recorrido de las filas y las columnas y demarca el límite del marco para posicionar las fichas que van cayendo.

mainLoop(){};
Método que se repite constantemente en el juego para revisar si la ficha se puede mover o no. Si la ficha tiene límite de contacto no puede seguir bajando, si ya no se puede mover ejecuta el sonido del tap. También muestra el alert si pierde, el sonido se pausa, no se puede jugar más y se resetea y se sincronizan las piezas. El  Game.time out, es el tiempo en el que se demora en aparecer la otra ficha. y el sync lo usa para q se estén sincronizando las fichas continuamente con el tablero

cleanGameBoardAndOverlapExistingPieces(){};
Usado para limpiar el tablero, al momento en el que se pierde el color del tablero retorna a su color inicial

overlapCurrentFigureOnGameBoard(){}; superposición de la figura actual en el tablero de juego: Éste método superpone la pieza actualmente dibujada en el tablero sobre alguna pieza existente o en el fondo del tablero, dándole la ubicación en "Y" y "X" , también especifica que cuando esto ocurra se mantenga el color aleatorio de la pieza para poder distinguirse en el tablero.

syncExistingPiecesWithBoard(){};sincronizar piezas existentes con el  tablero: éste método llama las funciones de limpiar el tablero de juego(si se pierde el juego lo deja del color inicial lo que el usuario mirará será el tablero vacío para jugar nuevamente, si el usuario no ha perdido, proyecta la siguiente pieza y mantiene dibujadas las piezas existentes en el fondo del tablero) y también llama la función de superponer la figura actual, dejando ver en el tablero las que ya se han posicionado.

draw(){};
Se dibuja el tablero y lo actualiza cada 17 milisegundos. El requestanimation frametiene como funcion repintar el cuadro cada ciclo

refreshScore(){};
Se utiliza un nodo que se va actualizando a medida que se van agregando más puntos.

initSounds(){};
Define 4 variables de los 4 sonidos que se van a utilizar en el tetris 

initDomElements(){};
Mediante este método se decretan las variables que se llaman mediante el document.querySelector a los nodos identificados con los ID de los botones a utilizar en el juego. Así mismo se decretaron atributos para el ancho y largo del canvas en la medida pixeles y se declaró que el contexto de la dimensión del canvas sea en segunda dimensión.

chooseRandomFigure(){};
En este método se llama a la variable decretada en el constructor como currentFigure y pasa de null a cambiarle su valor al método getRandomFigure el cual crea las figuras de tetriminos

restartGlobalXAndY(){};
Ajusta la posición en la que van a salir las fichas en x y y dividiendo las columnas en 2 para encontrar el punto medio de salida.

getRandomFigure(){};
Crea las figuras indicando su posicionamiento en “x” & “y” y sus posibles rotaciones.

initBoardAndExistingPieces(){};
Se limpia constantemete el tablero para que las piezas puedan desplazarse, verifica los espacios existente en el eje y y x, si no hay espacios disponibles el juego se acába, es decir limita el tablero

relativePointOutOfLimits(){};
Se establece una posición relativa para las piezas. Detecta las colisiones, determina el máximo tope que puedan tener las fichas en x y en y.

absolutePointOutOfLimits(){};
Establece una operación matemática para señalar el límite de las piezas para moverse dentro del canva

isEmptyPoint(){};
Este método realiza la verificación de las piezas existentes en “y” y en “x” señalando que si no hay piezas existentes se retorne true, de lo contrario, si sí hay piezas en “y” o “x” se entienda que están tomadas (taken) y se retorne falso.

isValidPoint(){};
Verifica la posición de la pieza tanto en x como en y así declara que la ficha tiene una posición tomada para que no se superpongan unas con otras.

figureCanMoveRight
Se evalua si cada uno de los cuadritos que conforma el tetromino pueden moverse a la derecha, si es true va a aumentar x en 1, de lo contrario, no se hace dicho movimiento si no cuenta con el espacio para ello, retorna false.

figureCanMoveLeft
Se evalua si cada uno de los cuadritos que conforma el tetromino pueden moverse a la izquierda, si es true va a disminuir x en 1, de lo contrario, no se hace dicho movimiento si no cuenta con el espacio para ello, retorna false.

figureCanMoveDown
Se evalua si cada uno de los cuadritos que conforma el tetromino pueden moverse hacia abajo, si es true va a aumentar y en 1, de lo contrario, no se hace dicho movimiento si no cuenta con el espacio para ello, retorna false

figureCanRotate
Tiene en cuenta si la rotacion que va a hacer se hará hacia un punto válido si no es posible retorna false y no se rota.

rotateFigure
Señala que si la figura no se puede rotar se ejecute el sonido de denied de lo contrario que se pueda rotar sin reporoducir ningun sonido adicional

async askUserConfirmResetGame()
Crea un alert que resetea el juego. La declaración de función async define una función asíncrona, la cual devuelve un objeto AsyncFunction.




---------------------------------- CLASS UTILS -------------------------------

Esta contiene funciones que van a ser reutilizadas a lo largo de la ejecución del juego. Contiene 3 statics el primero de ellos getRandomNumberInRange genera un número aleatorio que va ser utilizado dentro del static getRandomColor , la manera en la que estas funciones se vinculan es que el número generado aleatoriamente en la función getRandomNumberInRange hará alusión al posicionamiento del color establecido en el array de COLORS para escoger el color de la pieza siguiente a caer.
También se encuentra al static loadSound que permite que cargue el sonido de manera automatica sin utilización de controles. 



---------------------------------- CLASS POINT -------------------------------

Esta clase contiene un constructor que tiene como parámetro el eje x y y


---------------------------------- CLASS TETROMINO -------------------------------


En ésta clase se aplican las rotaciones que son las figuras que representan al tetromino(forma geométrica compuesta por 4 cuadrados iguales),posee un constructor que recibe las rotaciones posibles que puede tener el tetromino. Se llama también al get point, se aplica un color aleatorio mediante el método getrandomcolor y se indica que para cada punto de rotación se utiliza el foreach aplicando un color aleatorio a cada punto indicado por la coordenada Y y X, y por último, tomando en cuenta que se cambia la rotación se incrementa el índice de rotación del tetromino.







