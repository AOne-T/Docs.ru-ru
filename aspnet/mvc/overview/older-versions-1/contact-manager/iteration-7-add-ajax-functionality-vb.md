---
uid: mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-vb
title: "Итерации #7 — функций Add Ajax (VB) | Документы Microsoft"
author: microsoft
description: "В седьмой итерации мы повысить скорость реагирования и производительности приложения, добавляя поддержку Ajax."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2009
ms.topic: article
ms.assetid: f640e063-150e-453d-8cfc-7e54a6ce0f1e
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-vb
msc.type: authoredcontent
ms.openlocfilehash: fa50fdea8ac165be3f8e96322ec049196a511ebe
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2017
---
<a name="iteration-7--add-ajax-functionality-vb"></a>Итерации #7 — функций Add Ajax (Visual Basic)
====================
по [Microsoft](https://github.com/microsoft)

[Загрузить исходный код](iteration-7-add-ajax-functionality-vb/_static/contactmanager_7_vb1.zip)

> В седьмой итерации мы повысить скорость реагирования и производительности приложения, добавляя поддержку Ajax.


## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>Создание приложения ASP.NET MVC управления контактами (Visual Basic)
  

В этой серии учебники мы создаем всего приложения управления контактами от начала и завершения. Приложение диспетчера контактов позволяет хранить контактные данные - имена, номера телефонов и адресов электронной почты — список людей.

Мы постройте приложение в нескольких итерациях. С каждой итерацией постепенно мы улучшить приложение. Это несколько итераций предназначена для того, чтобы позволяют понять причину для каждого изменения.

- Итерации #1 - создать приложение. В первой итерации мы создадим диспетчера контактов простейшим способом невозможно. Добавлена поддержка для основных операций базы данных: создание, чтение, обновление и удаление (CRUD).

- Итерации #2 — сделать приложение поиска работы с низким приоритетом. В этой итерации нам улучшить внешний вид приложения, изменив значение по умолчанию главной страницы представления ASP.NET MVC и каскадные таблицы стилей.

- Итерации #3 - Добавление проверки формы. В третьем проходе добавим проверки базовой формы. Мы запретить отправки формы, не завершая обязательные поля. Мы также для проверки адреса электронной почты и номера телефонов.

- Итерации #4 - сделать приложение слабо. В этой третьей итерации мы воспользоваться преимуществами нескольких шаблонов разработки программного обеспечения, чтобы упростить обслуживание и изменить приложение диспетчера контактов. Например мы выполнили рефакторинг наше приложение, чтобы использовать шаблон репозитория и шаблон внедрения зависимостей.

- Итерации #5 - Создание модульных тестов. В пятой итерации сделан нашего приложения проще в обслуживании и изменить, добавив модульных тестов. Мы макета наших классов модели данных и создания модульных тестов для наших контроллеров и логику проверки.

- Итерация &#6; — с помощью управляемой тестами разработки. В итерации этого шестой мы добавим новые функциональные возможности наше приложение, сначала написание модульных тестов и писать код для модульных тестов. В этой итерации добавим групп контактов.

- Итерации #7. Добавление функциональности Ajax. В седьмой итерации мы повысить скорость реагирования и производительности приложения, добавляя поддержку Ajax.

## <a name="this-iteration"></a>Этой итерации

В этой итерации приложение диспетчера контактов мы выполнили рефакторинг наше приложение использовать Ajax. Используя преимущества Ajax, мы ускорения нашего приложения. Можно избежать, подготовки к просмотру целой страницы, когда нам требуется обновление определенной области только на странице.

Мы будет рефакторинг нашей представление Index, чтобы мы не хотите t необходимость повторного отображения всей страницы всякий раз, когда кто-то выбирает группу новых контактов. Вместо этого при выборе пользователем группу контактов, мы просто обновить список контактов и оставьте только остальной части страницы.

Также мы изменим способ нашей удалить связь работает. Вместо отображения страницы отдельный подтверждения, мы отображать диалоговое окно подтверждения JavaScript. Если вы уверены, что вы хотите удалить контакт, операции HTTP DELETE выполняется на сервере, чтобы удалить запись из базы данных.

Кроме того мы будет использовать jQuery для добавления эффектов анимации в нашей представление индекса. Мы будем воспроизведения анимации, когда новый список контактов извлекается с сервера.

Наконец мы будем воспользоваться преимуществами ASP.NET AJAX framework поддержку управления журналом браузера. Мы создадим точек предыдущих состояний всякий раз, когда мы выполнить вызов Ajax для обновления списка контактов. В этом случае браузер прямой и обратной кнопок будет работать.

## <a name="why-use-ajax"></a>Зачем использовать Ajax?

С помощью Ajax имеет много преимуществ. Во-первых Добавление функциональности Ajax приложения позволяет улучшить взаимодействие с пользователем. В обычном веб-приложении всей страницы должны учитываться обратно на сервер каждый раз, пользователь выполняет действие. При каждом выполнении операции блокировки браузера и пользователю необходимо дождаться, пока вся страница извлечь и повторно.

Это может быть неприемлемо взаимодействие в случае классического приложения. Однако в большинстве случаев мы жили с этой неприятной ситуации, в случае веб-приложения, так как мы не знает, что бы мы могли сделать лучше. Мы решили, что ограничение веб-приложений при на самом деле он был ограничение наших imaginations.

В приложении Ajax вы не хотите t необходимо привести к остановке для обновления страницы взаимодействие с пользователем. Вместо этого можно выполнить асинхронный запрос в фоновом режиме, чтобы обновить страницу. Вы не хотите принудительно t пользователю, подождите, пока обновляется часть страницы.

Используя преимущества Ajax, можно повысить производительность приложения. Рассмотрим, как в данный момент работает приложение диспетчера контактов без обеспечения функциональности Ajax. Если щелкнуть группу контактов, необходимо повторно всего индекс представления. Список контактов и список групп контактов необходимо извлечь из базы данных сервера. Все эти данные должны передаваться по сети с веб-сервера веб-браузера.

После добавить функциональные возможности Ajax нашего приложения, тем не менее, можно избежать повторное отображение всей страницы, когда пользователь щелкает группу контактов. Мы больше не нужно захватить групп, контактов из базы данных. Мы также не хотите необходимость t для передачи всего индекса представления по каналу связи. Используя преимущества Ajax, мы сокращения объема работы, которую необходимо выполнять наши сервера базы данных и мы сократить объем сетевого трафика, необходимые для нашего приложения.

## <a name="don-t-be-afraid-of-ajax"></a>Пункт не быть боитесь Ajax

Некоторые разработчики не с помощью Ajax, так как они беспокоиться о браузерами нижнего уровня. Они хотели бы убедиться, что их веб-приложения по-прежнему будет работать при обращении к в браузере, не поддерживает JavaScript. Поскольку Ajax зависит от JavaScript, некоторые разработчики не с помощью Ajax.

Тем не менее если вы с осторожностью о том, как реализовать Ajax могут создавать приложения, работающие с верхнего и нижнего. Наше приложение диспетчера контактов будет работать с браузерами, которые поддерживают JavaScript и браузеры, которые этого не делают.

Если вы используете приложение диспетчера контактов с браузером, поддерживающим JavaScript необходимо будет улучшить взаимодействие с пользователем. Например при нажатии кнопки группу контактов, будет обновляться только область страницы, отображающей контакты.

Если, с другой стороны, используют приложение диспетчера контактов с помощью браузера, который не поддерживает JavaScript (или с JavaScript отключена) будет иметь более желательно взаимодействие с пользователем. Например при нажатии кнопки группу контактов, всего индекс представления должен обратной передаче браузера для отображения соответствующего списка контактов.

## <a name="adding-the-required-javascript-files"></a>Добавление файлов требуется JavaScript

Нам нужно будет использовать три файла JavaScript для добавления функций Ajax для нашего приложения. Все три эти файлы включены в папку «Скрипты» нового приложения ASP.NET MVC.

Если вы планируете использовать Ajax на нескольких страницах приложения затем смысл включить необходимые файлы JavaScript в главную страницу приложения s представления. Таким образом, файлы JavaScript будет автоматически включается в всех страниц в приложении.

Добавление следующего кода JavaScript включает внутри &lt;head&gt; тег на главной странице представления:

[!code-html[Main](iteration-7-add-ajax-functionality-vb/samples/sample1.html)]

## <a name="refactoring-the-index-view-to-use-ajax"></a>Рефакторинг индекс представления, чтобы использовать Ajax

Позволяет начать с изменения наших представление Index, чтобы только щелкнув группу контактов обновляет область представления, отображающий контакты s. Красный прямоугольник на рис. 1 содержит области, нам нужно обновить.


[![Обновление только контакты](iteration-7-add-ajax-functionality-vb/_static/image1.jpg)](iteration-7-add-ajax-functionality-vb/_static/image1.png)

**На рисунке 01**: обновление только контакты ([Просмотр полноразмерное изображение](iteration-7-add-ajax-functionality-vb/_static/image2.png))


Первым шагом является разделение части представления, что требуется обновление асинхронно в отдельных partial (пользовательский элемент управления view). Раздел индекса представление, которое отображает таблицу контактов была перемещена в разделяемом листинге 1.

**Листинг 1 - Views\Contact\ContactList.ascx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample2.aspx)]

