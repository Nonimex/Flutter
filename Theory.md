# Flutter
**StatelessWidget:** 

Componente inmutable. Una vez que se dibuja en la pantalla, sus valores no pueden cambiar por sí solos desde adentro. Si quieres que muestre datos nuevos, tendrías que destruir el widget y crear uno nuevo con otros parámetros externos.

Se usa para elementos estáticos: títulos, tarjetas de información fija, iconos, o textos que no dependen de que el usuario presione un botón para cambiar.

*Code: (To visualize the code, use ``` at the beginning and at the end)

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
