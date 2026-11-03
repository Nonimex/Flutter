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


´´´
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http; // 1. Importación de red

void main() {
  runApp(const MyApp());
}

// Pantalla principal de la App
class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Pokemon App',
      home: PokemonScreen(), // Llamamos a nuestra pantalla con estado
    );
  }
}


class MyWidget extends StatefulWidget {
  const new({super.key});

  @override
  State<MyWidget> createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  @override
  Widget build(BuildContext context) {
    return const Placeholder();
  }
}

// 2. Necesitamos un StatefulWidget porque los datos cambian al llegar de internet
class PokemonScreen extends StatefulWidget {
  const PokemonScreen({super.key});

  @override
  State<PokemonScreen> createState() => _PokemonScreenState(); 
}

class _PokemonScreenState extends State<PokemonScreen> {
  // Declaramos la variable de tipo Future que guardará la promesa del Pokémon
  late Future<Pokemon> futurePokemon;

  @override
  void initState() {
    super.initState();
    // 3. AQUÍ SE LLAMA: Apenas arranca la pantalla, disparamos la petición a la API
    futurePokemon = fetchPokemon(); 
  }

  // Función que va a la red a buscar los datos (Networking)
  Future<Pokemon> fetchPokemon() async {
    final response = await http.get(Uri.parse('https://pokeapi.co/api/v2/pokemon/1'));
    
    if (response.statusCode == 200) {
      // Aquí procesarías el JSON (simplificado para el ejemplo)
      return Pokemon(name: "Pikachu"); 
    } else {
      throw Exception('Fallo al cargar el pokemón');
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Mi Primer Networking'),
      ),
      body: Center(
        // 4. AQUÍ VA EL FUTUREBUILDER: Vigila el Future y dibuja según su estado
        child: FutureBuilder<Pokemon>(
          future: futurePokemon, // Le pasamos la promesa
          builder: (context, snapshot) {
            // Si ya llegaron los datos con éxito
            if (snapshot.hasData) {
              return Text('¡Pokémon encontrado: ${snapshot.data!.name}!');
            } 
            // Si ocurrió un error en la red
            else if (snapshot.hasError) {
              return Text('Error: ${snapshot.error}');
            }
            // Mientras tanto (cargando...)
            return const CircularProgressIndicator();
          },
        ),
      ),
    );
  }
}

// Clase modelo sencilla de ejemplo
class Pokemon {
  final String name;
  Pokemon({required this.name});
}
´´´
