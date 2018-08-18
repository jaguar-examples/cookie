# cookie

Example showing how to set, read, update and remove a cookie in Jaguar.

```dart
import 'dart:async';
import 'dart:io';
import 'package:jaguar/jaguar.dart';

Future<void> main() async {
  final server = Jaguar();
  // Setting/updating the cookie
  server.get('/add/cookie', (ctx) {
    ctx.response.cookies.add(Cookie('token', 'hello')..path = '/');
  });
  // Reading the cookie
  server.get('/read/cookie', (ctx) => ctx.cookies['token']?.value);
  // Removing the cookie
  server.get('/remove/cookie', (ctx) {
    ctx.response.deleteCookie('token');
  });
  server.log.onRecord.listen(print);
  await server.serve(logRequests: true);
}
```
