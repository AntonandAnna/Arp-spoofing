# Описание проекта
Современные информационные технологии подвергаются возрастающему количеству атак, которые представляют угрозу потери целостности и конфиденциальности данных. Актуальность проблемы сетевых атак, таких как ARP-spoofing, становится все более критичной в условиях большое использования локальных сетей в различных сферах жизни.

ARP-spoofing форма атаки, основанная на изменении протокола ARP, который отвечает за соответствие логических IP-адресов и физических MAC-адресов устройств. В ходе атаки злоумышленник отправляет ложные ARP-запросы и ответы, подменяя MAC-адреса. Это позволяет ему подделывать и перенаправлять сетевой трафик, что может привести к серьезным последствиям, таким как перехват информации, ее подмена или нарушение нормального функционирования сети.

Цель данной научной работы заключается в исследовании сценариев атаки ARP-spoofing в виртуальных локальных сетях, созданных с использованием платформы PnetLAB. Принимая во внимание актуальность проблемы и серьезность ее последствий, основной фокус направлен на разработку эффективных методов защиты от атак ARP-спуфинг. Результаты этого исследования могут служить основой для разработки стратегий безопасности и обеспечить устойчивость к подобным угрозам в виртуальных локальных сетях.

# Описание атаки
## Принцип работы ARP-протокола
Как известно, адресация в сети Internet представляет собой 32-битовую последовательность 0 и 1, называющихся IP-адресами. Но непосредственно связь между двумя устройствами в сети осуществляется по адресам канального уровня (MAC-адресам). Так вот, для определения соответствия между логическим адресом сетевого уровня (IP) и физическим адресом устройства (MAC) используется протокол ARP (Address Resolution Protocol)

Он выполняет две основные функции: сопоставление адресов IPv4 и MAC-адресов, а также сохранение таблицы сопоставлений (таблица arp).

Приведем пример получения физического адреса устройства по протоколу ARP, для наглядного рассмотрения уязвимостей при его использовании. Когда возникает необходимость создания соединения между двумя сетевыми устройствами (PC-1 и PC-2), устройство (PC-1) отправляет пакет с широковещательным адресом с целью узнать MAC-адрес, который принадлежит определенному устройству (PC-2) и просьбой отослать ответ. 
                
Сетевое устройство-получатель (PC-2), приняв данный пакет должно произвести сравнение IP-адреса со своим, и в случае совпадения сформировать сообщение-ответ, где указывается непосредственно его MAC-адрес (MAC-адрес устройства PC-2).

Пример такого взаимодействия можно увидеть на картинке.

![image](https://github.com/AntonAndAnna/Arp-spoofing/assets/103459290/555d6b68-ef9b-4e58-91d8-aef46430db0f)

## Описание атаки   
ARP-spoofing это кибератака, основанная на влиянии на передачу ARP-кадров. В ходе атаки злоумышленник сканирует сеть и подменяет MAC-адреса. Это позволяет ему подделывать и перенаправлять сетевой трафик, что приводит к серьезным последствиям, таким как перехват информации, ее подмена или нарушение нормального функционирования сети.

В связи с тем, что ARP-запрос содержит широковещательный MAC-адрес, то такой ARP-кадр может получить любое устройство в широковещательном сегменте. 
Поэтому возникает вариант атаки – реализация кибератаки «человек-посередине» с помощью подмены MAC-адреса порта маршрутизатора на MAC-адрес устройства-нарушителя в таблице ARP устройства жертвы. 

![image](https://github.com/AntonAndAnna/Arp-spoofing/assets/103459290/0f96907a-fb50-4f10-8f04-3f1af89d473b)

Таким образом весь трафик, идущий от устройства-пользователя на маршрутизатор, будет перенаправлен на устройство нарушителя при этом незаметно для самого пользователя.

# Описание платформы для реализации 
Для построения и реализации атаки ARP-спуфинг будет использоваться база платформы PnetLAB. Данная платформа предоставляет возможности проектирования локальных сетей в онлайн и офлайн режимах, а также совместное построение сети в режиме реального времени. При создании проекта (онлайн лаборатории) платформа позволяет добавлять устройства от различных производителей и осуществлять их настройку через встроенную консоль. Кроме встроенной консоли, доступа альтернатива использования сторонних приложений с консолью, так как к каждому добавленному устройству в сети есть возможность подключения по различным протоколам.

# Как установить PnetLab и добавить функцию ishare
Для начала необходимо перейти на официальный сайт во вкладку Download (https://pnetlab.com/pages/download) и загрузить файл с расширение .ova, далее с помощью виртуальных платформ (VMWare, VirtualBox и др.) загрузить данный файл на платформу. В данном проекте была использована виртуальная платформа VMWare. В результате получим:

![photo_2024-04-05_15-54-34](https://github.com/AntonAndAnna/Arp-spoofing/assets/103459290/f6856b56-ed53-42a5-a43e-ca86e5763537)

Далее по ip-адресу, который показываем виртуальная машина, перейти на web-сайт (например http://192.168.15.155). Выбрать вкладку Login by Online Mode, используя Sign Up создадим аккаунт (для этого введем имя пользователя, e-mail, и пароль).

![image](https://github.com/AntonAndAnna/Arp-spoofing/assets/103459290/9306e494-27ce-489b-b3b7-2ef497f7e955)

Потом вы попадете в рабочее пространство, в котором вы можете создавать проекты, также смотреть проекты других пользователей.

![image](https://github.com/AntonAndAnna/Arp-spoofing/assets/103459290/745c6c5c-5f5e-4d03-b2d6-b2254974a2f5)

Также процесс установки можно также найти на официальной сайте (https://pnetlab.com/pages/documentation?slug=install-PNETlab). 

Изначально PnetLAB имеет очень ограниченное количество устройств для выбора и использования, поэтому необходимо осуществить загрузку ishare2. 
Полная инструкция для скачивания этого расширения есть по ссылке:
https://github.com/ishare2-org/ishare2-cli?tab=readme-ov-file#quick-start-%F0%9F%9A%80

После установки ishare2 найти и выбрать необходимое оборудование можно найти и скачать следующим образом:
### 1.	В командной строке терминала PnetLAB ввести команду
(для примера будет осуществлять скачивание конфигурации Huawei)
**root@pnetlab:~# ishare2 search huawei**

![image](https://github.com/AntonAndAnna/Arp-spoofing/assets/103459290/2c26befc-bea0-45bc-b71e-8efdb6e858ac)

После чего будет выведен список доступных устройств с именем Huawei. Чтобы скачать конфигурацию определенного устройства необходимо прописать следующие команды: 
(для примера будет осуществлять скачивание конфигурации Huawei под номером 529)
  **root@pnetlab:~# ishare2 pull qemu 529**

![image](https://github.com/AntonAndAnna/Arp-spoofing/assets/103459290/ad1bf2e0-0cec-4612-aa4f-e1d10ab3b937)

Начнется загрузка соответствующей конфигурации
После окончания загрузки появится сообщение: 

![image](https://github.com/AntonAndAnna/Arp-spoofing/assets/103459290/166ae0f8-b5e6-4133-add5-8ef5ef4252f6)

Далее перейдем в лабораторию и в списке выбора оборудования увидим изменения – станет доступна конфигурация с именем Huawei. 

До:

![image](https://github.com/AntonAndAnna/Arp-spoofing/assets/103459290/14c7fd2a-8087-4361-9a5d-afdf7bb8f9e6)

После:

![image](https://github.com/AntonAndAnna/Arp-spoofing/assets/103459290/34fe1616-430a-41e7-afdc-dc8dfbb08ef3)
