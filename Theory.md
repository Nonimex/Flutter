# Flutter
**StatelessWidget:** 

Componente inmutable. Una vez que se dibuja en la pantalla, sus valores no pueden cambiar por sí solos desde adentro. Si quieres que muestre datos nuevos, tendrías que destruir el widget y crear uno nuevo con otros parámetros externos.

Se usa para elementos estáticos: títulos, tarjetas de información fija, iconos, o textos que no dependen de que el usuario presione un botón para cambiar.

const: Otra vez la palabra de optimización. Indica que este constructor puede generar objetos constantes.



* Code: (To visualize the code, use ``` at the beginning and at the end)
* MyStaticCard: El nombre del constructor (debe llamarse exactamente igual que la clase).
* { y } (Corchetes): En los constructores de Dart, los corchetes significan que los parámetros que van adentro son parámetros con nombre y opcionales.
* super: Es una palabra clave que hace referencia directa a la clase padre (en este caso, a StatelessWidget)
* .key: Las Keys (Llaves) en Flutter funcionan como un DNI o cédula de identidad única para cada widget. Cuando Flutter dibuja miles de elementos en pantalla, utiliza las Keys para identificar exactamente qué widget es cuál al momento de moverlos, destruirlos o actualizarlos en el árbol de componentes.
"Recibe una llave opcional desde afuera y envíasela automáticamente al constructor de la clase padre (StatelessWidget) para que el sistema de Flutter pueda rastrear este widget de forma única dentro del árbol visual"

* @override: Es una anotación (etiqueta con arroba). Le avisa explícitamente al compilador: "Voy a reescribir a mi manera una función obligatoria que ya venía predefinida en la clase padre (StatelessWidget)".
* Widget: Es el tipo de dato que va a retornar esta función. En Flutter, absolutamente todo lo que se ve en la pantalla es un Widget (un texto, un botón, un contenedor, un espacio vacío)
* build: Es el nombre obligatorio de la función principal de renderizado en Flutter.
* BuildContext context: Este es un parámetro vital. El context funciona como el GPS o la ubicación exacta de este widget dentro del árbol gigante de componentes de la aplicación. Le dice a Flutter: "Estoy parado exactamente en este nivel de la jerarquía", lo cual es necesario si el widget necesita buscar temas visuales, tamaños de pantalla o navegar hacia otras vistas.
* Text(...): Es un widget oficial de Flutter que se encarga de dibujar una cadena de caracteres en la pantalla.
* home:parámetro obligatorio o principal que recibe el widget MaterialApp, Esta es la pantalla principal que quiero que dibujes en el teléfono apenas arranque la aplicación
* body:Es un parámetro que pertenece al widget Scaffold (el cual actúa como el esqueleto o lienzo estándar de una pantalla en Flutter).
El Scaffold te permite dividir una pantalla en zonas lógicas (como una barra superior appBar, una barra de navegación inferior bottomNavigationBar, o botones flotantes). El body (cuerpo) es la propiedad que define el espacio central de trabajo. Todo lo que coloques dentro del body se dibujará en el área libre del centro de la pantalla, respetando los espacios de las barras si las hubiera.
* Center: Es un widget estructural cuyo único propósito en la vida es la alineación.
* child: Es un parámetro de propiedad que se escribe en muchos widgets de Flutter. En la arquitectura de Flutter, los componentes visuales se dividen estrictamente en dos tipos según cuántos elementos pueden contener adentro:
  - Widgets que aceptan un solo hijo: Como Center, Padding, Card o Container. Como solo pueden envolver a un elemento, obligatoriamente utilizan la propiedad child: (que significa "el       hijo único que tengo adentro es...").
  - Widgets que aceptan múltiples hijos (listas): Como Column o Row. Esos utilizan la propiedad children: (en plural) con corchetes [...].

```
import 'package:flutter/material.dart';

class MiTarjetaEstatica extends StatelessWidget {
  const MiTarjetaEstatica({super.key});

  @override
  Widget build(BuildContext context) {
    return Text('Hola, soy un texto estático');
  }
}
```

**StatefulWidget**

Componente que sí tiene memoria. Puede cambiar su apariencia visual en tiempo real cuando el usuario interactúa con él (por ejemplo, presionar un botón, escribir en un campo de texto, o cargar datos de internet).

en Flutter un StatefulWidget siempre se divide obligatoriamente en dos partes:

* La clase principal: Es inmutable, actúa como la carcasa y solo sirve para conectar el widget.
* La clase de Estado (State): Es la clase que vive en la memoria del teléfono, guarda las variables que cambian y contiene el método build para redibujar la pantalla.

```
import 'package:flutter/material.dart';

// 1. La Carcasa (El StatefulWidget)
class ContadorWidget extends StatefulWidget {
  const ContadorWidget({super.key});

  @override
  State<ContadorWidget> createState() => _ContadorWidgetState();
}

// 2. La Memoria y la Interfaz (El Estado)
class _ContadorWidgetState extends State<ContadorWidget> {
  // Variable de Estado (La memoria mutable)
  int contador = 0;

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        Text(
          'Número de clicks: $contador',
          style: const TextStyle(fontSize: 24),
        ),
        const SizedBox(height: 16),
        ElevatedButton(
          onPressed: () {
            // AQUÍ OCURRE LA MAGIA DEL ESTADO
            setState(() {
              contador++; // Incrementamos el valor en 1
            });
          },
          child: const Text('Incrementar'),
        ),
      ],
    );
  }
}

```
