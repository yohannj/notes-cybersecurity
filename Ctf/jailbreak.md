# Jailbreak techniques
https://translate.google.com/translate?sl=ko&tl=en&u=https://defenit.kr/2019/09/27/Pwn/%25E3%2584%25B4%2520Research/python_jail/

# Digraph / trigraph
2 or 3 characters may replace another one, this can help bypassing some forbidden characters
https://en.wikipedia.org/wiki/Digraphs_and_trigraphs

# Python
## Write/Execute code in comments
```python
# coding: raw_unicode_escape
#\u000aimport os
#\u000aos.system("ls -laF")
#\u000aos.system("cat *flag*")
```