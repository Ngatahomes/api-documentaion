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

>### Code Examples
>[PHP](PHP.md) | [Dart / Flutter](FLUTTER.md)
<br>
<br>

<br>

## API END-POINTS
### API ROOT END-POINT 
End-point: https://homes.ngata.co.tz/mobile


> <b style="color:orange">GET</b> &emsp;<span style="color: lightblue">/rent-to-own-properties</span> <br> <hr>
> &emsp;&emsp;&emsp;It fetches a list of verified rent-to-own properties (Off-plan and Existing) 
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
> [payload] : Returns encrypted data for a list of verified rent-to-own properties <br>
> [encrypted] : Returns status of data either encrypted or not, but always is encrypted = true

### Decrypted Payload Data Type
```json
{
    "existing": [
        {
            "monthly_price": 1034868.7151420625,
            "currency": "TZS",
            "selling_cash_price": 88365350.85,
            "project_type": "project",
            "house_type": "Ground duplex",
            "location": "Mwananyamala, Kinondoni, Dar es Salaam",
            "projectId": "061/03",
            "description": null,
            "total_rooms": 2,
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
            "monthly_price": 1946093.54625,
            "currency": "TZS",
            "selling_cash_price": 166173000,
            "project_type": "off-plan",
            "house_type": "Stand Alone",
            "location": "Goba, Kinondoni, Dar es Salaam",
            "projectId": "EST00093",
            "description": "2 Bedroom House",
            "total_sqm": 550,
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
> <b style="color:orange;">[ location ]</b><span style="color:lightblue">[ string ]</span> : Return location where project located. <br><hr>
> <b style="color:orange;">[ projectId ]</b><span style="color:lightblue">[ string ]</span> : Returns unique ID that used to identify a particular project.<br><hr>
> <b style="color:orange;">[ description ]</b><span style="color:lightblue">[ string ]</span> : Returns a detailed explanation about project.<br><hr>
> <b style="color:orange;">[ nearby ]</b><span style="color:lightblue">[ array ]</span> : Returns a list of features nearby the project eg. school, hospital, Bus stand etc.<hr>
> <b style="color:orange;">[ nearby ][ name ]</b><span style="color:lightblue">[ string ]</span> : Returns nearby feature name<hr>
> <b style="color:orange;">[ nearby ][ icon ]</b><span style="color:lightblue">[ string ]</span> : Returns nearby feature icon<hr>
> <b style="color:orange;">[ facilities ]</b><span style="color:lightblue">[ array ]</span> : Returns a list of facilities around the project eg. Air conditioner, Fan, Coach, Barcon etc.<hr>
> <b style="color:orange;">[ facilities ][ name ]</b><span style="color:lightblue">[ string ]</span> : Returns facilitiy name.<hr>
> <b style="color:orange;">[ facilities ][ icon ]</b><span style="color:lightblue">[ string ]</span> : Returns facilitiy icon.<hr>
> <b style="color:orange;">[ facilities ][ type ]</b><span style="color:lightblue">[ string ]</span> : Returns facilitiy icon type eg. fa => fontawesome, bi => bootstrap icon, si => silicon icon.<hr>

> ### Parameters appear only to existing projects
> <b style="color:orange;">[ total_rooms ]</b><span style="color:lightblue">[ int ]</span> : Returns total rooms found in house.<hr>


> ### Parameters appear only to off-plan projects 
> <b style="color:orange;">[ total_sqm ]</b><span style="color:lightblue">[ float ]</span> : Returns total square meters occupied by project<hr>
> <b style="color:orange;">[ drawing ]</b><span style="color:lightblue">[ object|null ]</span> : Return drawing information.<br><hr>
> <b style="color:orange;">[ drawing ][ codeID ]</b><span style="color:lightblue">[ string ]</span> : Returns unique ID that used to identify a particular drawing.<br><hr>
> <b style="color:orange;">[ drawing ][ arch_name ]</b><span style="color:lightblue">[ string ]</span> : Returns architect name.<br><hr>
> <b style="color:orange;">[ drawing ][ arch_email ]</b><span style="color:lightblue">[ string|null ]</span> : Returns architect email.<br><hr>
> <b style="color:orange;">[ drawing ][ arch_phone ]</b><span style="color:lightblue">[ string ]</span> : Returns architect phone number.<br><hr>
> <b style="color:orange;">[ drawing ][ arch_profile_picture ]</b><span style="color:lightblue">[ string ]</span> : Returns architect profile picture.
> <br>
> <br>