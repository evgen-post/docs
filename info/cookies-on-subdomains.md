[главная](../readme.md)

## Вводная информация

С поддоменов можно устанавливать куки как для самого адреса поддомена, видимого этому поддомену и его поддоменам, так и **для вышестоящих доменов.**

Например:


* Установка куки с домена `a.b.c.ru` для домена `a.b.c.ru` будет видна только этому домену и его поддоменам.
* Установка куки с домена `a.b.c.ru` для домена `c.ru` будет видна главному домену и всем его поддоменам.

**Итого**

Куки можно устанавливать с любого уровня домена для любого вышестоящего домена или для самого себя.

`a.b.c.ru` может установить куку для

```text
a.b.c.ru
b.c.ru
c.ru
```

Но не для

```text
f.d.c.ru
d.c.ru
```

**Однако, установив куку для `c.ru`, данная кука будет доступна всем поддоменам.** Таким образом, через главный домен можно передать куку на поддомен любого уровня.

С вышестоящих доменов нельзя устанавливать куки для поддоменов с указанием адреса поддомена, но это и не требуется, так как любая кука домена верхнего уровня будет доступна домену нижнего уровня, если при установке был указан адрес домена верхнего уровня.

# Небольшой тест


## Установка кук с главного домена (домена второго уровня)


**evk-api.localhost**

```php
$time = time()+60*60*24*30;
$domainLevel = 2;
$cookies = [
    ['domain-level-'.$domainLevel, 'evk-api.localhost',],
    ['dot_domain-level-'.$domainLevel, '.evk-api.localhost',],
    ['api_domain-level-'.$domainLevel, 'api.evk-api.localhost',],
    ['dot_api_domain-level-'.$domainLevel, '.api.evk-api.localhost',],
    ['sub_domain-level-'.$domainLevel, 'sub.evk-api.localhost',],
    ['dot_sub_domain-level-'.$domainLevel, '.sub.evk-api.localhost',],
    ['sub_api_domain-level-'.$domainLevel, 'sub.api.evk-api.localhost',],
    ['dot_sub_api_domain-level-'.$domainLevel, '.sub.api.evk-api.localhost',],
];
foreach ($cookies as $cookie) {
    setcookie($cookie[0], $cookie[1], $time, '/', $cookie[1]);
}
```

При подобной попытке установить куки

Успешно установлены только две.

```php
['domain-level-'.$domainLevel, 'evk-api.localhost',],
['dot_domain-level-'.$domainLevel, '.evk-api.localhost',],
```

### Видимость

Данные куки видны для самого главного домена, так же как и для всех поддоменов любого уровня.

## Установка кук с поддомена (домена третьего уровня)

**api.evk-api.localhost**

```php
$time = time()+60*60*24*30;
$domainLevel = 3;
$cookies = [
    ['domain-level-'.$domainLevel, 'evk-api.localhost',],
    ['dot_domain-level-'.$domainLevel, '.evk-api.localhost',],
    ['api_domain-level-'.$domainLevel, 'api.evk-api.localhost',],
    ['dot_api_domain-level-'.$domainLevel, '.api.evk-api.localhost',],
    ['sub_domain-level-'.$domainLevel, 'sub.evk-api.localhost',],
    ['dot_sub_domain-level-'.$domainLevel, '.sub.evk-api.localhost',],
    ['sub_api_domain-level-'.$domainLevel, 'sub.api.evk-api.localhost',],
    ['dot_sub_api_domain-level-'.$domainLevel, '.sub.api.evk-api.localhost',],
];
foreach ($cookies as $cookie) {
    setcookie($cookie[0], $cookie[1], $time, '/', $cookie[1]);
}
```

При подобной попытке установить куки

Успешно установлены только четыре.

```php
['domain-level-'.$domainLevel, 'evk-api.localhost',],
['dot_domain-level-'.$domainLevel, '.evk-api.localhost',],
['api_domain-level-'.$domainLevel, 'api.evk-api.localhost',],
['dot_api_domain-level-'.$domainLevel, '.api.evk-api.localhost',],
```

### Видимость

Для главного домена доступны только две установленные куки

```php
['domain-level-'.$domainLevel, 'evk-api.localhost',],
['dot_domain-level-'.$domainLevel, '.evk-api.localhost',],
```

Для поддоменов данного поддомена доступны все четыре установленные куки.

## Установка кук с поддомена (домена четвёртого уровня)

**sub.api.evk-api.localhost**

```php
$time = time()+60*60*24*30;
$domainLevel = 4;
$cookies = [
    ['domain-level-'.$domainLevel, 'evk-api.localhost',],
    ['dot_domain-level-'.$domainLevel, '.evk-api.localhost',],
    ['api_domain-level-'.$domainLevel, 'api.evk-api.localhost',],
    ['dot_api_domain-level-'.$domainLevel, '.api.evk-api.localhost',],
    ['sub_domain-level-'.$domainLevel, 'sub.evk-api.localhost',],
    ['dot_sub_domain-level-'.$domainLevel, '.sub.evk-api.localhost',],
    ['sub_api_domain-level-'.$domainLevel, 'sub.api.evk-api.localhost',],
    ['dot_sub_api_domain-level-'.$domainLevel, '.sub.api.evk-api.localhost',],
];
foreach ($cookies as $cookie) {
    setcookie($cookie[0], $cookie[1], $time, '/', $cookie[1]);
}
```

При подобной попытке установить куки

Успешно установлены шесть кук.

```php
['domain-level-'.$domainLevel, 'evk-api.localhost',],
['dot_domain-level-'.$domainLevel, '.evk-api.localhost',],
['api_domain-level-'.$domainLevel, 'api.evk-api.localhost',],
['dot_api_domain-level-'.$domainLevel, '.api.evk-api.localhost',],
['sub_api_domain-level-'.$domainLevel, 'sub.api.evk-api.localhost',],
['dot_sub_api_domain-level-'.$domainLevel, '.sub.api.evk-api.localhost',],
```

### Видимость

Для главного домена доступны только две установленные куки

```php
['domain-level-'.$domainLevel, 'evk-api.localhost',],
['dot_domain-level-'.$domainLevel, '.evk-api.localhost',],
```

Для верхнего поддомена третьего уровня доступны четыре куки

```php
['domain-level-'.$domainLevel, 'evk-api.localhost',],
['dot_domain-level-'.$domainLevel, '.evk-api.localhost',],
['api_domain-level-'.$domainLevel, 'api.evk-api.localhost',],
['dot_api_domain-level-'.$domainLevel, '.api.evk-api.localhost',],
```
