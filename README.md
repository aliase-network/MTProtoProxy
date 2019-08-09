# MTProtoProxy
Готовый вариант запуска собственного прокси-сервера на базе протокола MTProto.

### Что необходимо?
Для запуска собственного прокси-сервера, вам необходимо:

1. Абсолютно чистый сервер с ОС Ubuntu 16.04 или старше
2. Любой процессор/ОЗУ/диск (хотя бы: 1 ядро, 512 Мб ОЗУ, 5 ГБ диска)
3. Свободный порт и отсутствие любого файерволла (никакого NAT, желательно)

### Установка и запуск

1. `sudo apt-get -y update && sudo apt-get -y upgrade`
2. `sudo apt-get -y install curl && curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash`
3. `sudo apt-get install -y nodejs && npm install pm2 -g`
4. `cd && mkdir -p mtproto_org && cd mtproto_org`
5. `npm install @mtproto-org/mtproxy`
6. Создайте файл `mtproxy.js` и вставьте туда следующее:
```javascript
const mtproxy = require('@mtproto-org/mtproxy');

mtproxy()
```
7. Сохраните файл и выполните команду: `pm2 start mtproxy.js -i max`

#### Дополнительные настройки
Перейдите в папку, где лежит `mtproxy.js` и выполните одну из команд:

1. Запустить: `pm2 start mtproxy.js -i max`
2. Перезапустить: `pm2 restart mtproxy.js`
3. Выключить: `pm2 stop mtproxy.js`

### Что дальше?
По умолчанию:
1. Порт для подключения: `2233`
2. Секретный ключ: `11112222333344445555666677778888`

Для того чтобы изменить "порт" или "секретный ключ", смените переменную в `mtproxy()`:

  - `port`: (Number, **максимально до 5 числовых символов**)
  - `secret` : (String, **формат - hex32, обязательно 32 символа**)

Итоговый вариант, со своими переменными, выглядит так:
```javascript
const mtproxy = require('@mtproto-org/mtproxy');

mtproxy({
    port: 1234,
    secret: '11112222444455559999888877776666'
})
```


Вы можете поменять стандартный порт и секретный ключ, если хотите полной приватности. Рекомендуем сгенерировать секретный ключ из 32-х случайных чисел. Эти настройки установлены для тех, кому необходимо сразу запустить и пользоваться прокси-сервером.

### Как подключиться?
1. Перейдите в `Настройки`
2. Далее в `Продвинутые настройки`
3. Далее в `Тип соединения`
4. Выберите `Использовать собственный прокси`
5. `Добавить прокси`
6. Выберите `MTPROTO`
7. Хост - IP-адрес сервера или его `hostname`
8. Порт - ввежите порт прокси-сервера (по умолчанию: `2233`)
9. Ключ - введите ключ прокси-сервера (по умолчанию: `11112222333344445555666677778888`)
10. Нажмите кнопку `Сохранить`
11. Как только сервер добавится в список ваших прокси, выберите его и дождитесь статуса `Подключён`
12. Готово!

### Ревизия от Fossa

[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Fmtproto-org%2Fproxy.svg?type=large)](https://app.fossa.com/projects/git%2Bgithub.com%2Fmtproto-org%2Fproxy?ref=badge_large)

### Кто сделал? Мы
_**Aliase Network**: Open Source Initiative_<br>
_K.Sobolev & D.Shaymurzin for everyone_
