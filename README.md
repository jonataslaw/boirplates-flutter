# boirplates-flutter
Uma lista de boirplates úteis

#Custum dio

'''dart
import 'package:dio/dio.dart';
import 'package:tratar_erros_dio/src/shared/constants.dart';

class CustomDio {
  final Dio client;
  CustomDio(this.client) {
    client.options.baseUrl = BASE_URL;
    client.options.connectTimeout = 5000;
  }
}
'''