Обратите внимание, что partial в листинге 1 другой модели, чем индекс представления. *Inherits* атрибута в &lt;% @ Page %&gt; директива указывает, что разделяемом наследует от ViewUserControl&lt;группы&gt; класса.

Обновленное представление индекса содержится в списке 2.

**Листинг 2 - Views\Contact\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample3.aspx)]

Есть две вещи, которые можно заметить о обновленное представление в списке 2. Во-первых Обратите внимание, что все содержимое перемещено в разделяемом заменяются вызов Html.RenderPartial(). Метод Html.RenderPartial() вызывается при первом запросе индекс представления для отображения начальный набор контакты.

Во-вторых Обратите внимание, что Html.ActionLink(), используемый для отображения групп контактов были заменены Ajax.ActionLink(). Ajax.ActionLink() вызывается со следующими параметрами:

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample4.aspx)]

Первый параметр представляет текст, отображаемый для ссылки, второй параметр представляет значения маршрута, а третий параметр представляет параметры Ajax. В этом случае мы используем UpdateTargetId Ajax параметр для указания HTML &lt;div&gt; тег, который необходимо обновить после завершения запроса Ajax. Необходимо обновить &lt;div&gt; тег с нового списка контактов.

В списке 3 содержится обновленный метод Index() контроллера, обратитесь в службу.

