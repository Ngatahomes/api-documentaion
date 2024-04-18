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



```kotlin Kotlin codeCopyEnabled
data class Example(
	val text: String
)
```

```java Java
class Example {
    String text;
    
    Example(String text) {
        this.text = text;
    }
    
    String getText() {
        return text;
    }
 }
```

