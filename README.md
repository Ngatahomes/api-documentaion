# API DOCUMENTAION
This Markdown document outlines the following:-
* AES encryption procedures, 
* POST and GET endpoints, 
<!-- * error handling, and 
* authentication requirements for your API.  -->

## AES encryption
### Description
AES (Advanced Encryption Standard) is a symmetric encryption algorithm that is widely used to secure sensitive data. AES is a symmetric-key algorithm, meaning the same key is used for both encryption and decryption. <br>

### Usage

Encryption and Decryption keys <u>(IV and SECRET KEY)</u> will be sent to  validated third-party client emails.

<br>

## PHP DATA ENCRYPTION / DESCRIPTION
### Code Example
### Encryption
```php Encryption codeCopyEnabled

<?php
function aesEncrypt($data, $key, $iv) {
    // The encryption method to be used:
    $encrypt_method = "aes-256-cbc";

    // Encrypted payload:
    $encrypted = openssl_encrypt($data, $encrypt_method, $key, 0, $iv);
    
    // Base 64 Encode the encrypted payload:
    $encryptedData = base64_encode($encrypted);
    
    return $encryptedData;
}
```
### Decryption
```php Decryption codeCopyEnabled

<?php
function aesDecrypt($base64_encrypted_payload, $key, $iv) {
    // The encryption method to be used:
    $method = "aes-256-cbc";

    // Base 64 Decode to get encrypted payload
    $encrypted_data = base64_decode($base64_encrypted_payload);

    // Decrypted payload
    $decrypted = openssl_decrypt($encrypted_data, $method, $key, 0, $iv );
    return $decrypted;
}
```
<br>

## DART DATA ENCRYPTION / DESCRIPTION
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
```dart Decryption codeCopyEnabled="4"
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

