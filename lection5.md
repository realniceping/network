---
marp: false
---
# Продолжение разговоров за RIP 
---
### Немного за безопасность
>PPP = point to point protocol
- По умолчанию у cisco на serial включен HDLC, сильно лучше включить encapsuplation PPP
### Виды аутентификации PPP
- Аутентификация PAP - 2 step handshake (plain text) 
- Аутентификация CHAP
- Аутентификация EAP 
---
### Настройка PAP 
- Зеркально, на двух роутерах
> #username <name> password <pwd>
> #interface serial 3/0
> PPP authentication pap
> ppp pap sent-usernanme <name> password <pwd> 
--- 
### RIPNG
- Настойка ipv6 router rip 
> #ipv6 uncast-routing
> #ipv6 router rip <name-of-rip-exemplar>
- !!!В ipv6 нет команды network как класса 
- Настойка RIP осуществляется на интерфейсах 
> #int fa0/0
> #ipv6 enable / ipv6 address <a::1/64> - повешал линк локал адрес 
- На транзитных сетях не надо прописывать публичные адреса
> #ipv6 RIP <name> enable 
---
- Отправка Шлюза по умолчанию через RIP 
> #ipv4 - default-infornation originate 
> через #ipv6 rip <NAME> default-information originate 
- информация отправляема при default infornation при наличии допольнительных данных в пакете избыточна 
> более лучшая команда (давать только в случаях, если у тебя одна дорога до роутера) = #ipv6 <name> default-information only 
- хорошая команда 
> #show ipv6 rip database - узнать все о рип записях (включительно время жизни)
---
### Механизмы рипа для борьбы с петлями маршрутизации 
#### Все эти механизмы включены на cisco by default 
- Split Horizon
> Маршрут не анонсируется через тот же интерфейс, что и получен
- Route Poisoning
> Механизм об уведомлении о недоступности маршрута - завышение метрики об утеряном роуте
#### Вылюченные механизмы 
- Poisoning revers
- Paritional upates 
> update = 30 - говорим о том, что я знаю сетку
> если сетка отваливается, не ждать апдейт, а вещать сразу 
--- 
### Проблема - отправка таблицы маршрутизации хостам
#### РЕШЕНИЕ - тупиковые сети должны быть "пассивными"
- Отметить те интерфейсы, на которые не надо слать update
> passive-interface <int>
- Сильно круче будет если 
> passive interface default 
> на новых портах no passive interface
- Отправка апдейтов заблокирована - это пол беды
- Необходимо заблокировать отправка сообщение об апдейтах 
--- 
- По умолчанию в RIP включена суммаризация маршрутов до классовых сетей
> no auto-summary - твой бро, потому-что да 
> Если очень хочешь суммировать rip - ip summary-address 
> #router rip 
> #distance <cost>

