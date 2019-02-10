# Encryption

- [Introduction](#introduction)
- [Configuration](#configuration)
- [Using The Encrypter](#using-the-encrypter)
    - [Encrypting A Value](#encrypting-a-value)
    - [Encrypting Without Serialization](#encrypting-without-serialization)
    - [Decrypting A Value](#decrypting-a-value)

##Introduction
Framy's encrypter uses OpenSSL to provide AES-256 and AES-128 encryption. You are strongly encouraged to use Framy's built-in encryption facilities and not attempt to roll your own "homegrown" encryption algorithms. All of Framy's encrypted values are signed using a message authentication code (MAC) so that their underlying value cannot be modified once encrypted.

##Configuration
Before using Framy's encrypter, you must set a key option in your config/app.php configuration file. You should use the `php Framy key:generate` command to generate this key since this command will use PHP's secure random bytes generator to build your key. If this value is not properly set, all values encrypted by Framy will be insecure.

##Using The Encrypter
###Encrypting A Value
You may encrypt a value using the `encrypt` helper. All encrypted values are encrypted using OpenSSL and the AES-256-CBC cipher. Furthermore, all encrypted values are signed with a message authentication code (MAC) to detect any modifications to the encrypted string:

```php
$encryptet = encrypt($value);
```

###Encrypting Without Serialization
Encrypted values are passed through serializing during encryption, which allows for encryption of objects and arrays. Thus, non-PHP clients receiving encrypted values will need to unserialize the data. If you would like to encrypt and decrypt values without serialization, you may use the `encryptString()` and `decryptString()` methods of the `Crypt` class:

```php
use app\framework\Component\Encryption\Crypt;

$encrypted = Crypt::encryptString('Hello world.');

$decrypted = Crypt::decryptString($encrypted);
```

###Decrypting A Value
You may decrypt values using the `decrypt()` helper. If the value can not be properly decrypted, such as when the MAC is invalid, an app\framework\Component\Encryption\DecryptException will be thrown:

```php
use app\framework\Component\Encryption\DecryptException;

try {
    $decrypted = decrypt($encryptedValue);
} catch (DecryptException $e) {
    //
}
```