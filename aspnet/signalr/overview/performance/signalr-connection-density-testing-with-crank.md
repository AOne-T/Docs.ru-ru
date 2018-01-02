---
uid: signalr/overview/performance/signalr-connection-density-testing-with-crank
title: "Тестирование с помощью ручки плотность подключения SignalR | Документы Microsoft"
author: tfitzmac
description: "Тестирование с помощью ручки плотность подключения SignalR"
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/22/2015
ms.topic: article
ms.assetid: 148d9ca7-1af1-44b6-a9fb-91e261b9b463
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/performance/signalr-connection-density-testing-with-crank
msc.type: authoredcontent
ms.openlocfilehash: a3e8fdb47bd80d819358f9c48cd82fd51d6c0400
ms.sourcegitcommit: fe880bf4ed1c8116071c0e47c0babf3623b7f44a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
<a name="signalr-connection-density-testing-with-crank"></a>Тестирование с помощью ручки плотность подключения SignalR
====================
по [Tom FitzMacken](https://github.com/tfitzmac)

> В этой статье описывается использование средства ручки для тестирования приложения с несколькими клиентами имитации.


Когда приложение выполняется в среде размещения (либо Azure веб-роли, службы IIS, или резидентной с помощью Owin), можно проверить ответ приложения на высокую плотность подключения с помощью средства ручки. Среда размещения могут быть сервер Internet Information Services (IIS), узел Owin или веб-роли Azure. (Примечание: счетчики производительности доступны не на веб-приложениях службы приложений Azure, поэтому вы не сможете получить данные о производительности из плотность проверку соединения.)

Плотность подключения ссылается на число одновременных подключений TCP, которые можно установить на сервере. Каждое соединение TCP требует собственный ресурсов и открыв большое число неактивных соединений в конечном итоге создать узкое место в памяти.

[SignalR codebase](https://github.com/signalr/signalr) включает нагрузочное тестирование инструмент, который называется **Crank**. Последнюю версию ручки можно найти в [ветви Dev](https://github.com/SignalR/signalr/tree/dev) на GitHub. Вы можете загрузить Zip архив, состоящий из ветви Dev SignalR codebase [здесь](https://github.com/SignalR/SignalR/archive/dev.zip).

Ручки может будет использоваться для полностью насытить памяти сервера для вычисления общее число неактивных соединений, которые можно использовать на оборудование сервера. Кроме того вы может также использовать ручки для нагрузочного теста сервера под определенный объем нехватки памяти, увеличивать соединения до достижения определенного числа или пороговое значение памяти.

При тестировании, очень важно использовать удаленных клиентов, чтобы избежать любой соперничество за ресурсы (т. е. TCP-подключений и памятью). Мониторинг клиентов, чтобы убедиться, что они не предназначаются узкие места препятствует завершению в полном объеме (памяти или ЦП) сервера. Может потребоваться увеличить число клиентов для полной загрузки сервера.

### <a name="running-a-connection-density-test"></a>Выполнение теста плотность подключения

В этом разделе описываются шаги, необходимые для выполнения теста плотность соединения в приложении SignalR.

1. Загрузить и построить [codebase ветви Dev SignalR](https://github.com/SignalR/SignalR/archive/dev.zip). В командной строке перейдите к &lt;каталог проекта&gt;\src\Microsoft.AspNet.SignalR.Crank\bin\debug.
2. Развертывание приложения в среду размещения предполагаемого. Запишите конечной точки, используемых приложением; Например, в приложение, созданное в [учебник по началу работы](../getting-started/tutorial-getting-started-with-signalr.md), конечная точка `http://<yourhost>:8080/signalr`.
3. Установка [счетчиков производительности SignalR](signalr-performance.md#perfcounters) на сервере. Если приложение выполняется в Azure, см. раздел [с помощью счетчиков производительности SignalR в веб-роли Azure](using-signalr-performance-counters-in-an-azure-web-role.md).

Если вы загрузили и построение базы кода и установлены счетчики производительности на узле, ручки средства командной строки можно найти в `src\Microsoft.AspNet.SignalR.Crank\bin\Debug` папки.

Доступные параметры для средства ручки:

- **/?** : Показан экран справки. Если также отображаются доступные параметры **URL-адрес** параметр указан.
- **Или URL-адрес**: URL-адрес для подключения SignalR. Этот параметр обязателен. Для SignalR приложения, с помощью сопоставления по умолчанию, путь будет завершен через «/ signalr».
- **/ Транспорта**: имя транспорта, используемого. Значение по умолчанию — `auto`, который выберет наиболее протокола. Параметры включают в себя `WebSockets`, `ServerSentEvents`, и `LongPolling` (`ForeverFrame` не подходит для ручки, так как клиент .NET, а не использовать Internet Explorer). Дополнительные сведения о том, как SignalR выбирает транспортов см. в разделе [транспортов и в случае ошибки](../getting-started/introduction-to-signalr.md#transports).
- **/ BatchSize**: число клиентов, которые добавлены в каждом пакете. Значение по умолчанию — 50.
- **/ ConnectInterval**: интервал в миллисекундах между добавлением соединения. Значение по умолчанию — 500.
- **И соединения,**: количество подключений, используемый для нагрузочного тестирования приложения. Значение по умолчанию — 100 000.
- **/ ConnectTimeout**: время ожидания в секундах до прерывания тестового. Значение по умолчанию — 300.
- **MinServerMBytes**: МБ для достижения минимальной серверной. Значение по умолчанию — 500.
- **SendBytes**: размер полезных данных, отправляемых на сервер, в байтах. Значение по умолчанию — 0.
- **SendInterval**: задержку в миллисекундах между сообщения на сервер. Значение по умолчанию — 500.
- **SendTimeout**: время ожидания в миллисекундах для сообщения на сервер. Значение по умолчанию — 300.
- **ControllerUrl**: URL-адрес, где один клиент будет размещаться концентратор контроллера. Значение по умолчанию — null (нет контроллеров). Контроллер концентратор запускается при запуске сеанса ручки; Дальнейшая становится контакта между концентратором контроллера и ручки.
- **NumClients**: число имитацию клиентам подключаться к приложению. Значение по умолчанию — один.
- **Файл журнала**: имя файла для файла журнала для тестового запуска. Значение по умолчанию — `crank.csv`.
- **SampleInterval**: время в миллисекундах между выборок счетчиков производительности. Значение по умолчанию — 1000.
- **SignalRInstance**: имя экземпляра счетчиков производительности на сервере. Значение по умолчанию — использовать состояние подключения клиента.

### <a name="example"></a>Пример

Следующая команда проверите узел с названием `pfsignalr` в Azure, на котором размещается приложение через порт 8080 с концентратором с именем «ControllerHub», с использованием 100 соединений.

`crank /Connections:100 /Url:http://pfsignalr.cloudapp.net:8080/signalr`