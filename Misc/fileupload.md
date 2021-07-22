# Client side filtering
## Opt1: Remove the check
Intercept JS in Burp (need to update Options filtering js extension from intercept) and remove the code.

## Opt2: Alter after check
Provide a file validating the check then intercept the request in Burp and change the content to the wanted file (can be just updating the name of the file or its extension)

## Opt3: curl
curl -X POST -F "submit:VALUE" -F "FILE_PARAMETER:@PATH_TO_FILE" TARGET

# Server side filtering
## Use other extension
### php
php
php3
php4
php5
pht
phtml
phar
phps

## File extension trick
### Null byte
Add %2500 (%00 with % encoded) followed by a valid extension
some_file.php%2500.jpg

### Putting some valid extension
If .gif is valid, try some_file.gif.php

## Update magic bytes
Prefix the file with as much "A" as bytes you need to add, then use `hexeditor` to update those first bytes.