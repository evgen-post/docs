[главная](../../readme.md)

# Визуальный редактор битрикс

## Запретить обработку указанных тегов

Запретить обработку тегов: span, svg, use.

```php
\Bitrix\Main\Page\Asset::getInstance()->addString(<<<HTML
<script>
BX.addCustomEvent('OnEditorInitedBefore', function(toolbar) {
    var _this = this;
    BX.addCustomEvent(this, 'OnGetParseRules', BX.proxy(function() {
        _this.rules.tags.span = {};
        _this.rules.tags.svg = {};
        _this.rules.tags.use = {};
    }, this));
});
</script>
HTML
);
```