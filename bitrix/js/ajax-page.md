[главная](../../readme.md)

# Пример страницы для ajax

```php
define('NO_KEEP_STATISTIC', 'Y');
define('NO_AGENT_STATISTIC', true);
define('STOP_STATISTICS', true);
define('PUBLIC_AJAX_MODE', true);
define('NO_AGENT_CHECK', true);
define('NOT_CHECK_PERMISSIONS', true);
if (empty($_SERVER['DOCUMENT_ROOT'])) {
    $_SERVER['DOCUMENT_ROOT'] = realpath(__DIR__.'/../');
}
require($_SERVER['DOCUMENT_ROOT'] . '/bitrix/modules/main/include/prolog_before.php');
```