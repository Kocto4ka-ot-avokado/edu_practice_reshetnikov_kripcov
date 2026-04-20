## Часть 1.
### Шаг 1. Создание топологии сети.
![[topoligi1.png]]

*Рис.1 Топология сети.*




### Шаг 2. Настройка banner MOTD.


#### Настраиваем на каждом роутере MOTD согласно заданию и выдаем hostname, согласно топологии.

![[Pasted image 20260415145006.png]]

*Рис.2 Настройка MOTD на rus-msk-rt0.*

####Такую же настройку, но с изменением имен проводим с остальными устройствами.

![[Pasted image 20260415145936.png]]

*Рис3. Настройка MOTD на rus-msk-rt1*

![[Pasted image 20260415150105.png]]

*Рис.4 Настройка MOTD на rus-nsk-rt0*

### Шаг 3. Новые имена устройств.

<table>

<tr>

<td>

<h3>Москва</h3>

<table>

<tr><th>Первичная</th><th>Измененная</th></tr>

<tr><td>server0</td><td>rus-msk-serv1</td></tr>

<tr><td>switch0</td><td>rus-msk-sw1</td></tr>

<tr><td>router0</td><td>rus-msk-r1</td></tr>

<tr><td>router1</td><td>rus-msk-r2</td></tr>

<tr><td>Multilayer switch1</td><td>rus-msk-multisw1</td></tr>

<tr><td>PC0</td><td>rus-msk-pc1</td></tr>

<tr><td>PC1</td><td>rus-msk-pc2</td></tr>

</table>

</td>

<td>

<h3>Новосибирск</h3>

<table>

<tr><th>Первичная</th><th>Измененная</th></tr>

<tr><td>router0</td><td>rus-nsk-r1</td></tr>

<tr><td>switch0</td><td>rus-nsk-sw1</td></tr>

<tr><td>switch1</td><td>rus-nsk-sw2</td></tr>

<tr><td>PC0</td><td>rus-nsk-pc1</td></tr>

<tr><td>PC1</td><td>rus-nsk-pc2</td></tr>

<tr><td>PC2</td><td>rus-nsk-pc3</td></tr>

<tr><td>PC3</td><td>rus-nsk-pc4</td></tr>

<tr><td>PC4</td><td>rus-nsk-pc5</td></tr>

<tr><td>PC5</td><td>rus-nsk-pc6</td></tr>

</table>

</td>

</tr>

</table>

*Таб.1 Новые имена устройств*

### Шаг 4. Выдача доменных имен согласно местоположению.

<table>

<tr>

<td>

<h3>Москва</h3>

<table>

<tr><th>Устройство</th><th>Домен</th></tr>

<tr><td>rus-msk-serv1</td><td>msk.local</td></tr>

<tr><td>rus-msk-sw1</td><td>msk.local</td></tr>

<tr><td>rus-msk-r1</td><td>msk.local</td></tr>

<tr><td>rus-msk-r2</td><td>msk.local</td></tr>

<tr><td>rus-msk-multisw1</td><td>msk.local</td></tr>

<tr><td>rus-msk-pc1</td><td>msk.local</td></tr>

<tr><td>rus-msk-pc2</td><td>msk.local</td></tr>

</table>

</td>

<td>

<h3>Новосибирск</h3>

<table>

<tr><th>Устройство</th><th>Домен</th></tr>

<tr><td>rus-nsk-r1</td><td>nsk.local</td></tr>

<tr><td>rus-nsk-sw1</td><td>nsk.local</td></tr>

<tr><td>rus-nsk-sw2</td><td>nsk.local</td></tr>

<tr><td>rus-nsk-pc1</td><td>nsk.local</td></tr>

<tr><td>rus-nsk-pc2</td><td>nsk.local</td></tr>

<tr><td>rus-nsk-pc3</td><td>nsk.local</td></tr>

<tr><td>rus-nsk-pc4</td><td>nsk.local</td></tr>

