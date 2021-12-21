[главная](../../readme.md)

# Получить список всех кастомных событий библиотеки BX (javascript)

```php
<?php
\Bitrix\Main\Page\Asset::getInstance()->addString(<<<HTML
<script>
BX.ready(function(){
    // Лог событий.
    var originalBxOnCustomEvent = BX.onCustomEvent;
    BX.onCustomEvent = function (eventObject, eventName, eventParams, secureParams) {
        var logData = {
            eventObject: eventObject,
            eventName: eventName,
            eventParams: eventParams,
            secureParams: secureParams
        };
        if (eventObject !== null && typeof eventObject == 'object' && eventObject.constructor) {
        logData['eventObjectClassName'] = eventObject.constructor.name;
    }
    console.log(logData);
    originalBxOnCustomEvent.apply(null, [eventObject, eventName, eventParams, secureParams]);
};
});
</script>
HTML
, false, \Bitrix\Main\Page\AssetLocation::AFTER_JS);
```