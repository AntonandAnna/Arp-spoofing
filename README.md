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

# Как установить PnetLab и добавить функцию ishare2
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
### В командной строке терминала PnetLAB ввести команду
(для примера будет осуществлять скачивание конфигурации Huawei)
```
root@pnetlab:~# ishare2 search huawei
```
![image](https://github.com/AntonAndAnna/Arp-spoofing/assets/103459290/2c26befc-bea0-45bc-b71e-8efdb6e858ac)

После чего будет выведен список доступных устройств с именем Huawei. 

### Чтобы скачать конфигурацию определенного устройства необходимо прописать следующие команды: 
(для примера будет осуществлять скачивание конфигурации Huawei под номером 529)
```
root@pnetlab:~# ishare2 pull qemu 529
```
![image](https://github.com/AntonAndAnna/Arp-spoofing/assets/103459290/ad1bf2e0-0cec-4612-aa4f-e1d10ab3b937)

Начнется загрузка соответствующей конфигурации
### После окончания загрузки появится сообщение: 

![image](https://github.com/AntonAndAnna/Arp-spoofing/assets/103459290/70f2ac3e-2c80-4efc-9c63-53cfd31a246c)

### Далее перейдем в лабораторию и в списке выбора оборудования увидим изменения – станет доступна конфигурация с именем Huawei. 

До:

![image](https://github.com/AntonAndAnna/Arp-spoofing/assets/103459290/14c7fd2a-8087-4361-9a5d-afdf7bb8f9e6)

После:

![image](https://github.com/AntonAndAnna/Arp-spoofing/assets/103459290/34fe1616-430a-41e7-afdc-dc8dfbb08ef3)"

Может пройти также ситуация, где при поиске конфигурации через ishare2 она не будет найдена. Поэтому есть второй способ для добавления устройств.

Для начала нужно найти конфигурацию по ссылке:  https://drive.labhub.eu.org

Скачав нужный образ нам необходимо загрузить его напрямую в PnetLAB. Воспользуемся также Mobaxterm, При подключении к консоли слева можем увидеть файловое представление: 

![image](https://github.com/AntonAndAnna/Arp-spoofing/assets/103459290/520db192-a217-4ffe-b422-6f4a91d8c21d)

Необходимо перейти по пути:
```
/opt/unetlab/addons/qemu/
```

И после чего нажав в любом месте окна правой кнопкой мыши вызвать окно: 

![image](https://github.com/AntonAndAnna/Arp-spoofing/assets/103459290/a0a60412-5d3a-4f92-93ad-7ac2f5a98980)

Используя пункт «upload to current folder» загрузим необходимую конфигурацию

# Создание лаборатории сети
Построенная виртуальная лаборатория в PnetLab будет выглядеть так:

![image](https://github.com/AntonAndAnna/Arp-spoofing/assets/103459290/9a2562e2-9a16-492f-b999-a2f9d84e88c0)

В нее входит следующее оборудование:

– шлюз подключения к внешней сети (Network)

!!! Важно, что при использовании VMWare – необходимо выбрать Type( Management (Cloud0))

– маршрутизатор Microtik 7.6 (Router), можно загрузить с помощью ishare2 (описаннной выше).

– коммутатор Cisco IOS L2 (Switch) – ссылка на скачивание https://upw.io/772/i86bi_linux_l2-adventerprisek9-ms.SSA.high_iron_20190423 (добавление данного устройства описано выше)

– компьютер нарушителя с ОС Linux (Ubuntu);

– компьютер жертвы с ОС Linux (Ubuntu_victim);

Данные устройства уже есть в PnetLab.

![image](https://github.com/AntonAndAnna/Arp-spoofing/assets/103459290/886bf7e8-9547-4394-9433-66e02d87ae1b)

Загрузим Ubuntu Server 20.04 и Ubuntu Desktop 20.04, а также WireShark (пригодится в будушем)

Далее выбрав Doker.io, выберем файл image, как представлено ниже:

![image](https://github.com/AntonAndAnna/Arp-spoofing/assets/103459290/3fb79ca6-dfd6-4961-ade1-17bd19a62d0f)

Далее произведем настройку сетевого оборудования

Для настройки маршрутизатора на нем необходимо создать два VLAN, и настроить автоматическую раздачу IP-адресов для устройств, которые будут находится в этих VLAN
# Настройка Router (Microtik 7.6)
## Создание VLAN
```
interface vlan add name=vlan110 vlan-id=110 interface=ether2
interface vlan add name=vlan115 vlan-id=115 interface=ether2
```
## Назначение IP-адресов для данных VLAN
```
ip address add address=192.168.110.1/24 network=192.168.110.0 interface=vlan110
ip address add address=192.168.115.1/24 network=192.168.115.0 interface=vlan115
```
## Настройка DHCP-сервера для VLAN
```
dhcp server interface vlan 110 address space 192.168.110.0/24 gateway 192.168.110.1 addresses 192.168.110.2-192.168.110.15
dhcp server interface vlan 115 address space 192.168.115.0/24 gateway 192.168.115.1 addresses 192.168.115.2-192.168.115.15
```
## Настройка NAT для выхода во внешнюю сеть
```
ip firewall nat add action=masquerade chain=srcnat out-interface=ether2 
```
В результате получим конфигурацию, чтобы ее вывести можно использовать команду
```
/ export compact
```
![image](https://github.com/AntonAndAnna/Arp-spoofing/assets/103459290/5d7b1ffd-c9b7-4d09-b595-3b1bba4a9bb8)

# Настройка Switch
Для этого необоходимо перейти в привелегированный режим командамми
```
>enable
#configure terminal
```
## Создание VLAN
```
vlan 110
name pc
vlan 115
name trunk
```
## Назначение trunk и access портов
```
interface e0/0
switchport mode access
switchport access vlan 110
```
```
interface e0/2
switchport mode trunk
switchport encapsulation dot1q
switchport trunk native vlan 115
switchport trunk allowed vlan 110
```
Далее необходимо сохранить конфигурацию используя команду
```
write
```
И чтобы вывести конфигурацию используем команжу
```
show run
```

![image](https://github.com/AntonAndAnna/Arp-spoofing/assets/103459290/2e5ac7cb-765e-4f19-9fee-5d273c9000d4)

# Реализация атаки
# Методы защиты
# Реализация методов защиты