<tr><td>rus-nsk-pc5</td><td>nsk.local</td></tr>

<tr><td>rus-nsk-pc6</td><td>nsk.local</td></tr>

</table>

</td>

</tr>

</table>

*Таб.2 Доменные имена устройств*

### Шаг 5. Создание VLAN на коммутаторах в Новосибирске.

#### Создаем на rus-nsk-sw1 и rus-nsk-sw2 VLAN 2,3 и 4, не присваивая им имен.

![[Pasted image 20260415154116.png]]

*Рис.5 Создание VLAN без имен на rus-nsk-sw1*

![[Pasted image 20260415154420.png]]

*Рис.6 Создание VLAN без имен на rus-nsk-sw2*

### Шаг 6. Присвоение VLAN на интерфейсы.

#### Назначаем VLANы на интерфейсы согласно заданию.

![[Pasted image 20260415161735.png]]

*Рис.7 Присвоение VLAN на rus-nsk-sw1.*

![[Pasted image 20260415161835.png]]

*Рис.8 Присвоение VLAN на rus-nsk-sw2.*

### Шаг 7. Создание канала EtherChannel.

#### Необходимо создать канал EtherChannel 2-го уровня между коммутаторами в Новосибирске со следующими требованиями:

```
1. Использовать стандартный протокол для создания логической связи;
2. Коммутатор 0 долден являтся ответственным за инициирование согласования канала EtherChannel;
3. Изменить интерфейс агрегированного канала на транковый на обоих коммутаторах.
   
```

![[Pasted image 20260415162613.png]]
![[Pasted image 20260415162629.png]]
![[Pasted image 20260415162641.png]]

*Рис 9-11 Настройка EtherChannel на SW1*

#### Аналогично на SW2.

![[Pasted image 20260415163356.png]]

*Рис.12 Настройка EtherChannel на SW2*


### Шаг 8. Создания Management interface для VLAN 1.

#### Необходимо создать Management interface на SW1 используя:
```
1. VLAN 1;
2. IP: 1.0.0.50/8;
3. Шлюз: 1.0.0.1
```
![[Pasted image 20260415164931.png]]

*Рис.13 Настройка Management interface на SW1*

#### Аналогично создаем Management interface на SW1 используя:
```
1. VLAN 2;
2. IP: 2.0.0.50/8;
3. Шлюз: 2.0.0.1
```
![[Pasted image 20260415165301.png]]

*Рис. 14 Настройка Management interface на SW2*

### Шаг 10. Включение SSHv2 в Новосибирске.

#### Требования:
```
user = nsk
password = cisco
Только SSH
```
![[Pasted image 20260415165633.png]]

*Рис. 15 Настройка SSHv2 на SW1*

Точно также выполняем всю настройку на SW2.
```
`conf t`
`username nsk secret cisco`
`crypto key generate rsa`
`1024`
`ip ssh version 2`
`line vty 0 15`
`login local`
`transport input ssh`
`exit`
`end`
`wr`
```

### Шаг 11. Подключение F0/24 от SW1 к R1.

#### Необходимо подключить интерфейс f0/24 от sw1 к r1 в режиме trunk.

![[Pasted image 20260415170345.png]]

*Рис. 16 Включение режима trunk на f0/24*

### Шаг 12. Настройка MOTD на SW1 и SW2.

![[Pasted image 20260415170825.png]]

*Рис. 17 Настройка MOTD на  rus-nsk-sw1*

![[Pasted image 20260415171019.png]]

*Рис. 18 Настройка MOTD на rus-nsk-sw2*

### Шаг 13. Настройка f0/2, f0/3, f0/4.

### Требования:
```
1.Fast forwarding;
2.Не принимать BPDU;
3.Отключить CDP;
4.Port Security;
5.За нарушение - состояние err-disable
```
![[Pasted image 20260415172101.png]]

*Рис 19 Настройка интерфейсов на SW1*

#### Точно такие же команды выполняем на SW2, не забывая сохранить изменения.

