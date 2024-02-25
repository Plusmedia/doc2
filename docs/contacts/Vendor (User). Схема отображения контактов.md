---
tags:
  - contacts
  - vendor
  - user
---
## Лог изменений
|№|Изменение|Автор|Дата|
|---|---|---|---|
|1|Добавлена таблица правил|@Sergey Petrukhin|11.11.2023|
|2|—|Костикова Е.|16.11.2023|

## Пользовательская история

[GRK-444 Схема отображения контактов и быстрого запроса](https://pmcloud.atlassian.net/browse/GRK-444)

|Как|Менеджер проекта|
|---|---|
|Я хочу|Видеть в API набор флагов, на основании которых нужно выводить или не выводить тот или иной способ связи|
|Чтобы|Отображать на клиенте способы связи, в соответствии с типом страницы, типом размещения и доменом|

## Контекст

---

На клиентских приложениях не хватает критериев вывода, что приводит к появлению лишних контактов и быстрого запроса, там где они не нужны.

Тезисно:

- Логику вывода/скрытия конкретных контактов и быстрого запроса далее называем «Схема отображения»
- Схему отображения нужно хранить в едином месте — на бекенде или в базе данных
- Каждая схема должна иметь привязку к домену и городу (опционально) и содержать правила согласно таблице Rules
- API должно отдавать только нужные контакты, согласно схеме
- API должно также отдавать схему отображения в виде объекта с флагами в каждом методе, отдающим контакты непосредственно или в виде embed. Флаги приведены в таблице Parameters, а запросы в таблице API)
- Чтобы протестировать реализацию, помимо схемы в API, нужно вывести в панель администратора тип размещения заведения для тестировщика

