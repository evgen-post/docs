[главная](../../readme.md)

# Консольные команды

### Архив с 1с-битрикс

```(bash)
tar czf bitrix.tar.gz --exclude="./bitrix/catalog_export" --exclude="./bitrix/backup" --exclude="./bitrix/cache" --exclude="./bitrix/stack_cache" --exclude="./bitrix/managed_cache" --exclude="./bitrix/updates" --exclude="./bitrix/tmp" ./bitrix
```

### Добавление нового модуля на основе базового модуля

```(bash)
composer create-project evk/dummy-bx-base-module example/local/modules/ds.base "dev-master"
```

`evk/dummy-bx-base-module` - composer пакет

`example/local/modules/ds.base` - директория, куда будет установлен модуль.

`ds.base` - папка модуля. можно указать любое название по правилам именования модулей партнёров. (`partner_name.module_name`)

### Распаковка архива с базовыми компонентами

```(bash)
cd project/local/components/system/
git archive --format=tar --remote="git@gitlab.com:evkv/base-components.git" master | tar -xC "./"
```

### Распаковка архива с базовым компонентом complex

```(bash)
cd project/local/components/system/
mkdir complex
cd complex
git archive --format=tar --remote="git@gitlab.com:evkv/base-components.git" master complex | tar -xC "./"
```

#### Доступный список компонентов

- complex
- multilevel.cache.list
- standard.elements.list