### Шаг 14. Защита консоли.

![[Pasted image 20260415172733.png]]

*Рис. 20 Защита консоли на SW1*

#### Идентично выполняем на SW2.

### Шаг 15. Убрать timeout exex для консоли SSH.

#### Выполнить на SW1 и SW2 следующие команды:
```
`line console 0`
`exec-timeout 0 0`
`exit`

`line vty 0 15`
`exec-timeout 0 0`
`end`
`wr`
```

### Шаг 16. Не прерывать ввод логам. Изменения буфера истории до 256 строк.

#### Выполнить на SW1 и SW2 команды:
```
`line console 0`
`logging syschronous`
`exit`
`terminal history size 256`
`end`
`wr`
```

## Часть 2

### Шаг 1. IP на F0/1 маршрутизатора R1
![[Pasted image 20260416151049.png]]

*Рис. 21 настройка f0/1 на R1*


### Шаг 2. Router-on-a-Stick для VLAN 1,2,3,4

#### Настройка VLAN 1
![[Pasted image 20260416152015.png]]

*Рис. 22 насройка f0/0.1*

#### Настройка VLAN 2
![[Pasted image 20260416152152.png]]

*Рис. 23 настройка f0/0.2*


#### Настройка VLAN 3
![[Pasted image 20260416152431.png]]

*Рис.24 настройка f0/0.3*


#### Настройка VLAN 4
![[Pasted image 20260416152732.png]]

*Рис. 25 настройка f0/0.4*


#### Включить физ. интерфейс
![[Pasted image 20260416153043.png]]
 
 *Рис. 26 настройка f0/0*

### Шаг 3. DHCP исключения.

![[Pasted image 20260416161159.png]]

*Рис. 27. Некоторые настройки DHCP.*

#### Шаг 4. DHCP pool для VLAN 

![[Pasted image 20260416161448.png]]

*Рис.28 DHCP pool для VLAN2*

![[Pasted image 20260416161615.png]]

*Рис.29 DHCP pool для VLAN3*

![[Pasted image 20260416161826.png]]

*Рис.30 DHCP pool на VLAN4*

#### Шаг 5. Проверка на ПК.

#### Необходимо проверить корректность IP configuration на всех ПК в Новосибирске.

![[Pasted image 20260416162044.png]]

*Рис. 31 Итоговая конфигурация на PC0*

![[Pasted image 20260416162121.png]]

*Рис.32 Итоговая конфигурация на PC1*

![[Pasted image 20260416162209.png]]

*Рис.33 Итоговая конфигурация на PC2*


## Часть 3. 

### Шаг 1. Настройка имени и включение маршрутизации.

#### Настройка имени согласно топологии:

![[Pasted image 20260416163021.png]]

*Рис.34 Настройка имени на MLS*

![[Pasted image 20260416163107.png]]

*Рис.35 Включение маршрутизации на MLS.*

### Шаг 2. Создание и настройка портов доступа.

![[Pasted image 20260416163303.png]]

*Рис. 36 Создание VLAN 100 и VLAN 200*

![[Pasted image 20260416163442.png]]

*Рис 37. Назначение VLAN на соответствующие порты*

### Шаг 3. Настройка SVI интерфейсов.

![[Pasted image 20260416163859.png]]

*Рис.38 Назначение IP для VLAN 100 и 200*

### Шаг 4. Перевод портов в L3 порты.

#### Необходимо перевести порты: F0/1, F0/2 F0/3 в L3 порты.

![[Pasted image 20260416164138.png]]

*Рис. 39 Настройка F0/1*

![[Pasted image 20260416164226.png]]\\

*Рис. 40 Настройка F0/2*

![[Pasted image 20260416164718.png]]

*Рис. 41 Настройка F0/3*

### Шаг 5. Настройка ПК

![[Pasted image 20260416164851.png]]

*Рис.42 Настройка сети для PC0*

