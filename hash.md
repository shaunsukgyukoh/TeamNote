# Basic hash function

- sha256

``` python
import hashlib

data = 'test'.encode()
hash_obj = hashlib.sha256()
hash_obj.update(data)
hex_dig = hash_obj.hexdigest()
print(hex_dig)
```