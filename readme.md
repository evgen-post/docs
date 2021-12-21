# Содержание

Раздел для битрикс
-
- [Ядро D7](bitrix/core-d7/readme.md)
- [Ядро Bitrix (старое ядро)](bitrix/core-bx/readme.md)
- Работа с js
  - [Пример страницы для ajax](bitrix/js/ajax-page.md)
  - [Запретить перемещение определённого тега js вниз на странице](bitrix/js/js-skip-moving.md)
  - [Получить список всех кастомных событий библиотеки BX (javascript)](bitrix/js/get-bx-custom-events.md)
- Работа с событиями
  - [Получить список обработчиков событий для модуля по названию события]()
- Работа с текстом
  - [Склонение существительных (plural)](bitrix/texts/plural.md)
- [Визуальный редактор](bitrix/visual-text-editor/visual-text-editor.md)
- [Консольные команды](bitrix/console/readme.md)
- [Общая информация по СЕО](bitrix/ceo/ceo.md)

Консольные команды:
-
- [Для битрикс](bitrix/console/readme.md)
- [Общего назначения](console/readme.md)

Подключение xdebug (phpstorm - docker - xdebug)
-
- [Настройка xdebug на docker-контейнер](docker/xdebug/xdebug.md)

Куки на поддоменах (Cookies on subdomains)
- 
- [Куки на поддоменах (Cookies on subdomains)](info/cookies-on-subdomains.md)

Работа с сертификатами безопасности
-
- Проверка поддерживаемых алгоритмнов шифрования в php
```php
print_r(join("<br/>", openssl_get_md_methods()));
```