# boirplates-flutter
Uma lista de boirplates úteis

# Custum dio

```dart
import 'package:dio/dio.dart';
import 'package:tratar_erros_dio/src/shared/constants.dart';

class CustomDio {
  final Dio client;
  CustomDio(this.client) {
    client.options.baseUrl = BASE_URL;
    client.options.connectTimeout = 5000;
  }
}
```

# Singleton bloc

```dart
class SingletonBloc {
  static SingletonBloc _favoriteBloc;
//devolva sempre a mesma instancia 
  factory SingletonBloc() {
    if (_favoriteBloc == null) _favoriteBloc = SingletonBloc._();
    return _favoriteBloc;
  }
// coloque aqui seus controllers e as variaveis que você vai acessar
  var count = 0;
  BehaviorSubject<int> _contador;
  get contador => _contador.stream;

  // construtor privado
  SingletonBloc._() {
//inicilize seus métodos e instancie seus controller aqui
    _contador = BehaviorSubject<int>();
    increment();
  }
//se precisar chamar algum método, chama assim:
  increment() {
    _contador.sink.add(count++);
  }

//feche suas streams quando o dispose for chamado
  dispose() {
    _contador.close();
  }
}

```

# Open database (HomePage deve ser home do materialApp)
```dart
class HomePage extends StatelessWidget {
  const HomePage({Key key}) : super(key: key);
  @override
  Widget build(BuildContext context) {
    return FutureBuilder(
        future: openDatabase(),
        builder: (context, snapshot) {
          if (snapshot.connectionState == ConnectionState.done) {
            if (snapshot.error != null) {
              print(snapshot.error);
              return Scaffold(
                body: Center(
                  child: Text('Something went wrong :/'),
                ),
              );
            } else {
              return MainPage();
            }
          } else {
            return Scaffold(body: Center(
                  child: CupertinoActivityIndicator(),
                ));
          }
        });
  }
}

```
