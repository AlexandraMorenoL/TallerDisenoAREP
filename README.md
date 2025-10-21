# TallerDisenoAREP
Nombre: Alexandra Moreno Latorre 

---
 

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
