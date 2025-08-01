# Конфигурация

Сервисы, иконки, язык и прочие настройки задаются в едином файле `config.yml`.
Его необходимо передать в docker контейнер, как это сделать указано в разделе [начало работы](../guide/getting-started.md).

## Заголовок

При желании вы можете настроить заголовок страницы.

```yaml
title: Моя домашняя страница
```

Значение по умолчанию: `Mafl Home Page`

## Язык

Установите нужный язык с помощью:

```yaml
lang: ru
```

Поддерживаемые значения: `en`, `ru`, `zh`, `hi`, `es`, `ar`, `pl`, `fr`, `de`, `gr`, `nl`, `hu`

Значение по умолчанию: `en`

## Тема оформления

Вы можете настроить фиксированные темы, передав опцию `theme`, как показано ниже:

```yaml
theme: dark
```

Поддерживаемые значения: `system`, `light`, `dark`, `deep`, `sepia`, `bluer`

Значение по умолчанию: `system`

## Поверка обновлений

Данный параметр отвечает за автоматическую проверку обновлений.
Если появится новая версия, то внизу экрана появится сообщение с новой версией.

```yaml
checkUpdates: true
```

Значение по умолчанию: `true`

::: info Пояснение
С параметром `true` автоматического обновления не будет.
Если хотите, чтобы система могла обновляться сама, то рекомендуем воспользоваться [watchtower](https://containrrr.dev/watchtower/).
:::

## Поведение

Группа параметров отвечающих за поведение приложения.

### Target <in-version value="0.7.6" />

Поведение браузера при нажатии на сервис.
С помощью этого свойства, можно сделать открытие сервиса в текущем или новом окне.

```yaml
behaviour:
  target: _blank
```

Поддерживаемые значения:

| Значение  | Описание                                                                                                                |
|-----------|-------------------------------------------------------------------------------------------------------------------------|
| `_blank`  | Загружает страницу в новое окно браузера                                                                                |
| `_self`   | Загружает страницу в текущее окно                                                                                       |
| `_parent` | Загружает страницу во фрейм-родитель, если фреймов нет, то это значение работает как `_self`                            |
| `_top`    | Отменяет все фреймы и загружает страницу в полном окне браузера, если фреймов нет, то это значение работает как `_self` |

Значение по умолчанию: `_blank`

::: warning Внимание
Если в сервисе определено поле `target`, то оно будет являться приоритетным. Подробнее можно прочитать в [базовом сервисе](../services/base.md#target)
:::

## Теги <in-version value="0.10.0" />

Теги позволяют разграничивать сервисы.

```yaml
tags:
  - name: Домашние
    color: green
  - name: Рабочее
    color: blue
```

::: info Информация
Более подробно о тегах можно прочитать в [разделе](../reference/tags.md).
:::

## Макет <in-version value="0.14.0" />

Группа параметров отвечающих за макет приложения.

### Сетка

Позволяет настроить количество колонок на разных разрешениях экрана.

```yaml
layout:
  grid:
    small: 2
    medium: 2
    large: 3
    xlarge: 4
```

Поддерживаемые значения: диапазон `1 - 12`

Вы можете указать только одно значение, остальные будут установлены автоматически.

## Сервисы

Все сервисы, которые отображаются на главной странице задаются в данном параметре.
Он поддерживает как список, так и группировку. Кол-во сервисов не ограниченно.

::: warning Список сервисов
Полный список всех сервисов можно посмотреть в левой боковой колонке в разделе **Сервисы**.
Рекомендуем начать ознакомления с [базового сервиса](../services/base.md), на котором основываются все остальные.
:::

### Список
```yaml
services:
  - title: Home Assistant
    description: Автоматизация дома
    link: https://home-assistant.home.local/
```

### Группировка

```yaml
services:
  Группа 1:
    - title: Home Assistant
      description: Автоматизация дома
      link: https://home-assistant.home.local/
  Группа 2:
    - title: Home Assistant
      description: Автоматизация дома
      link: https://home-assistant.home.local/
```

Это обязательный параметр и без него домашняя страница не отроется.
Более развернутые примеры можно посмотреть ниже.

## Примеры

### Список

Конфигурация в которой все сервисы расположены на одном уровне.

::: code-group
```yaml [config.yml]
title: Моя домашняя страница
services:
  - title: Home Assistant
    description: Автоматизация дома
    link: https://home-assistant.home.local/
    icon:
      name: simple-icons:homeassistant
      wrap: true
      color: '#3dbcf3'
    status:
      enabled: true
  - title: Сетевое хранилище
    description: Synology DS223
    link: https://nas.home.local/
    icon:
      name: mdi:nas
      wrap: true
    status:
      enabled: true
```
:::

### Группировка

Простая конфигурация с создаем двух групп `Сервисы` и `Устройства`.

::: code-group
```yaml [config.yml]
title: Моя домашняя страница
services:
  Сервисы:
    - title: Home Assistant
      description: Автоматизация дома
      link: https://home-assistant.home.local/
      icon:
        name: simple-icons:homeassistant
        wrap: true
        color: '#3dbcf3'
      status:
        enabled: true
  Устройства:
    - title: Роутер
      description: Keenetic Peak
      link: http://192.168.1.1/
      icon:
        name: mdi:router-network
        wrap: true
    - title: Сетевое хранилище
      description: Synology DS223
      link: https://nas.home.local/
      icon:
        name: mdi:nas
        wrap: true
      status:
        enabled: true
```
:::
