# main dart

```
import 'package:flutter/material.dart';

import 'package:app_sem11_py_contact4949/MyContactList.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: Mycontactlist()
    );
  }
}


```

# Mycontactlist

```
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;
import 'dart:convert';
class Mycontactlist extends StatefulWidget {
  const Mycontactlist({super.key});

  @override
  State<Mycontactlist> createState() => _MycontactlistState();
}

class _MycontactlistState extends State<Mycontactlist> {
  String url = "https://randomuser.me/api/?results=500";
  List data=[];

  Future<String> makeRequest() async{
    var response = await http.get(Uri.parse(url),
    headers: {'Accept': 'aplication/json'});


    setState(() {
      var extractData = json.decode(response.body);
      data = extractData['results'];
    });

    //print('Name: ' +data[0]['name']['first"']);
    //print('Email: ' +data[0]['email']);

    //print(response.body);
    return (response.body);

  }

  @override
  void initState(){
    this.makeRequest();


  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("My contact list")
      ),
      body: ListView.builder(
        itemCount: data == null ? 0 : data.length,

          itemBuilder: (BuildContext context, i){
          return ListTile(
            title: Text(data[i]['name']['first']),
            subtitle: Text(data[i]['cell']),
            leading: CircleAvatar(
              backgroundImage: NetworkImage(data[i]['picture']['thumbnail']),
            ),
            onTap: (){},
          );
          }
      )
    );
  }
}

```  
