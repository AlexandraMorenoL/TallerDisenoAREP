# TallerDisenoAREP
Nombre: Alexandra Moreno Latorre 

---
vesrwfd
---

Dentro encontrarás esta estructura:

math-proxy-microservices/
├─ proxy/                 # Spring Boot: proxy round-robin + cliente web (index.html)
│  └─ src/main/resources/static/index.html
├─ math-service/          # Spring Boot: Fibonacci, Factorial, Primalidad
└─ README.md              # Cómo compilar, correr local, y desplegar en AWS EC2

Cómo probar rápido (resumen)

Compilar:

cd math-service && mvn -q clean package
cd ../proxy && mvn -q clean package


Levantar dos instancias de math-service:

# Terminal A
java -jar math-service/target/math-service-0.0.1-SNAPSHOT.jar --server.port=8081
# Terminal B
java -jar math-service/target/math-service-0.0.1-SNAPSHOT.jar --server.port=8082


Levantar el proxy (apuntando a ambas):

# Linux/macOS
export MATH_TARGETS="http://localhost:8081,http://localhost:8082"
# Windows PowerShell
$env:MATH_TARGETS="http://localhost:8081,http://localhost:8082"

java -jar proxy/target/math-proxy-0.0.1-SNAPSHOT.jar --server.port=8080


Abre el cliente:
http://localhost:8080/
(o también prueba: /api/fib?n=10, /api/fact?n=10, /api/isPrime?n=97, /api/targets).

Todo lo demás (incluido AWS EC2 paso a paso) está explicado dentro del README.md del zip.
