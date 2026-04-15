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
