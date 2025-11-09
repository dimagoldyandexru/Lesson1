___
# Урок №1.Обновление ядра системы.
**Homework1. System kernel update.**  
Исх. данные.-предварительно установленное и настроенное следующее ПО:  
Хостовая ОС                                             - Window 10 Home  
Установлено ПО                                          - Oracle VirtualBox v 7.2.4  
Гостевая система                                        - Ubuntu 24.04 Desktop  
Клиент для удаленного доступа по протоколам SSH         - PuTTY v.0.77  
___
Выполнение Д.З.  
Подключаемся по **ssh** к созданной виртуальной машине:  
`ssh -p 8022 user@50.50.50.60`  
Проверим текущую версию ядра:  
```
user@vmubuntu:~$ uname -r
6.8.0-87-generic
```
Далее зайдём в браузере в репозиторий, где найдём свежую версию ядра для нашей архитектуры  
https://kernel.ubuntu.com/mainline  
На момент составления документа нам подходит версия 6.17.7: 
https://kernel.ubuntu.com/mainline/v6.17.7/  
Качаем пакеты на виртуальную машину:  
```
user@vmubuntu:~$ mkdir kernel && cd kernel  // создаем каталог kernel в домашней директории и переходим в каталог kernel и затем копируем файлы в этот каталог
user@vmubuntu:~$ wget https://kernel.ubuntu.com/mainline/v6.17.7/amd64/linux-headers-6.17.7-061707-generic_6.17.7-061707.202511021342_amd64.deb
user@vmubuntu:~$ wget https://kernel.ubuntu.com/mainline/v6.17.7/amd64/linux-headers-6.17.7-061707_6.17.7-061707.202511021342_all.deb
user@vmubuntu:~$ wget https://kernel.ubuntu.com/mainline/v6.17.7/amd64/linux-image-unsigned-6.17.7-061707-generic_6.17.7-061707.202511021342_amd64.deb
user@vmubuntu:~$ wget https://kernel.ubuntu.com/mainline/v6.17.7/amd64/linux-modules-6.17.7-061707-generic_6.17.7-061707.202511021342_amd64.deb

```
Устанавливаем все пакеты сразу:  
```user@vmubuntu:~$ sudo dpkg -i *.deb```  
Проверяем, что ядро появилось в /boot.  
```user@vmubuntu:~$ ls -al /boot```  
```
drwxr-xr-x  4 root root     4096 ноя  8 15:27 .
drwxr-xr-x 23 root root     4096 ноя  8 14:16 ..
-rw-r--r--  1 root root   302491 ноя  2 18:43 config-6.17.7-061707-generic
-rw-r--r--  1 root root   287442 июл  5  2024 config-6.8.0-40-generic
-rw-r--r--  1 root root   287416 окт 10 23:20 config-6.8.0-87-generic
drwx------  3 root root     4096 янв  1  1970 efi
drwxr-xr-x  6 root root     4096 ноя  8 15:32 grub
lrwxrwxrwx  1 root root       32 ноя  8 15:27 initrd.img -> initrd.img-6.17.7-061707-generic
-rw-r--r--  1 root root 76245073 ноя  8 15:27 initrd.img-6.17.7-061707-generic
-rw-r--r--  1 root root 74072106 ноя  8 14:31 initrd.img-6.8.0-40-generic
-rw-r--r--  1 root root 74071992 ноя  8 14:30 initrd.img-6.8.0-87-generic
lrwxrwxrwx  1 root root       27 ноя  8 15:27 initrd.img.old -> initrd.img-6.8.0-87-generic
-rw-r--r--  1 root root   142796 апр  8  2024 memtest86+ia32.bin
-rw-r--r--  1 root root   143872 апр  8  2024 memtest86+ia32.efi
-rw-r--r--  1 root root   147744 апр  8  2024 memtest86+x64.bin
-rw-r--r--  1 root root   148992 апр  8  2024 memtest86+x64.efi
-rw-------  1 root root 11301148 ноя  2 18:43 System.map-6.17.7-061707-generic
-rw-------  1 root root  9058665 июл  5  2024 System.map-6.8.0-40-generic
-rw-------  1 root root  9114947 окт 10 23:20 System.map-6.8.0-87-generic
lrwxrwxrwx  1 root root       29 ноя  8 15:27 vmlinuz -> vmlinuz-6.17.7-061707-generic
-rw-------  1 root root 17060031 ноя  2 18:43 vmlinuz-6.17.7-061707-generic
-rw-------  1 root root 14944648 июл  5  2024 vmlinuz-6.8.0-40-generic
-rw-------  1 root root 15006088 окт 10 23:41 vmlinuz-6.8.0-87-generic
lrwxrwxrwx  1 root root       24 ноя  8 15:27 vmlinuz.old -> vmlinuz-6.8.0-87-generic
```
Обновляем конфигурацию загрузчика:  
`user@vmubuntu:~$ sudo update-grub`  
Выбраем загрузку нового ядра по умолчанию:    
`user@vmubuntu:~$ sudo grub-set-default 0`  
Перезагружаем нашу виртуальную машину с помощью команды  
`sudo reboot`  
После перезагрузки снова проверяем версию ядра:  
```
user@vmubuntu:~$  uname -r   
6.17.7-061707-generic  
```  
На этом обновление ядра закончено.











