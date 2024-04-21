# API DOCUMENTAION
>This Markdown document outlines the following:-
>* AES encryption procedures, 
>* POST and GET endpoints 
<br>
<br>

<br>

<!-- * error handling, and 
* authentication requirements for your API.  -->

## AES encryption
> ### Description
> AES (Advanced Encryption Standard) is a symmetric encryption algorithm that is widely used to secure sensitive data. AES is a symmetric-key algorithm, meaning the same key is used for both encryption and decryption. <br>

>### Usage
> Encryption and Decryption keys <u>(IV and SECRET KEY)</u> will be sent to  validated third-party client emails.
<br>
<br>

## PHP DATA ENCRYPTION AND DECRYPTION
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
<br>

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

## API END-POINTS
### API ROOT END-POINT 
End-point: https://homes.ngata.co.tz/mobile


> <b style="color:orange">GET</b> &emsp;<span style="color: lightblue">/project-list</span> <br> <hr>
> It fetches a list of verified rent-to-own properties (Off-plan and Existing) 
<br>
<br>

## Response
### Encrypted Payload
```json 
{
    "payload": "RlhtUkE1MDVqb29QOWdXRGRoytICRg==",
    "encrypted": true
}
```
> [payload][string] : Returns encrypted data for a list of verified rent-to-own properties <br>
> [encrypted][boolean] : Returns status of data either encrypted or not, but always is encrypted = true

