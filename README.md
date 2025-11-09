# Lesson1
Homework. System kernel update.
Предварительно установленное и настроенное следующее ПО:
Хостовая ОС                                             - Window 10 Home
Установлено ПО                                          - Oracle VirtualBox v 7.2.4
Гостевая система                                        - Ubuntu 24.04 Desktop
Клиент для удаленного доступа по протоколам SSH         - PuTTY v.0.77
--
Д.З.
Подключаемся по ssh к созданной виртуальной машине
ssh -p 8022 user@50.50.50.60
Проверим текущую версию ядра:
user@vmubuntu:~$ uname -r
6.17.7-061707-generic
