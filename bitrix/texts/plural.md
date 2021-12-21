[главная](../../readme.md)

# Склонение существительных (plural)

```php
use Bitrix\Main\Grid\Declension;
$year = 11;
$yearDeclension = new Declension('год', 'года', 'лет');
$yearDeclension->get($year);
```