### Decrypted Payload Data Type
```json
{
    "existing": [
        {
            "projectId": 209,
            "codeId": "061/03",
            "monthly_price": 1034868.7151420625,
            "currency": "TZS",
            "selling_cash_price": 88365350.85,
            "project_type": "project",
            "house_type": "Ground duplex",
            "location": "Mwananyamala, Kinondoni, Dar es Salaam",
            "description": "Nyumba ipo mahali pazuri karibu na huduma muhimu za jamii kama Hospitali, shule n.k \r\nMaji yapo ndani ya nyumba masaa 24.",
            "total_rooms": 2,
            "redirect_url": "https://homes.ngata.co.tz/rent-to-own/project-details/209/project",
            "images": [
                {
                    "path": "https://filesystem.ngata.co.tz/properties/projects/houses/UNI-N15R8WYV-c10xaWVRGsCFFMfJROEaViBSoW8RTrGFaupcfA5C.png",
                    "elevation": "front"
                },
                {
                    "path": "https://filesystem.ngata.co.tz/properties/projects/houses/UNI-N15R8WYV-Z4o1wpzFjlZU6tjO9MCRAX7HA7nOIfQSBAiPqe0A.png",
                    "elevation": "rear"
                },
                {
                    "path": "https://filesystem.ngata.co.tz/properties/projects/houses/UNI-N15R8WYV-CqxLGJD1VBzERKTbU0iOc2mRVHTDpmsZTGRwDIu9.png",
                    "elevation": "right"
                },
                {
                    "path": "https://filesystem.ngata.co.tz/properties/projects/houses/UNI-N15R8WYV-XQjFhELRz5ei36lJRcuqqT9CG8nxCzCtr5qa1A59.png",
                    "elevation": "left"
                }
            ],
            "map_coordinate": {
                "latitude": "-6.781848",
                "longitude": "39.2337241"
            },
            "facilities": [
                {
                    "id": 2,
                    "name": "Living Room",
                    "icon": "couch",
                    "type": "fa"
                },
            ],
            "nearby": [
                {
                    "name": "Bus Stand",
                    "icon": "location_on"
                },
            ]
        }
    ], 
    "offplan": [
        {
            "projectId": 93,
            "codeId": "EST00093",
            "monthly_price": 1946093.54625,
            "currency": "TZS",
            "selling_cash_price": 166173000,
            "project_type": "off-plan",
            "house_type": "Stand Alone",
            "location": "Goba, Kinondoni, Dar es Salaam",
            "description": "2 Bedroom House",
            "total_sqm": 550,
            "redirect_url": "https://homes.ngata.co.tz/rent-to-own/project-details/93",
            "images": [
                {
                    "path": "https://filesystem.ngata.co.tz/documents/drawings/rsmrVanT1qVbFXiNNQciv8kCD2Rjl3ikbYVEm261.jpg",
                    "elevation": "aerial"
                },
                {
                    "path": "https://filesystem.ngata.co.tz/documents/drawings/Yzo7lCk7LuKLcMGmIeYkDqtpQM7b4EkBCwhvU4o9.jpg",
                    "elevation": "sided"
                },
                {
                    "path": "https://filesystem.ngata.co.tz/documents/drawings/Uu7vyPF3ydq1J5OxiwUFRzX2VMpGVpXZecmygQaU.jpg",
                    "elevation": "layers"
                },
                {
                    "path": "https://filesystem.ngata.co.tz/documents/drawings/0niM0gTUTBxBMdPZQXt8QErFZ0ocM7E38kvf3llg.jpg",
                    "elevation": "others"
                }
            ],
            "map_coordinate": {
                "latitude": "-6.781848",
                "longitude": "39.2337241"
            },
            "drawing": {
                "id": 186,
                "codeID": "DRW00187",
                "features": "[\"1\",\"2\",\"3\",\"5\",\"15\",\"16\",\"17\"]",
                "facilities": null,
                "arch_name": "Paul Paschal Bwaye",
                "arch_email": "paulbwaye85@gmail.com",
                "arch_phone": "+255756077455",
                "arch_profile_picture": "https://filesystem.ngata.co.tz/avatars/avatar0.webp",
                "house_type": {
                    "id": 2,
                    "title": "Stand Alone",
                }
            },
            "facilities": [
                {
                    "id": 1,
                    "name": "M Bedroom",
                    "icon": "bed",
                    "type": "fa"
                }
            ]
        }
    ]
}
```
> ## Payload Parameters description
> <b style="color:orange;">[ monthly_price ]</b><b style="color:lightblue">[ float ]</b> : Returns Monthly Price. <hr>
> <b style="color:orange;">[ currency ]</b><span style="color:lightblue">[ string ]</span> : Returns price currency which can be either TZS or USD. <hr>
> <b style="color:orange;">[ selling_cash_price ]</b><span style="color:lightblue">[ float ]</span> : Returns project cash selling price.<br><hr>
> <b style="color:orange;">[ project_type ]</b><span style="color:lightblue">[ string ]</span> : Returns project type eg. off-plan or project (means existing project)<br><hr>
> <b style="color:orange;">[ house_type ]</b><span style="color:lightblue">[ string ]</span> : Returns projecct type eg. Stand Alone, Ground Duplex, Appartment etc.<br><hr>
> <b style="color:orange;">[ location? ]</b><span style="color:lightblue">[ string|null ]</span> : Return location where project located. <br><hr> 
> <b style="color:orange;">[ projectId ]</b><span style="color:lightblue">[ int ]</span> : Returns unique ID that used to identify a particular project.<br><hr>
> <b style="color:orange;">[ codeId ]</b><span style="color:lightblue">[ string ]</span> : Returns unique project label.<br><hr>
> <b style="color:orange;">[ descriptions? ]</b><span style="color:lightblue">[ string ]</span> : Returns a detailed explanation about project.<br><hr>
> <b style="color:orange;">[ redirect_url ]</b><span style="color:lightblue">[ string ]</span> : Returns url for webview, it displays project details on web. <br><hr>
> <b style="color:orange;">[ images ]</b><span style="color:lightblue">[ string ]</span> : Returns project images. <br><hr>
> <b style="color:orange;">[ images ][ path ]</b><span style="color:lightblue">[ string ]</span> : Returns image source url. <br><hr>
> <b style="color:orange;">[ images ][ elevation ]</b><span style="color:lightblue">[ string ]</span> : Returns projet image elevations (front, rear, right, left and others for existing projects) and (aerial, layers, sided and others for offplan projects ). <br><hr>
> <b style="color:orange;">[ map_coordinate ]</b><span style="color:lightblue">[ object|map ]</span> : Returns location coordinates that will be used to display project on map. <br><hr>
> <b style="color:orange;">[ map_coordinate ][ latitude? ]</b><span style="color:lightblue">[ float|null ]</span> : Returns latitude. <br><hr>
> <b style="color:orange;">[ map_coordinate ][ longitude? ]</b><span style="color:lightblue">[ float|null ]</span> : Returns longitude. <br><hr>
> <b style="color:orange;">[ nearby? ]</b><span style="color:lightblue">[ array|null ]</span> : Returns a list of features nearby the project eg. school, hospital, Bus stand etc.<hr>
> <b style="color:orange;">[ nearby ][ name ]</b><span style="color:lightblue">[ string ]</span> : Returns nearby feature name<hr>
> <b style="color:orange;">[ nearby ][ icon ]</b><span style="color:lightblue">[ string ]</span> : Returns nearby feature icon<hr>
> <b style="color:orange;">[ facilities? ]</b><span style="color:lightblue">[ array|null ]</span> : Returns a list of facilities around the project eg. Air conditioner, Fan, Coach, Barcon etc.<hr>
> <b style="color:orange;">[ facilities ][ name ]</b><span style="color:lightblue">[ string ]</span> : Returns facilitiy name.<hr>
> <b style="color:orange;">[ facilities ][ icon ]</b><span style="color:lightblue">[ string ]</span> : Returns facilitiy icon.<hr>
> <b style="color:orange;">[ facilities ][ type ]</b><span style="color:lightblue">[ string ]</span> : Returns facilitiy icon type eg. fa => fontawesome, bi => bootstrap icon, si => silicon icon.<hr>

> ### Parameters appear only to existing projects
> <b style="color:orange;">[ total_rooms ]</b><span style="color:lightblue">[ int ]</span> : Returns total rooms found in house.<hr>

> ### Parameters appear only to off-plan projects 
> <b style="color:orange;">[ total_sqm ]</b><span style="color:lightblue">[ float ]</span> : Returns total square meters occupied by project<hr>
> <b style="color:orange;">[ drawing? ]</b><span style="color:lightblue">[ object|null ]</span> : Return drawing information.<br><hr>
> <b style="color:orange;">[ drawing ][ codeID ]</b><span style="color:lightblue">[ string ]</span> : Returns unique ID that used to identify a particular drawing.<br><hr>
> <b style="color:orange;">[ drawing ][ arch_name ]</b><span style="color:lightblue">[ string ]</span> : Returns architect name.<br><hr>
> <b style="color:orange;">[ drawing ][ arch_email? ]</b><span style="color:lightblue">[ string|null ]</span> : Returns architect email.<br><hr>
> <b style="color:orange;">[ drawing ][ arch_phone ]</b><span style="color:lightblue">[ string ]</span> : Returns architect phone number.<br><hr>
> <b style="color:orange;">[ drawing ][ arch_profile_picture ]</b><span style="color:lightblue">[ string ]</span> : Returns architect profile picture.
> <br>
> <br>