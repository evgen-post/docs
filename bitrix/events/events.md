[главная](../../readme.md)

Получить список обработчиков событий для модуля по названию события
-
```php
$eventManager = \Bitrix\Main\EventManager::getInstance();
$events = $eventManager->findEventHandlers('iblock', 'OnBeforeIBlockElementAdd');
```
