---
title: "Обработка ошибок в ASP.NET Core"
author: ardalis
description: "Узнайте, как обрабатывать ошибки в приложениях ASP.NET Core."
manager: wpickett
ms.author: tdykstra
ms.custom: H1Hack27Feb2017
ms.date: 11/30/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/error-handling
ms.openlocfilehash: 5b0cda7b79b8a9523d1ba6a9b321d22d3ccc753a
ms.sourcegitcommit: 18d1dc86770f2e272d93c7e1cddfc095c5995d9e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/30/2018
---
# <a name="introduction-to-error-handling-in-aspnet-core"></a>Общие сведения об обработке ошибок в ASP.NET Core

Авторы: [Стив Смит](https://ardalis.com/) (Steve Smith) и [Том Дакстра](https://github.com/tdykstra/) (Tom Dykstra)

В этой статье рассматриваются основные методы обработки ошибок в приложениях ASP.NET Core.

[Просмотреть или скачать образец кода](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/error-handling/sample) ([как скачивать](xref:tutorials/index#how-to-download-a-sample))

## <a name="the-developer-exception-page"></a>Страница со сведениями об исключении для разработчика

Чтобы настроить вывод в приложении страницы с подробными сведениями об исключениях, установите пакет NuGet `Microsoft.AspNetCore.Diagnostics` и добавьте строку в [метод Configure в классе Startup](startup.md):

[!code-csharp[Main](error-handling/sample/Startup.cs?name=snippet_DevExceptionPage&highlight=7)]

Поместите метод `UseDeveloperExceptionPage` перед каждым промежуточным слоем, в котором нужно перехватывать исключения, например `app.UseMvc`.

>[!WARNING]
> Включать страницу со сведениями об исключении для разработчика следует **только тогда, когда приложение выполняется в среде разработки**. Подробные сведения об исключениях не должны быть общедоступными при выполнении приложения в рабочей среде. [Дополнительные сведения о настройке сред](environments.md).

Чтобы увидеть страницу со сведениями об исключении для разработчика, запустите образец приложения, указав среду `Development`, и добавьте элемент `?throw=true` к базовому URL-адресу приложения. Страница содержит несколько вкладок со сведениями об исключении и запросе. На первой вкладке приводится трассировка стека. 

![Трассировка стека](error-handling/_static/developer-exception-page.png)

На следующей вкладке представлены параметры строки запроса, если они имеются.

![Параметры строки запроса](error-handling/_static/developer-exception-page-query.png)

У этого запроса не было файлов cookie, но если бы они были, они бы отображались на вкладке **Cookies** (Файлы cookie). На последней вкладке можно просмотреть переданные заголовки.

![Заголовки](error-handling/_static/developer-exception-page-headers.png)

## <a name="configuring-a-custom-exception-handling-page"></a>Настройка пользовательской страницы обработки исключений

Если приложение выполняется не в среде `Development`, желательно настроить страницу обработки исключений.

[!code-csharp[Main](error-handling/sample/Startup.cs?name=snippet_DevExceptionPage&highlight=11)]

В приложении MVC не следует явным образом декорировать метод действия обработки ошибок атрибутами метода HTTP, например `HttpGet`. Из-за использования явных команд некоторые запросы могут не передаваться в метод.

```csharp
[Route("/Error")]
public IActionResult Index()
{
    // Handle error here
}
```

## <a name="configuring-status-code-pages"></a>Настройка страниц с кодами состояния

По умолчанию приложение не предоставляет специальных страниц для кодов состояния HTTP, таких как код 500 (внутренняя ошибка сервера) или 404 (не найдено). Вы можете настроить `StatusCodePagesMiddleware`, добавив строку в метод `Configure`:

```csharp
app.UseStatusCodePages();
```

По умолчанию этот промежуточный слой добавляет простые текстовые обработчики для распространенных кодов состояния, например 404:

![Страница 404](error-handling/_static/default-404-status-code.png)

Промежуточный слой поддерживает несколько разных методов расширения. Один из них принимает лямбда-выражение, а другой — тип содержимого и строку формата.

[!code-csharp[Main](error-handling/sample/Startup.cs?name=snippet_StatusCodePages)]

```csharp
app.UseStatusCodePages("text/plain", "Status code page, status code: {0}");
```

Имеются также методы расширения для перенаправления. Один из них отправляет клиенту код состояния 302, а другой возвращает исходный код состояния клиенту, а также выполняет обработчик для URL-адреса перенаправления.

[!code-csharp[Main](error-handling/sample/Startup.cs?name=snippet_StatusCodePagesWithRedirect)]

```csharp
app.UseStatusCodePagesWithReExecute("/error/{0}");
```

Если нужно отключить страницы с кодами состояния для некоторых запросов, это можно сделать так:

```csharp
var statusCodePagesFeature = context.Features.Get<IStatusCodePagesFeature>();
if (statusCodePagesFeature != null)
{
  statusCodePagesFeature.Enabled = false;
}
```

## <a name="exception-handling-code"></a>Код обработки исключений

Код на страницах обработки исключений может создавать исключения. Часто желательно, чтобы страницы ошибок в рабочей среде содержали только статическое содержимое.

Кроме того, имейте в виду, что после отправки заголовков для ответа нельзя изменить код состояния ответа, а также невозможно выполнение страниц или обработчиков исключений. Необходимо завершить ответ или прервать подключение.

## <a name="server-exception-handling"></a>Обработка исключений на сервере

Помимо логики обработки исключений в приложении, [сервер](servers/index.md), на котором размещается приложение, также выполняет ряд операций по обработке исключений. Если сервер перехватывает исключение перед отправкой заголовков, он отсылает ответ 500 "Внутренняя ошибка сервера" без текста. Если сервер перехватывает исключение после отправки заголовков, он закрывает соединение. Запросы, не обработанные приложением, обрабатываются сервером. Все возникшие исключения обрабатываются с помощью механизма обработки исключений на сервере. Настроенные пользовательские страницы ошибок, промежуточный слой обработки исключений и фильтры не влияют на этот процесс.

## <a name="startup-exception-handling"></a>Обработка исключений при запуске

Исключения, возникающие во время запуска приложения, могут обрабатываться только на уровне размещения. Вы можете [настроить реакцию узла на ошибки при запуске](hosting.md#detailed-errors) с помощью метода `captureStartupErrors` и ключа `detailedErrors`.

Узел может отображать страницу со сведениями о перехваченной ошибке при запуске, только если ошибка произошла после привязки адреса и порта узла. Если выполнить привязку по какой-либо причине не удается, уровень размещения записывает в журнал критическое исключение, происходит аварийное завершение процесса dotnet и страница со сведениями об ошибке не выводится.

## <a name="aspnet-mvc-error-handling"></a>Обработка ошибок ASP.NET MVC

В приложениях [MVC](xref:mvc/overview) есть дополнительные возможности обработки ошибок, например настройка фильтров исключений и проведение проверки модели.

### <a name="exception-filters"></a>Фильтры исключений

Фильтры исключений можно настраивать глобально либо для отдельных контроллеров, либо для действий в приложении MVC. Эти фильтры обрабатывают все необработанные исключения, которые возникают во время выполнения действия контроллера или другого фильтра. Иным образом они не вызываются. Дополнительные сведения о фильтрах исключений см. в статье [Фильтры](../mvc/controllers/filters.md).

>[!TIP]
> Фильтры исключений хорошо подходят для перехвата исключений, которые происходят в действиях MVC, однако они не так гибки, как ПО промежуточного слоя для обработки ошибок. ПО промежуточного слоя предпочтительнее для общих случаев. Фильтры следует использовать только тогда, когда обработка ошибок должна осуществляться *по-разному* в зависимости от выбранного действия MVC.

### <a name="handling-model-state-errors"></a>Обработка ошибок состояния модели

[Проверка модели](../mvc/models/validation.md) проводится перед вызовом каждого действия контроллера. Метод действия отвечает за проверку свойства `ModelState.IsValid` и соответствующую реакцию.

В некоторых приложениях соблюдается стандартное соглашение об обработке ошибок проверки модели. В этом случае подходящим местом для реализации такой политики может быть [фильтр](../mvc/controllers/filters.md). Следует проверить, как выполняются действия при недопустимых состояниях модели. Дополнительные сведения см. в статье [Тестирование логики контроллеров](../mvc/controllers/testing.md).



