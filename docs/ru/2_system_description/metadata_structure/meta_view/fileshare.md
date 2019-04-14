#### [Оглавление](/docs/ru/index.md)

### Предыдущая страница: [Опции](/docs/ru/2_system_description/metadata_structure/meta_view/options.md)

## Ведение проектных документов

**Ведение проектных документов** - это настройка `"fileshare-list"` и `"fileshare"` предназначена для управления документами, как например возможность скачать и/или получить ссылку на файл. Для настройки, в представлении атрибута типа "Файл" необходимо указать свойство:

```
 "options": {
              "template": "fileshare-list"
            }
```
* `fileshare-list` - для типа `multifile` - множественные файлы
* `fileshare` - для типа `file` - один файл

В `deploy.json` в настройках `registry` подключаем кастомный файл-аплоадер (который с шарой директории и расширенными настройками):

```
  "modules": {
    "registry": {
      "globals": {
        ...
        "di": {
          ...
          "fileshareController": {
            "module": "applications/viewlib/lib/controllers/api/fileshare",
            "initMethod": "init",
            "initLevel": 0,
            "options": {
              "module": "ion://module",
              "fileStorage": "ion://fileStorage"
            }
          }
```

## Cохранение файлов в облаке

Путь для сохранения файла в облаке настраивается в `deploy.json` приложения. Для обращения к свойствам объекта используется знак `$`.

```
{item.названиеСвойства.свойствоСсылочногоОбъекта}
```
т.е. используем `${item.}` для того чтобы обозначить что это обращение к объекту.

### Пример:

```json
"modules": {
    "registry": {
      "globals": {
        "storage": {
          "basicObj@project-management": {
            "cloudFile": "/${class}/pm_${attr}/${dddd}/"
          },
          "project@project-management": {
            "cloudFile": "/${item.name} (${item.code})/"
          },
          "eventControl@project-management": {
            "cloudFile": "/${class}/pm_${attr}/${dddd}/"
          },
          "eventOnly@project-management": {
            "cloudFile": "/${class}/pm_${attr}/${dddd}/"
          }
        }
      }
    }
 }
```
_Настройка позволяет задавать любую структуру хранения файлов (линейно/иерархически, коллекцией/один файл)_



## Функционал шаринга на файлы

### Подключение

В представлении необходимо задать свойство атрибута типа `"Файл"`:
```
"tags": [
            "share"
          ],
```
### Использование

При клике на значок "share" необходимо открывать окно управления шарой аналогичное как в овнклауд - в окне предусмотреть кнопки:
* `применить` - по апи облачного хранилища для файлика/каталога передаем все выбранные параметры:
* `поделиться ссылкой` - формируем шару на файлик/каталог - после применения возвращаем в поле для возможности копирования ссылки
* `разрешить на редактирование`
* `защитить паролем `- поле для ввода пароля
* `установить срок действия` - поле для даты
* `перейти в хранилище` - открываем в новой вкладке по ссылке на шару где находится файл/каталог - ( к примеру файл к примеру каталог )
* `закрыть` - закрыть окно управления файлом

**NB:** Настройка шаринга доступна как для каждого файла, так и для всего каталога. Если на файле/каталоге уже есть шаринг то при открытии управляющего окна отображаются настройки шаринга, при необходимости свойства можно изменить.

## Переход по прямой ссылки до хранения файла

### Возможности

* сразу скачать

* перейти на nextCloud и там увидеть/редактировать

### Условия хранения ссылок

Условия хранения ссылок, созданных в процессе работы с файлами: `TO DO` возможность удалять все ссылки, созданные в процессе работы с файлом спустя какое-то время или же за ненадобностью.

### Настройка доступа

Настройка пользователей и прав доступа к объектам хранилища Owncloud. В ряде случаев необходимо задавать пользователей и права для них на создаваемые объекты хранилища.

Настройка задается в файле `deploy.json` проекта. 

### Пример:

```json
"ownCloud": {
  "module": "core/impl/resource/OwnCloudStorage",
  "options": {
   ...
     "users": [
        {
           "name": "user",
           "permissions": {
              "share": true,
              "create": false,
              "edit": true,
              "delete": false
           }
         }
      ]
   }
}
```

### Следующая страница: [Комментарии](/docs/ru/2_system_description/metadata_structure/meta_view/comments.md)

--------------------------------------------------------------------------  


 #### [Licence](/LICENCE.md) &ensp;  [Contact us](https://iondv.com) &ensp;  [Russian](/docs/ru/2_system_description/metadata_structure/meta_view/fileshare.md)   &ensp; [FAQs](/faqs.md)  <div><img src="https://mc.iondv.com/watch/local/docs/framework" style="position:absolute; left:-9999px;" height=1 width=1 alt="iondv metrics"></div>         



--------------------------------------------------------------------------  

Copyright (c) 2018 **LLC "ION DV"**.  
All rights reserved. 