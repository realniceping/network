---
marp: true
---
# Таймеры в протоколе RIP
---
### RFC specification 
- update timer = 30 sec 
- invalid timer = 180 sec время валидности маршрута, удаляется из таблицы маршрутизации, но не из database
### CISCO extra specification 
- +holddown timer - борьба с петлями маршрутизации - начинает работу после invalid timer пока длиться holddown не принимаем ни от кого этот маршрут, и ананосируем его с метрикой 16
- +flush = 240 sec - update time to live in database (удаление из базы данных)
---
### Важное понятие - redistribute 
> объединение маршрутов из разных источников, выбрасывание внешних, по отношению к какому-либо протоколу маршрутов
> `(config-terminal)#redistribute connected metric 5    `
###### Изученные типы маршрутов
- connected
- static 
- RIP ...

    