# TallerDisenoAREP
Nombre: Alexandra Moreno Latorre 

---
### Agrega esto
Funciones de ordenamiento:
Sus servicios  deben incluir dos funciones. 
Uno recibe una lista de cadenas y un valor a buscar e implementa la búsqueda lineal :  linearSearch(lista, valor) retorna un json con el índice de la primera aparición del valor o con -1 si no encuentra el valor
Uno recibe una lista ordenada de cadenas y un valor a buscar e implementa la búsqueda binaria de manera recursiva : binarySearch(n), retorna un json con el índice de la primera aparición del valor o con -1 si no encuentra el valor.
PARA AMBAS IMPLEMENTACIONES ESCRIBA EL ALGORITMO. Usted debe implementar las dos funciones, no debe usar funciones de una librería o del API (si ya existen).
 
 
La búsqueda lineal y la búsqueda binaria son dos algoritmos fundamentales utilizados para encontrar un elemento específico en un conjunto de datos. Aquí te describo en detalle cómo funcionan estos dos algoritmos:

Búsqueda Lineal
La búsqueda lineal, también conocida como búsqueda secuencial, es un método simple y directo para encontrar un elemento en un conjunto de datos. Funciona de la siguiente manera:

Inicio: Comenzar desde el primer elemento del conjunto de datos.
Comparación: Comparar cada elemento con el valor buscado.
Resultado:
Si el elemento actual es igual al valor buscado, se retorna la posición de ese elemento, indicando así que el elemento ha sido encontrado.
Si el elemento actual no es igual al valor buscado, se pasa al siguiente elemento.
Finalización: Este proceso continúa hasta que se encuentra el elemento o se ha recorrido todo el conjunto de datos.
No encontrado: Si se llega al final del conjunto sin encontrar el valor, se indica que el elemento no está presente.
La búsqueda lineal no requiere que los datos estén ordenados y es efectiva para conjuntos de datos pequeños, pero su eficiencia disminuye a medida que el tamaño del conjunto de datos aumenta, ya que en el peor caso, se deben comparar todos los elementos.

Búsqueda Binaria
La búsqueda binaria es un método más eficiente que la búsqueda lineal, pero requiere que el conjunto de datos esté ordenado previamente. Su proceso se describe de la siguiente manera:

Inicio: Determinar los índices de inicio y fin del conjunto de datos, que inicialmente son el primer y último elemento, respectivamente.
División: Calcular el índice medio del conjunto de datos actual y comparar el elemento en esta posición con el valor buscado.
Comparación:
Si el elemento medio es igual al valor buscado, se retorna la posición de este elemento, indicando que se ha encontrado.
Si el elemento medio es mayor que el valor buscado, se descarta la mitad superior del conjunto y se repite el proceso con la mitad inferior.
Si el elemento medio es menor que el valor buscado, se descarta la mitad inferior del conjunto y se repite el proceso con la mitad superior.
Iteración: El proceso se repite, reduciendo a la mitad el tamaño del conjunto de datos en cada paso.
Finalización: Este proceso continúa hasta que se encuentra el valor o el subconjunto se reduce a cero.
La búsqueda binaria es muy eficiente en conjuntos de datos grandes, ya que reduce significativamente el número de comparaciones necesarias en comparación con la búsqueda lineal, logrando una complejidad temporal de O(log n), donde n es el número de elementos en el conjunto de datos.

 
Detalles adicionales de la arquitectura y del API
Implemente los servicios para responder al método de solicitud HTTP GET. Deben usar el nombre de la función especificado. Los parámetros deben ser pasados en variables de query con nombres "list" y "value".
 
El proxy debe delegar el llamado a los servicios de backend. El proxy y los servicios se deben implementar en Java usando Spring.
 
Ejemplo 1 de un llamado:
 
https://amazonxxx.x.xxx.x.xxx:{port}/linearsearch?list=10,20,13,40,60&value=13
 
Salida. El formato de la salida y la respuesta debe ser un JSON con el siguiente formato
 
{
 "operation": "linearSearch",
 "inputlist": "10,20,13,40,60",
 "value": "13"
 "output":  "2"
}
 
Ejemplo 2 de un llamado:
 
 
https://amazonxxx.x.xxx.x.xxx:{port}/linearsearch?list=10,20,13,40,60&value=99
 
Salida. El formato de la salida y la respuesta debe ser un JSON con el siguiente formato
 
{
 "operation": "linearSearch",
 "inputlist": "10,20,13,40,60",
 "value": "99"
 "output":  "-1"
}
 
 
Ejemplo 3 de un llamado:
 
 
https://amazonxxx.x.xxx.x.xxx:{port}/binarysearch?list=10,20,13,40,60&value=13
 
Salida. El formato de la salida y la respuesta debe ser un JSON con el siguiente formato
 
{
 "operation": "binarySearch",
 "inputlist": "10,20,13,40,60",
 "value": "13"
 "output":  "2"
}
 
 
En el campo de texto escriba la dirección de su repositorio GITHUB.
---

Lo que añadí

En math-service (puerto 8081):

GET /linearsearch?list=<csv>&value=<v> → búsqueda lineal (lista de cadenas).
Respuesta JSON: {"operation":"linearSearch","inputlist":"<csv>","value":"<v>","output":"<idx|-1>"}

GET /binarysearch?list=<csv>&value=<v> → búsqueda binaria recursiva (requiere lista ordenada lexicográficamente).
Respuesta JSON análoga, retornando primera ocurrencia si hay duplicados.

En proxy (puerto 8080): rutas espejo que delegan a los backends:

GET /linearsearch?list=...&value=...

GET /binarysearch?list=...&value=...

Sigue soportando /api/fib, /api/fact, /api/isPrime, etc.

MATH_TARGETS configura los targets (coma-separado).

En el cliente web (proxy/src/main/resources/static/index.html):

Formularios para Linear Search y Binary Search (asincrónicos con XHR; sin librerías).

Prueba rápida (resumen)

Compilar:

(cd math-service && mvn -q clean package)
(cd proxy && mvn -q clean package)


Ejecutar dos instancias del servicio:

java -jar math-service/target/math-service-0.0.1-SNAPSHOT.jar --server.port=8081
java -jar math-service/target/math-service-0.0.1-SNAPSHOT.jar --server.port=8082


Ejecutar el proxy apuntando a ambas:

# Linux/macOS
export MATH_TARGETS="http://localhost:8081,http://localhost:8082"
# Windows PowerShell
$env:MATH_TARGETS="http://localhost:8081,http://localhost:8082"

java -jar proxy/target/math-proxy-0.0.1-SNAPSHOT.jar --server.port=8080


Navega a http://localhost:8080/ y usa los formularios o invoca directo:

http://localhost:8080/linearsearch?list=10,20,13,40,60&value=13
http://localhost:8080/linearsearch?list=10,20,13,40,60&value=99
http://localhost:8080/binarysearch?list=10,13,20,40,60&value=13


Todo el detalle de documentación y comandos quedó en el README del zip.