![[Pasted image 20260416165026.png]]

*Рис.43 Настройка сети для PC1*

## Часть 4.

### Шаг 1. Настройка IP на R2.
![[Pasted image 20260416170226.png]]
![[Pasted image 20260416170443.png]]

*Рис.44,45 настройка IP на R2*


### Шаг 2. Настройка IP на R3
 ![[Pasted image 20260416170842.png]]
 ![[Pasted image 20260416170941.png]]
 

*Рис. 46-47 настройка IP на R3*


### Поверка HSRP

#### На R2
![[Pasted image 20260416172611.png]]
*Рис.48*

#### На R3
![[Pasted image 20260416172753.png]]
*Рис.49*


### Тест отказоустойчивости

#### На R2 выключить f0/1
![[Pasted image 20260416173006.png]]
*Рис.50*

#### На R3
![[Pasted image 20260416173243.png]]
*Рис. 51*


### Часть 5.

#### Какие чети участвуют
1.0.0.0/8
2.0.0.0/8
3.0.0.0/8
4.0.0.0/8
10.0.0.0/8
11.0.0.0/8
12.0.0.0/8
40.40.40.0/24
100.0.0.0/8
200.0.0.0/24

#### R1-EIGRP
![[Pasted image 20260416181054.png]]
*рис.52*


#### R1-EIGRP
![[Pasted image 20260416181310.png]]
*рис.53*

#### R2-EIGRP
![[Pasted image 20260420150316.png]]
*рис 54*

#### RUS-MSK-MULTISW1:

![[Pasted image 20260420151355.png]]
*Рис. 55*

### Шаг 2 - Проверка с помощью SSH.

![[Pasted image 20260420152700.png]]

*Рис.55 SSH на sw1*

Подключение SSH с сервера на sw2:

![[Pasted image 20260420152813.png]]

*Рис.56 SSH на sw2*

## Шаг 3 - Пинг с сервера:

![[Pasted image 20260420152850.png]]

*Рис.57 Пинг с сервера*

# Часть 6
## Шаг 1 - Настройка доступа по SSH к SW1 и SW2 

rus-nsk-sw1:

![[Pasted image 20260420152916.png]]

*Рис.58 Настройка доступа SSH на sw1*

rus-nsk-sw2:

![[Pasted image 20260420152938.png]]

*Рис.59 Настройка доступа SSH на sw2*

## Шаг 2 - Настройка доступ к веб-серверу

rus-nsk-r1:

![[Pasted image 20260420152959.png]]

*Рис.60 Настройка доступ к веб-серверу*

## Шаг 3 - Запрет ответа на ping R1 и R2 в Москве

rus-msk-r1:

![[Pasted image 20260420153048.png]]

*Рис.61 Запрет ответа на ping на R1*

rus-msk-r2:

![[Pasted image 20260420153108.png]]

*Рис.62 Запрет ответа на ping на R2*

# Часть 7
## Шаг 1 - Создание loopback-интерфейса на R1

rus-nsk-r1:

![[Pasted image 20260420153125.png]]

*Рис.63 Создание loopback-интерфейса на R1*

## Шаг 2 - Настройка loopback на R2 в Москве

rus-msk-r2:

![[Pasted image 20260420153137.png]]

*Рис.64 Настройка loopback на R2*

## Шаг 3 - Настройка анонсирования Loopback-интерфейса через RIPv2

rus-nsk-r1:
![[Pasted image 20260420153212.png]]


*Рис.65 Настройка анонсирования loopback-интерфейса*

rus-msk-r2:

![[Pasted image 20260420153227.png]]

*Рис.66 Настройка анонсирования loopback-интерфейса*

## Шаг 4 - Ограничение работы RIPv2

rus-msk-r1:

![[Pasted image 20260420153242.png]]

*Рис.67 Ограничение RIPv2 на R1 в Мск*

rus-msk-multisw1:

![[Pasted image 20260420153250.png]]

*Рис.68 Ограничение RIPv2 на MLS в Мск*

