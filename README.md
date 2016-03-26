[![Stars](https://img.shields.io/github/stars/oknosoft/metadata.js.svg?label=Github%20%E2%98%85&a)](stargazers)
[![Release](https://img.shields.io/github/tag/oknosoft/metadata.js.svg?label=Last%20release&a)](releases)
[![NPM downloads](http://img.shields.io/npm/dm/metadata-js.svg?style=flat&label=npm%20downloads)](https://npmjs.org/package/metadata-js?)
[![NPM version](https://img.shields.io/npm/l/metadata-js.svg?)](http://licenseit.ru/wiki/index.php/GNU_Affero_General_Public_License_version_3)

**Metadata.js** - это библиотека для разработки бизнес-ориентированных и учетных offline-first браузерных приложений

[English version](README.en.md)

### Почему Metadata.js?
Metadata.js - это JavaScript реализация [Объектной модели 1С](http://v8.1c.ru/overview/Platform.htm). Библиотека эмулирует для веб-программиста наиболее востребованные классы API 1С внутри браузера или Node.js, дополняя их средствами автономной работы и  обработки данных на клиенте.

### Для кого?
Библиотека ориентирована на разработчиков браузерных бизнес-приложений, которым близка парадигма разработки 1С, но которым тесно в рамках традиционной платформы 1С. Metadata.js предоставляет программисту:
- высокоуровневые [data-объекты](http://www.oknosoft.ru/upzp/apidocs/modules/metadata.html), схожие по функциональности с документами, регистрами и справочниками платформы 1С
- инструменты декларативного описания метаданных и автогенерации интерфейса, схожие по функциональности с метаданными и формами платформы 1С 
- средства событийно-целостной репликации и эффективные классы обработки данных, не имеющие прямых аналогов в 1С 

## Предпосылки
Проект начинался с реализации лёгкого javascript клиента 1С (в дополнение к толстому, тонкому и веб-клиентам) и предназначался для чтения и редактирования данных, расположенных на [сервере 1С](http://v8.1c.ru/overview/Term_000000033.htm) с большим числом подключений (дилеры или интернет-витрина с сотнями анонимных либо авторизованных внешних пользователей).
Позже, была реализована математика, использующая в качестве сервера хранилище данных на базе [CouchDB](http://couchdb.apache.org/) и [PouchDB](http://pouchdb.com/) с поддержкой прозрачной в реальном времени синхронизации с 1С.
   
## Концепция и философия
> В metadata.js предпринята попытка дополнить лучшее из современных технологий обработки данных инструментами, которых нам не хватало в повседневной работе

![Структура системы на базе metadata.js](examples/imgs/metadata_infrastructure.png)

![Структура metadata.js в браузере](examples/imgs/metadata_structure.png)
 
### Используем самое ценное от 1С
- Эффективная модель *Метаданных* со *ссылочной типизацией* и *подробным описанием реквизитов*
- Высокоуровневая объектная модель данных. Предопределенное (при необходимости, переопределяемое) поведение *Документов*, *Регистров*, *Справочников* и *Менеджеров объектов*, наличие *стандартных реквизитов* и *событий*, повышает эффективность разработки *в разы* по сравнению с фреймворками, оперирующими записями реляционных таблиц
- Автогенерация форм и элементов управления
 
Чтобы предоставить разработчику на javascript инструментарий, подобный 1С-ному, на верхнем уровне фреймворка реализованы классы:
- [AppEvents](http://www.oknosoft.ru/upzp/apidocs/classes/AppEvents.html), обслуживающий события при старте программы, авторизацию пользователей и состояния сети
- [Meta](http://www.oknosoft.ru/upzp/apidocs/classes/Meta.html) - хранилище метаданных конфигурации
- [DataManager](http://www.oknosoft.ru/upzp/apidocs/classes/DataManager.html) с наследниками `RefDataManager`, `EnumManager`, `InfoRegManager`, `CatManager`, `DocManager` - менеджеры объектов данных - аналоги 1С-ных `ПеречислениеМенеджер`, `РегистрСведенийМенеджер`, `СправочникМенеджер`, `ДокументМенеджер`
- [DataObj](http://www.oknosoft.ru/upzp/apidocs/classes/DataObj.html) с наследниками `CatObj`, `DocObj`, `EnumObj`, `DataProcessorObj` - аналоги 1С-ных `СправочникОбъект`, `ДокументОбъект`, `ОбработкаОбъект`

### Дополняем возможностями ES2015 и Web UI
- При разработке фреймворка, было решено отказаться от поддержки устаревших браузеров и смело использовать расширения javascript ES2015. Это позволило сократить объём кода, улучшить его структуру и повысить эффективность
- Для визуализации данных, в текущей реализации, использованы компоненты [dhtmlx](http://dhtmlx.com/). Любители ExtJS, Angular, Dojo, Webix, SAP UI5 и т.д. - могут при необходимости подключить нужные визуальные компоненты к нашим объектам данных
 
### Отличия от конкурентов
Metadata.js не конкурирует с клиентскими [Web UI](https://ru.wikipedia.org/wiki/%D0%A1%D1%80%D0%B0%D0%B2%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5_%D0%BA%D0%B0%D1%80%D0%BA%D0%B0%D1%81%D0%BE%D0%B2_%D0%B2%D0%B5%D0%B1-%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9) и клиент-серверными (в том числе, реактивными) фреймворками, а дополняет их новой абстракцией в виде [Объектов](http://www.oknosoft.ru/upzp/apidocs/classes/DataObj.html) и [Менеджеров](http://www.oknosoft.ru/upzp/apidocs/classes/DataManager.html) данных. Использование этих классов упрощает разработку сложных интерфейсов бизнес-приложений

## Установка и подключение

```bash
npm install --save metadata-js  # node
bower install --save metadata   # bower
```

Для браузера, подключите таблицы стилей `fontawesome`, `dhtmlx`, `metadata` и скрипты `alasql`, `dhtmlx`, `metadata`  

```html
<link rel="stylesheet" type="text/css" href="//cdn.jsdelivr.net/fontawesome/latest/css/font-awesome.min.css">
<link rel="stylesheet" type="text/css" href="//cdn.jsdelivr.net/g/metadata(dhx_web.css+metadata.css)">
<script src="//cdn.jsdelivr.net/g/alasql,metadata(dhtmlx.min.js+metadata.min.js)"></script>
```

## Web-приложение к серверу 1С - это просто
- Подключите скрипт с файлами описания метаданных ([см. демо](examples/unf)) и получите полнофункциональное приложение с бизнес-логикой, реализованной средствами 1С в конфигураторе 1С и отзывчивым интерфейсом, который автоматически сгенерирует библиотека metadata.js
- С фреймворком metadata.js легко создавать системы на сотни и даже тысячи рабочих мест, используя высокоуровневые инструменты платформы 1С на сервере, сочетая их с гибкостью, эффективностью и доступностью браузерных технологий
- Для типовых конфигураций на полной поддержке используется rest-сервис odata
   + Файлы описания метаданных, в этом случае, формируются внешней обработкой, входящей в комплект поставки
- Если внесение изменений в типовую конфигурацию допустимо, используется http-сервис библиотеки интеграции
   + На клиенте и сервере в этом случае, доступны дополнительные функции оптимизации вычислений, трафика и кеширования

## Презентация
[![Обзор metadata.js](examples/imgs/metadata_slideshare.jpg)](http://www.slideshare.net/ssuser7ad218/metadatajs)

## Примеры
- Приложение [code examples](examples/codex) дополняет документацию простыми примерами использования и настройки компонентов фреймворка а так же, примерами подключения к типовым конфигурациям 1С  
- На примере [Заказа покупателя в УНФ](examples/unf), расмотрено:
   + Как сформировать файлы описания метаданных
   + Как выгрузить статические данные перечислений и справочников для кеширования на клиенте
   + Как по описанию метаданных сформировать SQL-файл для создания таблиц data-объектов в памяти браузера
   + Какие и в какой последовательности возникают события при старте приложения, при авторизации и построении начальной страницы
   + В каких файлах размещать и как подключать модификаторы метаданных и обработчики событий data-объектов
   + Пример обработки события "при изменении номенклатуры или характеристики в строке табличной части заказа" - получает из регистра срез последних цены и подставляет полученную цену в редактируемую строку документа
- Пример [Счет и отгрузка для Бухгалтерии предприятия](examples/accounting), иллюстрирует аналогичное предыдущему подключение к типовой конфигурации БП 3.0. 

## Тесты
Первые [автоматические тесты](spec) добавлены к проекту в Августе 2015. Покрытие кода тестами пока составляет менее 1%, но начало положено.<br />Разработку нового функционала и работу над ошибками планируется вести _через тестирование_ 

## Благодарности
- Andrey Gershun, author of [AlaSQL](https://github.com/agershun/alasql) - Javascript SQL database library
- Авторам [PouchDB](http://pouchdb.com/) и [CouchDB](http://couchdb.apache.org/) - NoSQL database and data synchronization engine
- Авторам [dhtmlx](http://dhtmlx.com/) - a beautiful set of Ajax-powered UI components
- Прочим авторам за их замечательные инструменты, упрощающие нашу работу

## Лицензия
Библиотека metadata.js имеет две схемы лицензирования:
- Для некоммерческих Open Source проектов доступна лицензия [AGPL-3.0](http://licenseit.ru/wiki/index.php/GNU_Affero_General_Public_License_version_3)
- Коммерческая [лицензия на разработчика](http://www.oknosoft.ru/programmi-oknosoft/metadata.html) позволяет использовать и распространять ПО в любом количестве неконкурирующих продуктов, без ограничений на количество копий

Данная лицензия распространяется на все содержимое репозитория, но не заменеют существующие лицензии для продуктов, используемых библиотекой metadata.js

(c) 2014-2016, компания Окнософт (info@oknosoft.ru)