**Листинг 3 - Controllers\ContactController.vb (метод Index)**

[!code-vb[Main](iteration-7-add-ajax-functionality-vb/samples/sample5.vb)]

Обновленные Index() действия условно возвращает одно из следующих действий. Если действие Index() вызываемая Ajax-запросом контроллер возвращает частичной. В противном случае действие Index() возвращает всю область.

Обратите внимание, что действие Index() не нужно возвращать объема данных при вызове службой Ajax-запросом. В контексте обычным запросом действие индекса возвращает список всех групп, контактов и выбранную группу контактов. В контексте Ajax-запросом Index() действие возвращает только выбранной группы. AJAX означает меньше работы на сервере базы данных.

В случае верхнего и нижнего работает нашей измененного индекс представления. Если браузер поддерживает JavaScript щелкните группу контактов, обновляется только область представление, содержащее список контактов. Если, с другой стороны, ваш браузер не поддерживает JavaScript, все представление обновляется.


Наш обновленные представление индекса имеет одна проблема. Если щелкнуть группу контактов, выбранной группы гаснет. Поскольку список групп отображаются вне области, которая обновляется при выполнении запроса Ajax, подходящей группой не будут выявлены. Эта проблема будет устранена в следующем разделе.


## <a name="adding-jquery-animation-effects"></a>Добавление эффектов анимации jQuery

