# *Networking*

## Future:
Imagina que es como un vale o una promesa que te dan en una tienda cuando lo que quieres comprar aún no está listo en el mostrador. En programación, representa un valor que todavía no existe, pero que llegará más adelante (por ejemplo, los datos que tu app descarga de internet, como los de la PokeAPI). No es el dato en sí, sino la promesa de que el dato llegará.

## FutureBuilder:
Es un widget (un componente visual) experto en esperar y vigilar esa promesa (Future).Mientras el Future está viajando a internet, el FutureBuilder puede mostrar un círculo de carga (CircularProgressIndicator).En cuanto el Future regresa con éxito, el FutureBuilder toma esos datos, los lee mediante un snapshot (una instantánea) y dibuja el resultado en pantalla.   

## final:
Es una palabra que se usa para declarar variables cuyo valor se asigna una sola vez y ya no cambia nunca más. Es como escribir con tinta permanente: una vez que la variable recibe un dato, nadie puede modificarlo durante el tiempo que viva ese objeto. Esto da seguridad y optimiza la memoria.

## async (Asíncrono)
Significa "Esta función va a tomar su tiempo".
Cuando pones la palabra async al lado de una función, le estás advirtiendo a Dart: 
"Oye, dentro de esta función hay tareas que van a tardar (como ir a internet), 
así que maneja esto de forma asíncrona para no trabar la aplicación".

## await (Esperar)
Significa "**Párate** aquí un momentito hasta que esto responda".
La palabra await solo se puede usar dentro de una función que tenga async. Sirve para decirle al código: "Detén la ejecución de esta línea específica hasta que el Future termine de descargar los datos y nos entregue el resultado real".
