### Tuvio TUH04DE в Home Asistant через Tuya Local

(добавить конфиг в основной репозиторий автор пока [не разрешает](https://github.com/make-all/tuya-local/pulls?q=tuvio+label%3Asanctioned), потому что Россия под санкциями)

1. Увлажнитель нужно подключить через приложение SmartLife а не Tuvio
2. В HA установить [Tuya Local](https://www.youtube.com/watch?v=DvKf1nPx5c0) через HACS, не путайте с встроенной локальной туей, это не то.
3. Конфиг файл `.yaml` положить в `homeassistant/custom_components/tuya_local/devices`
   1. Если делаете первый раз то можно сначала просто добавить устройство, оно добавится но будет только кнопка вкл\выкл.
4. При добавлении может быть ошибка «Unable to connect to your device with those details», решается полным закрытием приложения SmartLife на телефоне
5. При выборе типа устройства нужно выбрать добавленный конфиг вместо абстрактного Humidifier. По идее он должен его выбрать автоматически определив устройство.

---

Как сделать конфиг на другое устройство, в общих чертах:

1. Привязываете устройство к SmartLife
2. Заходите на Tuya Developer Platform, регистрируетесь
3. На вкладке Cloud создаете проект  для разработок по умному дому.
4. В Devices => Link App Account подключаете ваш аккаунт SmartLife. Вы должны увидеть ваше устройство в Devices => All Devices. Копируете Device ID
5. Слева переходите на Cloud => Api Explorer. 
6. Device Control => Query Things Data Model. Вызываете по device_id, сохраняете model, это будет JSON [в виде строки](https://dadroit.com/string-to-json/), где будет описание всего что устройство умеет делать и показывать.
7. Собираете конфигурационный yaml, который описывает как model из Tuya мапится на entities HA. Помогут мой файл,
[документация tuya local](https://github.com/make-all/tuya-local/blob/main/custom_components/tuya_local/devices/README.md) и возможно [документация Home Asistant](https://developers.home-assistant.io/docs/core/entity/). LLM тоже без проблем пишет на 80% рабочий конфиг.