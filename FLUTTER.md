
## DART DATA ENCRYPTION AND DECRYPTION
### Installation (encrypt: ^5.0.3)
You can install the package from the command line:
<br> With dart:
```bash codeCopyEnabled
dart pub global activate encrypt
```

<br> With flutter:
```bash codeCopyEnabled
flutter pub add encrypt
```

### Code Example
### Encryption
```dart Encryption codeCopyEnabled
import 'package:encrypt/encrypt.dart';
import 'dart:convert';

String aesEncrypt(String plainText, String iv, String key) {
  IV ivObj = IV.fromUtf8(iv);
  Key keyObj = Key.fromUtf8(key);
  final encrypter = Encrypter(
    AES(
      keyObj,
      mode: AESMode.cbc,
    ),
  ); // Apply CBC mode //The encryption method to be used:

  // Encrypted payload:
  String encrypted = encrypter.encrypt(plainText, iv: ivObj).base64;

  // Base 64 Encode the encrypted payload:
  return base64.encode(encrypted.codeUnits);
}
```

### Decryption
```dart Decryption codeCopyEnabled
import 'package:encrypt/encrypt.dart';
import 'dart:convert';

String aesDecrypt(String cipherText, String iv, String key) {
  IV ivObj = IV.fromUtf8(iv);
  Key keyObj = Key.fromUtf8(key);
  final encrypter = Encrypter(
    AES(
      keyObj,
      mode: AESMode.cbc,
    ),
  ); // Apply CBC mode

  String firstBase64Decoding = String.fromCharCodes(
    base64.decode(payload),
  ); // First Base64 decoding

  final decrypted = encrypter.decrypt(
    Encrypted.fromBase64(firstBase64Decoding),
    iv: ivObj,
  ); // Second Base64 decoding (during decryption)
  
  return decrypted;
}
```
<br>

[ 🔙 Go Home ](README.md) | [PHP code example](PHP.md) 