## Rules
|domain == [gorko.ru](http://gorko.ru) && pessimism == false|
|---|

|Размещение|Бесплатное|Платное|
|---|---|---|
|Признак в базе|top == 0|top == 1|
|Способ связи (Mobile)|Окно контактов [ОК]|Окно контактов [ОК]|
|Способ связи (Desktop)|Окно контактов [ОК]|Окно контактов [ОК]|
|[ОК] Основной телефон|✔️Да|✔️Да|
|[ОК] Мессенджеры|✔️Да|✔️Да|
|[ОК] Личные сообщения|✔️Да|✔️Да|
|[ОК] Дополнительные контакты|✔️Да|✔️Да|

|domain == [gorko.ru](http://gorko.ru) && cities == all && pessimism == true|
|---|

|Размещение|Бесплатное|Платное|
|---|---|---|
|Признак в базе|top == 0|top == 1|
|Способ связи (Mobile)|Окно контактов [ОК]|Окно контактов [ОК]|
|Способ связи (Desktop)|Окно контактов [ОК]|Окно контактов [ОК]|
|[ОК] Основной телефон|✔️Да|✔️Да|
|[ОК] Мессенджеры|❌Нет|✔️Да|
|[ОК] Личные сообщения|✔️Да|✔️Да|
|[ОК] Дополнительные контакты|❌Нет|✔️Да|

|domain in [[wedpro.com.ua](http://wedpro.com.ua), [belwed.com](http://belwed.com), [kzwed.com](http://kzwed.com), [slubowisko.pl](http://slubowisko.pl)], cities == all|
|---|

|Размещение|Бесплатное|Платное|
|---|---|---|
|Признак в базе|top == 0|top == 1|
|Способ связи (Mobile)|Окно контактов [ОК]|Окно контактов [ОК]|
|Способ связи (Desktop)|Окно контактов [ОК]|Окно контактов [ОК]|
|[ОК] Основной телефон|✔️Да|✔️Да|
|[ОК] Мессенджеры|✔️Да|✔️Да|
|[ОК] Личные сообщения|✔️Да|✔️Да|
|[ОК] Дополнительные контакты|✔️Да|✔️Да|

|domain == [centerwedding.com](http://centerwedding.com), cities == all|
|---|

|Размещение|Бесплатное|Платное|
|---|---|---|
|Признак в базе|top == 0|top == 1|
|Способ связи (Mobile)|Окно контактов [ОК]|Окно контактов [ОК]|
|Способ связи (Desktop)|Окно контактов [ОК]|Окно контактов [ОК]|
|[ОК] Основной телефон|✔️Да|✔️Да|
|[ОК] Мессенджеры|✔️Да|✔️Да|
|[ОК] Личные сообщения|✔️Да|✔️Да|
|[ОК] Дополнительные контакты|✔️Да|✔️Да|


## API
Методы требующие вывода схемы

|Метод|Пример вызова|Платформа|
|---|---|---|
|…/v3/vendorcard|[https://api.gorko.ru/api/v3/vendorcard?entity[cityId]=4917&entity[languageId]=1&entity[specKey]=0&list[cityId]=4917&list[filters]=service%3D0&list[page]=1&list[perPage]=20&list[seed]=668297&list[typeId]=5](https://api.gorko.ru/api/v3/vendorcard?entity%5BcityId%5D=4917&entity%5BlanguageId%5D=1&entity%5BspecKey%5D=0&list%5BcityId%5D=4917&list%5Bfilters%5D=service%3D0&list%5Bpage%5D=1&list%5BperPage%5D=20&list%5Bseed%5D=668297&list%5BtypeId%5D=5)|Mobile, Desktop|
|…/v2/users/user_id|[https://api.gorko.ru/api/v2/users/239095?embed=&fields=coords,busy,has_free_date&city_id=4400](https://api.gorko.ru/api/v2/users/239095?embed=&fields=coords,busy,has_free_date&city_id=4400)|Mobile, Desktop|
|…/v2/media/media_id/neighbor|[https://api.gorko.ru/api/v2/media/52336933/neighbor?next_limit=1&order=position&prev_limit=1&type=album&embed=album%2Calbum.belong_to%2Clikes(limit%3A6)%2CmediaFeed%2Cuser.contacts%2Cuser.feedback_list&preview_size=50x50%2Cb&fields=my_vote&city_id=3912](https://api.gorko.ru/api/v2/media/52336933/neighbor?next_limit=1&order=position&prev_limit=1&type=album&embed=album%2Calbum.belong_to%2Clikes(limit%3A6)%2CmediaFeed%2Cuser.contacts%2Cuser.feedback_list&preview_size=50x50%2Cb&fields=my_vote&city_id=3912)|Desktop|
|…/v2/media/media_id/neighbor5|[https://api.gorko.ru/api/v2/media/52336933/neighbor5?embed=user.contacts%2Cuser.feedback_list%2Calbum%2Clikes(limit%3A6)%2CmediaFeed&preview_size=50x50%2Cb&prev_limit=30&next_limit=30&prev_offset=0&next_offset=0&order=-id&type=album&city_id=3912](https://api.gorko.ru/api/v2/media/52336933/neighbor5?embed=user.contacts%2Cuser.feedback_list%2Calbum%2Clikes(limit%3A6)%2CmediaFeed&preview_size=50x50%2Cb&prev_limit=30&next_limit=30&prev_offset=0&next_offset=0&order=-id&type=album&city_id=3912)|Desktop|
|.../v2/albums/album_id|[https://api.gorko.ru/api/v2/albums/2083183?embed=user.feedback_list,user.contacts&fields=spouses,my_link_confirm,belong_to](https://api.gorko.ru/api/v2/albums/2083183?embed=user.feedback_list,user.contacts&fields=spouses,my_link_confirm,belong_to)|Desktop|

В выдаче апи в каждой модели есть атрибут со схемой контактов
```json
v2
contact_schema: {
  "id": 9,
  "main_method_desktop": "contacts",
  "main_method_mobile": "call",
  "is_show_phone": true,
  "is_show_messengers": false,
  "is_show_contacts": false,
  "add_contacts": null
}
v3
contactSchema: {
  "main_method_desktop": "contacts",
  "main_method_mobile": "call",
  "is_show_phone": true,
  "is_show_messengers": false,
  "is_show_contacts": false,
  "add_contacts": null
}
```

## Parameters
|Параметр|Описание|Тип|
|---|---|---|
|showMainPhone|Основной телефон|Boolean|
|showMessengers|Мессенджеры|Boolean|
|showLine|Единый Line (Таиланд)|Boolean|
|showPM|Личные сообщения|Boolean|
|showAdditionalContacts|Дополнительные контакты|Boolean|
|showQuickInquiry|Быстрый запрос|Boolean|

![[venue_contacts.png|venue_contacts.png]]