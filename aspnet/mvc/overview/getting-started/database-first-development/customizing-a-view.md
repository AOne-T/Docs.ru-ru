---
uid: mvc/overview/getting-started/database-first-development/customizing-a-view
title: "EF базы данных сначала с ASP.NET MVC: Настройка представления | Документы Microsoft"
author: tfitzmac
description: "С помощью MVC, Entity Framework и формирование шаблонов ASP.NET, можно создать веб-приложения, который предоставляет интерфейс для существующей базы данных. Этот учебник seri..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/01/2014
ms.topic: article
ms.assetid: 269380ff-d7e1-4035-8ad1-fe1316a25f76
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/database-first-development/customizing-a-view
msc.type: authoredcontent
ms.openlocfilehash: af9609396cff18b08824732731ddb9c5cca578fa
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2017
---
<a name="ef-database-first-with-aspnet-mvc-customizing-a-view"></a>EF базы данных сначала с ASP.NET MVC: Настройка представления
====================
по [Tom FitzMacken](https://github.com/tfitzmac)

> С помощью MVC, Entity Framework и формирование шаблонов ASP.NET, можно создать веб-приложения, который предоставляет интерфейс для существующей базы данных. Этот ряд учебника показано, как автоматически создают код, который дает пользователям возможность отображения, изменения, создания и удаления данных, которые хранятся в таблице базы данных. Созданный код соответствует столбцам в таблице базы данных.
> 
> Эта часть ряда фокусируется на изменение представлений автоматически создается, чтобы улучшить представление.


## <a name="add-enrolled-courses-to-student-details"></a>Добавьте сведения об учащихся зарегистрированных курсов

Сформированный код предусматривает хорошей отправной точкой для вашего приложения, но он не обязательно предоставляет все функциональные возможности, необходимые в приложении. Можно изменить код в соответствии с требованиями приложения. В настоящее время приложение не отображает зарегистрированных курсов для выбранного учащегося. В этом разделе вы добавите курсов, зарегистрированных для каждого студента для **сведения** представление для учащихся.

Откройте **Students/Details.cshtml**и ниже последней &lt;/dl&gt; вкладки, но перед закрывающим тегом &lt;/div&gt; , добавьте следующий код.

[!code-cshtml[Main](customizing-a-view/samples/sample1.cshtml)]

Этот код создает таблицу, отображающую строку для каждой записи в таблицу Enrollment для выбранного учащегося. **Отображения** метод отображает HTML для объекта (modelItem), который представляет выражение. Используйте метод отображения (а не просто внедрение значение свойства в коде) чтобы убедиться, что оно будет отформатировано неправильно на основе ее типа и шаблон для этого типа. В этом примере каждое выражение возвращает одно свойство из текущей записи в цикле и значения, простые типы, которые отображаются в виде текста.

Перейдите к представлению студентов или индекса еще раз и выберите **сведения** для одного из слушателей. Вы увидите, что Зарегистрированные курсы включены в представление.

![студента с регистрации](customizing-a-view/_static/image1.png)

>[!div class="step-by-step"]
[Назад](changing-the-database.md)
[Вперед](enhancing-data-validation.md)
