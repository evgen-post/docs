[главная](../readme.md)

# Консольные команды

### Извлечение файла из git

Извлечь файл (`database.sql`) из репозитория (`git@gitlab.digital-sector.ru:example/example_database.git`) из ветки master в каталог `../docker/data/mysql/dump/`
Если не указывать конкретный файл, то будет извлечён весь репозиторий.

```(bash)
git archive --remote=git@gitlab.digital-sector.ru:example/example_database.git master database.sql | tar -xC "../docker/data/mysql/dump/"
```

### Просмотр сертификата домена

```(bash)
openssl s_client -connect www.yandex.ru:443
```

### Dump mysql

```(bash)
export MYSQL_PWD='password'; mysql -u login database < database.sql
export MYSQL_PWD='password'; mysqldump -u login database > database.sql
```

### Проверка скорости работы ssh соединения
```shell
yes | pv | ssh remote_host "cat >/dev/null"
```

### Рекурсивный поиск подстроки в файлах в директории
Поиск подстроки "N1325764" в файлах, находящихся в директории log с исключёнными директориями rcrm_order,api,mindbox,rcrm.
```shell
grep -rnw log -e 'N1325764' --exclude-dir={rcrm_order,api,mindbox,rcrm}
```
Итого будут проигнорированы такие директории как log/rcrm_order, log/api, log/mindbox, log/rcrm
