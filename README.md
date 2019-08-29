# Memory API
En este laboratorio ganará algún grado de familiaridad con la asignación de memoria (memory allocation). Para el caso, ustedd escribirá algunos programas con bugs. Luego, usará algunas herramientas para localizar los bugs que usted ha insertado. De este modo se familiarizará con algunas de estas herramientas para un uso futuro. Estas herramientas son: el debuger (gdb) y el memory-bug detector (valgrind).

## Questions

1. Escriba un programa simple llamado null.c que cree un puntero a un entero, llevelo a null y entonces intente desreferenciarlo (esto es, asignarle un valor). Compile este programa llamado null. ¿Qué pasa cuando usted ejecuta este programa?

Cuando se ejecuta el programa en la consola sale Segmentation fault (core dumped), lo que quiere decir es que hay un error al momento de acceder a la memoria, pues se tiene un apuntador sin una dirección para referenciar.
![alt tag](https://github.com/Jeroquendo/SO/blob/master/imagenes/null.png)

2. Compile el programa del ejercicio anterior usando información de simbolos (con la flag -g). Al hacer esto se esta poniendo mas informacion en el ejecutable para permitir al debugger acceder a informacion util sobre los nombres de las variables y cosas similares. Ejecute el programa bajo el debugger digitando en consola (para el caso) gdb null y entonces una vez el gdb este corriendo ejecute run. ¿Qué muestra gdb?

El gdb muestra en que linea se generó el Segmentation fault, en este caso en la linea 6.
![alt tag](https://github.com/Jeroquendo/SO/blob/master/imagenes/punto2.png)

3. Haga uso de la herramienta valgrind en el programa empleado en los puntos anteriores. Se usará la herramienta memcheck que es parte de valgrind para analizar lo que pasa: valgrind --leak-check=yes null. ¿Qué pasa cuando corre esto?, Â¿Puede usted interpretar la salida de la herramienta anterior?

La herramienta memcheck está encargada de detectar los errores en memoria, nos muestra el problema en la linea 6 en el programa. Este error causa que en el stack haya un overflow.
![alt tag](https://github.com/Jeroquendo/SO/blob/master/imagenes/punto3.png)

4. Escriba un programa sencillo que asigne memoria usando malloc() pero olvide liberarla antes de que el programa termina. ¿Qué pasa cuando este programa se ejecuta?, ¿Puede usted usar gdb para encontrar problemas como este?, ¿Que dice acerca de Valgrind (de nuevo use este con la bandera --leak check=yes)?

Se ejecuta el programa y no hay ningún problema.
![alt tag](https://github.com/Jeroquendo/SO/blob/master/imagenes/punto4.1.png)

Utilizando el gdb no muestra ningun error y se ejecuta bien.
![alt tag](https://github.com/Jeroquendo/SO/blob/master/imagenes/punto4.2.png)

Utilizando valgrind muestra cuanta memoria separó en el heap (4 bytes).
![alt tag](https://github.com/Jeroquendo/SO/blob/master/imagenes/punto4.3.png)

5. Escriba un programa que cree un array de enteros llamado data de un tamaño de 100 usando malloc; entonces, lleve el data[100] a 0. ¿Qué pasa cuando este programa se ejecuta?, ¿Qué pasa cuando se corre el programa usando valgrind?, ¿El programa es correcto?

El programa se ejecuta correctamente.
![alt tag](https://github.com/Jeroquendo/SO/blob/master/imagenes/punto5.1.png)

Usando valgrind muestra un error en la memoria, el cual consiste en la asginacion fuera de rango
![alt tag](https://github.com/Jeroquendo/SO/blob/master/imagenes/punto5.2.png)

6. Codifique un programa que asigne un array de enteros (como arriba), luego lo libere, y entonces intente imprimir el valor de un elemento del array. ¿El programa corre?, ¿Que pasa cuando hace uso de valgrind?

El programa se ejecuta correctamente.
![alt tag](https://github.com/Jeroquendo/SO/blob/master/imagenes/punto6.1.png)

Utilizando valgrind, muestra un error en el que se liberó un elemento del array aunque ya se había leido.
![alt tag](https://github.com/Jeroquendo/SO/blob/master/imagenes/punto6.2.png)

7. Ahora pase un funny value para liberar (e.g. un puntero en la mitad del array que usted ha asignado) ¿Qué pasa?, ¿Ústed necesita herramientas para encontrar este tipo de problemas?

Al ejecutarlo aparece un error invalid pointer.
![alt tag](https://github.com/Jeroquendo/SO/blob/master/imagenes/punto7.1.png)

Utilizamos la herramienta valgrind, la cual detecta 2 errores generados por el apuntador. Al momento de ejecutarlo igual se mostró el problema.
![alt tag](https://github.com/Jeroquendo/SO/blob/master/imagenes/punto7.2.png)
