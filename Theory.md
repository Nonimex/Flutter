# Flutter
* StatelessWidget: componente inmutable. Una vez que se dibuja en la pantalla, sus valores no pueden cambiar por sí solos desde adentro. Si quieres que muestre datos nuevos, tendrías que destruir el widget y crear uno nuevo con otros parámetros externos.

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
