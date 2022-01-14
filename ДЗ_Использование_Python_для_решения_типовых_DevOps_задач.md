### 1. 
будет ошибка, т.к. типы не соответсвуют для операции , int и str

c=str(a)+b

c=a+int(b)


### 2. 
##### Лишняя переменная is_change и команда break, которая прерывает обработку при первом же найденом вхождении
```
#!/usr/bin/env python3

import os

bash_command = ["cd ~/devops-netology", "git status"]
fullpath = os.path.abspath("~/devops-netology")
print(fullpath)
result_os = os.popen(' && '.join(bash_command)).read()
for result in result_os.split('\n'):
    if result.find('изменено') != -1:
        prepare_result = result.replace('\tизменено:   ', '').replace(' ', '')
        print(prepare_result)
```

### 3.
```
#!/usr/bin/env python3

import os
import sys

path = os.getcwd()
if len(sys.argv)>1:
    path = sys.argv[1]
bash_command = ["cd "+path, "git status 2>&1"]
fullpath = os.path.abspath(path)
print(fullpath)
result_os = os.popen(' && '.join(bash_command)).read()
for result in result_os.split('\n'):
    if result.find('fatal') != -1:
        print('Не является GIT репозиторием')
        break
    if result.find('изменено') != -1:
        prepare_result = result.replace('\tизменено:   ', '').replace(' ', '')
        print(prepare_result)
```        

### 4.
```
#!/usr/bin/env python3

import socket
import sys

list = ["drive.google.com=142.251.1.194", "mail.google.com=0.0.0.0", "google.com=0.0.0.0"]

i = 0

while i < len(list):
 value = list[i]
 host = value.split('=')
 url = host[0]
 oip = host[1]

 ip = socket.gethostbyname(url)

 if ip != oip:
  print('[ERROR] ' + url +' IP mistmatch: '+oip+' '+ip)
 else:
  print(url+' - '+ip)

 i+=1
 ```
 