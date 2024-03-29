.. _`JS`: https://www.npmjs.com/package/oidc-client
.. _`.Net`: https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.OpenIdConnect
.. _`Java`: https://mvnrepository.com/artifact/org.springframework.security/spring-security-openid
.. _инструкции: https://integrations.kontur.ru/documentation

Подключение к Контур.ID
=========================

.. toctree::
   :maxdepth: 2
   :hidden:

   auth
   auth_and_authorize
   auth_app
   discovery
   user_errors
   using_refresh

* :ref:`Последовательность интеграции<rst-murkup-steps>`
* :ref:`Описание взаимодействия<rst-murkup-descr>`
* :ref:`Регистрация приложения<rst-murkup-registration>`
* :ref:`Реализация сценариев работы с OpenID Connect<rst-murkup-realization>`

Порядок работы с :ref:`OpenID Провайдером<rst-murkup-provider>` зависит от цели и задач, которые вы решаете. OpenID Connect основан на получении и использовании токенов аутентификации и авторизации. Токены — это цифро-буквенная строка символов, они бывают трех видов и различаются по назначению:

* :ref:`Id Token<rst-murkup-idtoken>` — для аутентификации,
* :ref:`Access Token<rst-murkup-acesstoken>` — для авторизации,
* :ref:`Refresh Token<rst-murkup-refreshtoken>` — для продления доступов.

И для аутентификации, и для авторизации пользователей ваше приложение будет взаимодействовать с OpenID Провайдером. 

.. _rst-murkup-steps:

.. rubric::  Последовательность интеграции

1. Для интеграции с OpenID Connect и получения токенов прежде всего нужно выбрать сценарий, который вы собираетесь реализовать. Описание см. в статье :doc:`Сценарии использования OpenID Connect</scenarios>`. 

2. Ознакомьтесь, как :ref:`приложение будет взаимодействовать с OpenID Connect<rst-murkup-descr>`.

3. :ref:`Зарегистрируйте приложение<rst-murkup-registration>`.

4. :ref:`Реализуйте сценарий интеграции<rst-murkup-realization>`.

.. _rst-murkup-descr:

.. rubric::  Описание взаимодействия

В общем случае работа с OpenID Connect будет выглядеть следующим образом:

1. Приложение перенаправляет пользователя в браузере на OpenID Провайдер. При перенаправлении нужно будет указать ваш client_id и какие права вам нужны.
2. Пользователь входит в учетную запись Контура и предоставляет вашему приложению права на доступ к данным.
3. OpenID Провайдер перенаправляет пользователя на клиентский адрес — URL адрес, который нужно указать при регистрации приложения. Также OpenID Провайдер возвращает код подтверждения для приложения.
4. Приложение запрашивает токены в обмен на код подтверждения, и передает свои учетные данные client_id и client_secret.
5. OpenID Провайдер возвращает приложению токены.

.. _rst-murkup-registration:

.. rubric:: Регистрация приложения 

Ваше приложение нужно зарегистрировать, прежде чем пользователи смогут входить в него с помощью OpenID Connect.

1. Обратитесь к менеджеру продукта, который вы собираетесь подключить. Менеджер создаст конфигурацию вашего приложения и выдаст вам доступ для настройки приложения.

2. Настройте ваше приложение по инструкции_.

В процессе регистрации для приложения будут назначены его индивидуальные учетные данные, которые нужны для обращения к OpenId Провайдеру:

* ``client_id`` — идентификатор, который определяет ваше приложение;
* ``client_secret`` — секретный ключ приложения;
* Список прав доступа (:ref:`scope<rst-murkup-scope>`), которые можно запрашивать у OpenID провайдера при получении токенов.

.. _rst-murkup-realization:

.. rubric:: Реализация сценариев работы с OpenID Connect

После регистрации приложение взаимодействует с OpenID Провайдером, отправляя к нему запросы. Адреса конечных точек, открытый ключ OpenID Провайдера можно посмотреть при :doc:`получении документа метаданных OpenID Connect</schemes/discovery>`. 

Адреса OpenID Провайдера для отправки запросов:

* Рабочая площадка: http://identity.kontur.ru/
* Тестовая площадка: http://identity.testkontur.ru/

Для многих языков разработки в открытом доступе есть уже готовые библиотеки или реализации интеграции с OpenID Connect:

* `JS`_
* `.Net`_
* `Java`_

Выделим основные направления в работе с OpenID Connect:

* :doc:`/schemes/auth`
* :doc:`/schemes/auth_and_authorize`

В этих статьях вы найдете подробный алгоритм работы с OpenID Провайдером, примеры обращений к конечным точкам и описание возвращаемых данных. 