Как правило если щелкнуть ссылку на веб-странице, можно использовать индикатор браузера для обнаружения ли браузер активно извлекает обновленное содержимое. При выполнении Ajax-запросом, с другой стороны, индикатор браузера не содержит никаких действий. Это можно сделать нервозности пользователей. Как узнать, имеет ли замороженную браузер?

Существует несколько способов, которые можно указать для пользователя, работа выполняется при выполнении Ajax-запросом. Один из подходов заключается в том, чтобы отобразить простая анимация. Например можно Исчезание область при начале Ajax-запросом, затухание в регионе, после выполнения запроса.

Мы будем использовать библиотеку jQuery, в который входит в состав платформы Microsoft ASP.NET MVC, создание эффектов анимации. Обновленное представление индекса содержится в листинге 4.

**Листинг 4 - Views\Contact\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample6.aspx)]

Обратите внимание, что обновленный индекс представления содержит три новые функции JavaScript. Первые две функции использовать jQuery Исчезание и затухание в списке контактов, при нажатии кнопки группу новых контактов. Третья функция отображает сообщение об ошибке, когда результаты запроса Ajax в ошибку (например, время ожидания сети).

Первая функция также отвечает за выделение выбранной группы. Класс = выбранный атрибут добавляется к родительскому элементу (элемент LI) щелчке элемента. Опять же jQuery упрощает выбор правильного элемента и добавить класс CSS.

Эти сценарии, привязаны к связи группами с помощью параметра Ajax.ActionLink() AjaxOptions. Вызов метода обновленные Ajax.ActionLink() выглядит следующим образом:

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample7.aspx)]

## <a name="adding-browser-history-support"></a>Добавление поддержки журнал браузера

Как правило если щелкнуть ссылку, чтобы обновить страницу, журнал обозревателя обновляется. Таким образом, можно щелкнуть кнопку Назад в браузере и перемещает назад во времени к предыдущему состоянию страницы. Например если нажать в группу друзей и нажмите кнопку бизнес-групп, контактов, можно щелкнуть кнопку Назад в браузере и перейти к состоянию страницы, если был выбран в группу друзей.

К сожалению выполнение Ajax-запросом не обновляются журнал браузера. Если вы щелкните группу контактов и получить список совпадающих контактов с Ajax-запросом, журнал браузера не обновляется. Нельзя использовать «назад» браузера для обратного перехода к группе контактов после выбора новой группе контактов.

Дает пользователям возможность использовать обратно в браузере кнопку после выполнения запросов Ajax, необходимо выполнить немного больше работы. Необходимо воспользоваться преимуществами функций управления журнала браузера, встроенных в платформы ASP.NET AJAX.

Журнал браузера ASP.NET AJAX, необходимо выполнить три действия:

1. Включите журнал браузера, присвоив свойству enableBrowserHistory значение true.
2. При изменении состояния представления с помощью вызова метода addHistoryPoint(), сохраните точек предыдущих состояний.
3. Восстановить состояние представления, при возникновении события перехода.

Обновленное представление индекса содержится в листинге 5.

**Список 5 - Views\Contact\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample8.aspx)]

В листинге 5 в функции pageInit() включен журнал браузера. Функция pageInit() также используется для настройки обработчика событий для события перехода. События перехода возникает всякий раз, когда браузер вперед или кнопку "Назад" вызывает состояние страницы для изменения.

Метод beginContactList() вызывается при нажатии кнопки группу контактов. Этот метод создает точку предыдущего путем вызова метода addHistoryPoint(). Идентификатор группы контактов щелчке добавляется в журнал.

Идентификатор группы, извлекается из атрибута expando ссылку группы контактов. Такие ссылки выводятся при следующем вызове Ajax.ActionLink().

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample9.aspx)]

Последний параметр, передаваемый Ajax.ActionLink() добавляет атрибут expando с именем groupid к ссылке (в нижнем регистре для совместимости с XHTML).

