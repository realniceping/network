---
marp: true
---
# СЕТИ: Лекция 2
### Концепция статической маршрутизации
---
## Cтатичная маршрутизация работает по средством канальной среды L2
## Типы канальных сред
- BMA - broadcast multiaccess - работает на MAC 
- NBMA - Frame Relay - non boroadcast multiaccess c DLCI идентификатором. Работает на протокле Frame Delay
- Poing-to-Point = HDLC + PPP = non broadcast ---
> HDLC - протокол по умолчанию для сетей p2p - Исторически использовался для подключения терминалов, у циски по сути это cHDLC 
> PPP - протокол L2 
---
# PPP
- Вкладывается в L1 
- ближе всего к PPP - LCP - link control protocol - протокл установления логического канала связи - L2 для PPP 
> NCP - network control protocols - протокол взаимодействия с сетевым уровнем возможны вложения IPv4 IPv6 - L3 для PPP
> CDPCP - cisco discovery protocol - Так же возможное вложения для LCP
---
# Про команду encapsulation на L3 интерфейсе для PPP
- По умолчанию включен encapsulation hdlc
- Куча из этих инкапсуляций - сказание стороны глубокой
- Нам будет интересен PPP 
- А еще пропиши ipv6 unicast routing или не будет работать 
---
# Достоинства PPP 
- aggregation (multilink) + comptess + auth
- PPPoE - overEthernet (Инкапсуляция PPP в Ethernet) - для проверки паролей
- L1 - cooper - serial IT - PSTN - public switch telephone network
--- 
### DTE
- Устройство на стороне клиента - задает скорость
### DCE 
- Устройство на стороне провайдера - задающее скорость 
- Модуль на циске называется HWIC - 2T
- Условное обозначение на схеме - провод в виде молнии
#(config-if)clock rate <bit/s>
---
# Буквы в таблице маршрутизации 
С - directly connected network - Непосредствено подключеные сети
L  - Local - нитерфейс
для таких вещей как serial interface лучше использовать маску 30 
S - обозначение для статических маршрутов - административная дистанция = 0 
> запись S появляется если сеть приделана через интерфейс
> Рекоммендуется только для интерфейств p2p
