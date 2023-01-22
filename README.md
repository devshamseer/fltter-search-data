# Flutter search 

## Flutter data serch simple 
| S | H | A | M | S | E | E | R |
|-|-|-|-|-|-|-|-|

 <img src="https://devshamseer.github.io/fltter-search-data/Screenshot_1674387396.png" alt="Logo" width="400" height="900"> 



2. add you get api code
## Flutter using dio package

1. Add dependency
```sh
  dependencies:
  dio: ^4.0.6
```
  2. import package

```sh
import 'package:dio/dio.dart';
```
3. Get api 

```sh
http://universities.hipolabs.com/search?country
 ```

 4. search full code
  
```sh

import 'package:flutter/material.dart';
import 'package:dio/dio.dart';

var gethttpList;
void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return const MaterialApp(
      // Remove the debug banner
      debugShowCheckedModeBanner: false,

      home: HomePage(),
    );
  }
}

class HomePage extends StatefulWidget {
  const HomePage({Key? key}) : super(key: key);

  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  // This holds a list of fiction users
  // You can use data fetched from a database or a server as well
  var _allData = [];

  var _searchData = [];
  @override
  initState() {
    _searchData = _allData;
    getHttp();
    super.initState();
  }

  void _runFilter(String enteredKeyword) {
    var results = [];
    if (enteredKeyword.isEmpty) {
      results = _allData;
    } else {
      results = _allData
          .where((user) =>
              user["name"].toLowerCase().contains(enteredKeyword.toLowerCase()))
          .toList();
      // we use the toLowerCase() method to make it case-insensitive
    }

    // Refresh the UI
    setState(() {
      _searchData = results;
    });
  }

  var response = [];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text(''),
      ),
      body: Padding(
        padding: const EdgeInsets.all(10),
        child: Column(
          children: [
            ElevatedButton(
                onPressed: () {
                  getHttp();
                },
                child: Text('gello')),
            Text('All Datas ${_allData.length.toString()}'),
            TextField(
              onChanged: (value) => _runFilter(value),
              decoration: const InputDecoration(
                  labelText: 'Search', suffixIcon: Icon(Icons.search)),
            ),
            const SizedBox(
              height: 20,
            ),
            Expanded(
              child: _searchData.isNotEmpty
                  ? ListView.builder(
                      itemCount: _searchData.length,
                      itemBuilder: (context, index) => Card(
                        key: ValueKey(_searchData[index]["id"]),
                        color: Colors.amberAccent,
                        elevation: 4,
                        margin: const EdgeInsets.symmetric(vertical: 10),
                        child: ListTile(
                          leading: Text(
                            _searchData[index]['alpha_two_code'],
                            style: const TextStyle(fontSize: 24),
                          ),
                          title: Text(_searchData[index]['name']),
                          subtitle: Text(_searchData[0]['web_pages'][0]),
                        ),
                      ),
                    )
                  : const Text(
                      'No results found',
                      style: TextStyle(fontSize: 24),
                    ),
            ),
          ],
        ),
      ),
    );
  }

  void getHttp() async {
    try {
      gethttpList =
          await Dio().get('http://universities.hipolabs.com/search?country');
      // print(response.data['name']);

      //  response.where((valu){
      //     print(valu);
      //   });

      setState(() {
        // print( gethttpList.data);
        _allData.addAll(gethttpList.data);
        print(_allData[0]['web_pages'][0]);
      });

// print(_searchData);

      // .where((user) =>
      //     user["name"].toLowerCase().contains('NorthCap University'));

      // print(game.runtimeType);
    } catch (e) {
      print(e);
    }
  }
}

 ```
  

 # End happy hacking 😄