Когда пользователь нажимает клавишу обратно в браузер или кнопка "вперед", возникает событие navigate и вызывается метод navigate(). Этот метод обновляет контактов, отображаемые на странице на соответствие состоянию страницы, которая соответствует точке журнала браузера, передаваемый в метод navigate.

## <a name="performing-ajax-deletes"></a>Удаляет выполнение Ajax

В настоящее время для удаления контакта, необходимо щелкнуть ссылку «Удалить» и нажмите кнопку «Удалить», отображаются на странице подтверждения удаления (см. рис. 2). Это выглядит как страница запросов делать что-то простое, например удаление записи базы данных.


[![Страница подтверждения удаления](iteration-7-add-ajax-functionality-vb/_static/image2.jpg)](iteration-7-add-ajax-functionality-vb/_static/image3.png)

**На рисунке 02**: страница подтверждения удаления ([Просмотр полноразмерное изображение](iteration-7-add-ajax-functionality-vb/_static/image4.png))


Это заманчивой пропустить страницу подтверждения удаления, и удаление контакта непосредственно в представлении индекса. Не следует использовать этот стремитесь, поскольку этот подход открывает приложению брешей в безопасности. В общем случае Дон t, потребуется выполнить операция HTTP GET, при вызове действие, которое изменяет состояние веб-приложения. При выполнении инструкции delete, необходимо выполнить запрос HTTP POST или лучше всего, операции HTTP DELETE.

Удалить связь содержится в список частичные контактов. Обновленный список частичные контактов содержится в 6 со списком.

**Перечисление 6 - Views\Contact\ContactList.ascx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample10.aspx)]

Удалить ссылки выводятся на следующий вызов метода Ajax.ImageActionLink():

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample11.aspx)]

> [!NOTE] 
> 
> Ajax.ImageActionLink() не является стандартной частью платформы ASP.NET MVC. Ajax.ImageActionLink() является пользовательских вспомогательных методов, включенных в проект диспетчера контактов.


Параметр AjaxOptions имеет два свойства. Во-первых подтверждение свойство используется для отображения диалогового окна подтверждения JavaScript контекстного меню. Во-вторых свойство HttpMethod используется для выполнения операции HTTP DELETE.

Листинг 7 содержит новое действие AjaxDelete(), будет добавлен контроллер контакта.

**Листинг 7 - Controllers\ContactController.vb (AjaxDelete)**   

[!code-vb[Main](iteration-7-add-ajax-functionality-vb/samples/sample12.vb)]

Действие AjaxDelete() помечено атрибутом AcceptVerbs. Этот атрибут не допускает действие вызов за исключением того, все операции HTTP, отличной от операции HTTP DELETE. В частности вы не можете вызывать это действие с помощью HTTP GET.

После удаления записи базы данных, которые нужно отобразить обновленный список контактов, не содержащий удаленной записи. Метод AjaxDelete() возвращает список частичные контактов и обновленный список контактов.

## <a name="summary"></a>Сводка

В этой итерации мы добавили функций Ajax в наше приложение диспетчера контактов. Мы использовали Ajax для повышения скорости реагирования и производительности приложения.

Во-первых мы оптимизировали представление Index, щелкнув группу контактов не обновляет все представление. Вместо этого щелкните группу контактов только обновляет список контактов.

Далее мы использовали эффекты анимации jQuery Исчезание и затухание в списке контактов. Добавление анимации в приложении Ajax можно использовать для предоставления пользователям приложения эквивалентом индикатор браузера.

Мы также добавили поддержки работы с журналом браузера в приложении Ajax. Мы включенных пользователей для щелкните браузер назад и вперед кнопки для изменения состояния представления индекса.

Наконец мы создали удалить ссылку, которая поддерживает операции HTTP DELETE. Путем удаления Ajax, мы позволяют пользователям удалять записи базы данных без пользователя для запроса дополнительных delete страница подтверждения.

>[!div class="step-by-step"]
[Назад](iteration-6-use-test-driven-development-vb.md)