## Шаг 5 - Настройка IP-адресации туннеля 

rus-nsk-r1:

![[Pasted image 20260420153304.png]]

*Рис.69 Настройка IP-адресации туннеля на R1*

rus-msk-r2:

![[Pasted image 20260420153318.png]]

*Рис.70 Настройка IP-адресации туннеля на R2*

## Шаг 6 - Проверка

![[Pasted image 20260420153354.png]]

*Рис.71 Проверка loopback-интерфейса*

# Часть 8
## Шаг 1 - Настрйока NTP-сервера и Syslog-сервера
rus-nsk-r1:

![[Pasted image 20260420153422.png]]

*Рис.72 Настрйока NTP-сервера и Syslog-сервера*


rus-msk-r1:

![[Pasted image 20260420153442.png]]

*Рис.73 Настрйока NTP-сервера и Syslog-сервера*

rus-msk-r2:

![[Pasted image 20260420153517.png]]

*Рис.74 Настрйока NTP-сервера и Syslog-сервера*

## Шаг 2 - Включение SNMP на R1 и R2 в Мск
rus-msk-r1:

![[Pasted image 20260420153539.png]]

*Рис.75 Включение SNMP на R1 в Мск*

rus-msk-r2

![[Pasted image 20260420153605.png]]

*Рис.76 Включение SNMP на R2 в Мск*

## Шаг 3 - Настройка AAA и Telnet на R2 в Мск
rus-msk-r2:

![[Pasted image 20260420153619.png]]

*Рис.77 Настройка AAA и Telnet на R2 в Мск*

## Шаг 4 - Настройка FTP на R1 в Мск
rus-msk-r1:

![[Pasted image 20260420153652.png]]
'
*Рис.78 Настройка FTP на R1 в Мск*

## Шаг 5 - Отправка конфигурации R1 на сервер, с помощью FTP
rus-msk-r1:

![[Pasted image 20260420153710.png]]

*Рис.79 Отправка конфигурации*

## Шаг 6 - Отправка конфигурации R2 на сервер, с помощью TFTP
rus-msk-r2:

![[Pasted image 20260420153727.png]]

*Рис.80 Отправка конфигурации*

## Шаг 7 - Проверка на использование команд boot system в R2 в Мск
rus-msk-r2:

![[Pasted image 20260420153745.png]]

*Рис.81 Проверка на использование команд boot system в R2 в Мск*

Команда ничего не выдаёт, значит команд boot system нет

## Шаг 8 - Проверка подключения к R2 в Мск по telnet
Для начала создадим пользователя Standby на R2.

rus-msk-r2:

![[Pasted image 20260420153807.png]]

*Рис.82 Создание пользователя Standby*

Для работы на R2 по telnet нужео поставить пароль для перехода в привилегерованный режим.

rus-msk-r2:

![[Pasted image 20260420153844.png]]

*Рис.83 Пароль для привилегерованного режима.*

Дальше можем подключаться по telnet.

rus-msk-r1:

![[Pasted image 20260420153903.png]]

*Рис.84 Подключение к R2 по telnet*

## Шаг 9 - Изменение локального имени пользователя в R2
Для начала вводим команду для игнорирования конфигурации при загрузке. Вся настройка происходит на rus-msk-r2.

![[Pasted image 20260420155829.png]]

*Рис.85 Ввод команды для игнорирования конфигурации при загрузке.*

Дальше предложит войти в диалоговое окно начальнйо настойки, нужно отказаться.

![[Pasted image 20260420155849.png]]

*Рис.86 Отказ от входа в диалоговое окно начальной настройки*

Затем загружаем старую конфигурацию и изменяем имя пользователя 

![[Pasted image 20260420155904.png]]

*Рис.87 загрузка старой конфигурации

Возвращаем значение конфигурационного регистра.

![[Pasted image 20260420155917.png]]

*Рис.88 Возвращение значения конфигурационного регистра.