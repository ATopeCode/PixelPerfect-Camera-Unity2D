# PixelPerfect-Camera-Unity2D

Si eres desarrollador de videojuegos de la 'vieja' escuela, has usado XNA, MONOGAME, SDL... y quieres programar videojuegos 2D en 
Unity 3D, el primer inconveniente que encontrarás será que Unity es un motor 3D, aún cuando el proyecto sea 2D.
Cuando creas un proyecto 2D, Unity lo que hace es crear un proyecto 3D pero con cámara ortográfica, además de añadir varios componentes para trabajo en 2D, pero el motor del juego sigue siendo 3D.

Esto lo que produce es que nuestro 'sprites' o 'texturas' no se visualicen en pantalla en la posiciones y tamaños que nosotros queramos. Y tampoco tenemos la opción de seleccionar una resolución por defecto (320x200, 640x480...) para nuestro juego y adaptar
el tamaño de los sprites a dicha resolución.

Otro incoveniente que encuentro, si eres un programador de la vieja escuela es que ahora se acabó el fijar los FPS del juego. 
Es decir, antes, al final de cada ciclo de juego, se espera 'x' tiempo hasta que dicho ciclo durase el tiempo que le correspondía
según los FPS para los que se diseñaba. Esto evitaba que en ordenadores muy rápidos el juego fuera a toda leche. Lo que se consigue
es que el juego vaya a la misma velocidad en todos los equipos, lógicamente, si el ordenador es muy lento no hay nada que hacer y
el juego se verá relentizado.
Hoy en día se ha cambiado esta técnica por no utilizar la 'espera' al final de cada ciclo de juego. Lo que se hace es que el juego
va a su máxima velocidad en todos los equipos y el movimiento de los 'Sprites' y demás cálculos se hacen en función del 'deltaTime' o tiempo transcurrido desde el último ciclo de juego hasta el actual. Si sabes que tu sprite se moverá 1 punto en pantalla cada 0.10
segundos, solo tienes que multiplicar '0.10 * deltaTime' para saber desplazamiento tendrá en cada ciclo de juego.

PixelPerfectCamer.cs:
---------------------
Una clase 'Behavior' para añadir al gameObject de la 'Camara' de la Escena Unity.
Dándole valor a los campos del Behavior desde la escena unity se consigue obtener una resolución de pantalla que coincide con la resolución virtual del juego, es decir, si decidimos desarrollar nuestro juego en una resolución 320x200 el resultado en pantalla del juego será equivalente a cuando antiguamente se cambiaba la resolución de la tarjeta gráfica a 320x200.

El resultado visual es el mismo, lo que pasa es que nuestro dispositivo (pc, móvil...) mantiene su resolución pero la imagen del juego es 'escalada' en cada frame por Unity para que ocupe toda la pantalla.

Se obtiene 'PixelPerfect', es decir, se hace coincidir el tamaño de un punto o pixel de nuestros Sprites con el tamaño de 1 punto o pixel de nuestra 'resolución virtual' en pantalla. Para que se entienda mejor, si nuestra resolución virtual es de 320x200 y usamos en nuestro juego un sprite de ancho 320, al centrarlo en pantalla ocupará todo el ancho de la misma.

NOTA.- Para todas las texturas utilizadas en el juego, el campo 'PixelsPerUnits' debe conservar su valor por defecto '100'.

Con esta idea en cabeza el diseño de juegos se hace como se hacía antiguamente, se diseña el juego para una resolución de pantalla específica (320x200, 640x480 ...) que será nuestra 'resolución virtual' para poder saber de que tamaño deben ser los Sprites del juego o Tiles.

Además provee varios métodos para conversión de posiciones o coordenadas, ya que las posiciones de Unity son de tipo 'float' y las
de nuestra resolución virtual son tipo 'int'.
Si queremos hacer referencia a la posición (10,20) de nuestra 'resolución virtual' 320x200 por ejemplo, la posición 10 en el eje 'x' de unity no coincidirá con el punto/pixel nº10 de nuestra resolución virtual. Por defecto en Unity la posición 10 de nuestra resolución será la posición 0.10 y viceversa.
Utilizando los método de conversión de posiciones, en este caso: 

Vector3 posicion = new Vector3(10,20,0);
Vector3 posicionUnity = Position2DToWorld(posicion);

Conseguimos convertir las posiciones y desarrollar nuestro juego con una metodología 'PixelPerfect'. 
