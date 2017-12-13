---
uid: web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-cs
title: "Разрешение только для некоторых символов в текстовом поле (C#) | Документы Microsoft"
author: wenz
description: "Проверяющие элементы управления ASP.NET гарантирует, что вводимые пользователем данные разрешены только определенные символы. Однако это по-прежнему не препятствует пользователям вводить недопустимые..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: fd2a1c52-d717-44af-8a61-67c8279bb26e
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-cs
msc.type: authoredcontent
ms.openlocfilehash: 246c3b5dd55ceb0f47ad1f4982ae5b3bf855e747
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2017
---
<a name="allowing-only-certain-characters-in-a-text-box-c"></a><span data-ttu-id="ddc3b-104">Разрешение только для некоторых символов в текстовом поле (C#)</span><span class="sxs-lookup"><span data-stu-id="ddc3b-104">Allowing Only Certain Characters in a Text Box (C#)</span></span>
====================
<span data-ttu-id="ddc3b-105">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ddc3b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ddc3b-106">[Загрузить код](http://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.cs.zip) или [скачать PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="ddc3b-106">[Download Code](http://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0CS.pdf)</span></span>

> <span data-ttu-id="ddc3b-107">Проверяющие элементы управления ASP.NET гарантирует, что вводимые пользователем данные разрешены только определенные символы.</span><span class="sxs-lookup"><span data-stu-id="ddc3b-107">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="ddc3b-108">Однако это по-прежнему не запрещает пользователям вводить недопустимые символы и при попытке отправить форму.</span><span class="sxs-lookup"><span data-stu-id="ddc3b-108">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>


## <a name="overview"></a><span data-ttu-id="ddc3b-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="ddc3b-109">Overview</span></span>

<span data-ttu-id="ddc3b-110">Проверяющие элементы управления ASP.NET гарантирует, что вводимые пользователем данные разрешены только определенные символы.</span><span class="sxs-lookup"><span data-stu-id="ddc3b-110">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="ddc3b-111">Однако это по-прежнему не запрещает пользователям вводить недопустимые символы и при попытке отправить форму.</span><span class="sxs-lookup"><span data-stu-id="ddc3b-111">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>

## <a name="steps"></a><span data-ttu-id="ddc3b-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="ddc3b-112">Steps</span></span>

<span data-ttu-id="ddc3b-113">Содержит набор элементов управления ASP.NET AJAX `FilteredTextBox` элемента управления, который расширяет текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="ddc3b-113">The ASP.NET AJAX Control Toolkit contains the `FilteredTextBox` control which extends a text box.</span></span> <span data-ttu-id="ddc3b-114">После активации только определенный набор символов можно ввести в поле.</span><span class="sxs-lookup"><span data-stu-id="ddc3b-114">Once activated, only a certain set of characters may be entered into the field.</span></span>

<span data-ttu-id="ddc3b-115">Чтобы это работало, необходимо сначала обычным образом ASP.NET AJAX `ScriptManager` открывается библиотеки JavaScript, которые также используются в наборе элементов управления ASP.NET AJAX:</span><span class="sxs-lookup"><span data-stu-id="ddc3b-115">For this to work, we first need as usual the ASP.NET AJAX `ScriptManager` which loads the JavaScript libraries which are also used by the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample1.aspx)]

<span data-ttu-id="ddc3b-116">Затем мы должны текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="ddc3b-116">Then, we need a text box:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample2.aspx)]

<span data-ttu-id="ddc3b-117">Наконец `FilteredTextBoxExtender` управления отвечает за ограничение символы разрешены для ввода пользователя.</span><span class="sxs-lookup"><span data-stu-id="ddc3b-117">Finally, the `FilteredTextBoxExtender` control takes care of restricting the characters the user is allowed to type.</span></span> <span data-ttu-id="ddc3b-118">Сначала следует задать `TargetControlID` атрибут `ID` из `TextBox` элемента управления.</span><span class="sxs-lookup"><span data-stu-id="ddc3b-118">First, set the `TargetControlID` attribute to the `ID` of the `TextBox` control.</span></span> <span data-ttu-id="ddc3b-119">Выберите один из доступных `FilterType` значений:</span><span class="sxs-lookup"><span data-stu-id="ddc3b-119">Then, choose one of the available `FilterType` values:</span></span>

- <span data-ttu-id="ddc3b-120">`Custom`по умолчанию; Вы должны предоставить список допустимых символов</span><span class="sxs-lookup"><span data-stu-id="ddc3b-120">`Custom` default; you have to provide a list of valid chars</span></span>
- <span data-ttu-id="ddc3b-121">`LowercaseLetters`только строчные буквы</span><span class="sxs-lookup"><span data-stu-id="ddc3b-121">`LowercaseLetters` lowercase letters only</span></span>
- <span data-ttu-id="ddc3b-122">`Numbers`только цифры</span><span class="sxs-lookup"><span data-stu-id="ddc3b-122">`Numbers` digits only</span></span>
- <span data-ttu-id="ddc3b-123">`UppercaseLetters`только прописные буквы</span><span class="sxs-lookup"><span data-stu-id="ddc3b-123">`UppercaseLetters` uppercase letters only</span></span>

<span data-ttu-id="ddc3b-124">Если `Custom FilterType` используется, `ValidChars` свойства должен быть задан и указать список символов, которые могут быть типизированы.</span><span class="sxs-lookup"><span data-stu-id="ddc3b-124">If the `Custom FilterType` is used, the `ValidChars` property must be set and provide a list of characters that may be typed.</span></span> <span data-ttu-id="ddc3b-125">Кстати: при попытке вставить текст в текстовом поле, будут удалены все недопустимые символы.</span><span class="sxs-lookup"><span data-stu-id="ddc3b-125">By the way: if you try to paste text into the text box, all invalid chars are removed.</span></span>

<span data-ttu-id="ddc3b-126">Разметка для `FilteredTextBoxExtender` управления, который разрешает только цифры (то, что также было бы возможно при `FilterType="Numbers"`):</span><span class="sxs-lookup"><span data-stu-id="ddc3b-126">Here is the markup for the `FilteredTextBoxExtender` control that only allows digits (something that would also have been possible with `FilterType="Numbers"`):</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample3.aspx)]

<span data-ttu-id="ddc3b-127">Запустить страницу и повторите вводить буквы, если включить JavaScript, работать не будет; Тем не менее знаков, отображаемых на странице.</span><span class="sxs-lookup"><span data-stu-id="ddc3b-127">Run the page and try to enter a letter if JavaScript is enabled, it will not work; digits however appear on the page.</span></span> <span data-ttu-id="ddc3b-128">Однако обратите внимание, что защита `FilteredTextBox` предоставляет не является подтверждением маркера: если JavaScript включен, все данные могут вводиться в текстовом поле, поэтому следует использовать средства дополнительную проверку, т. е. ASP. NET проверяющие элементы управления.</span><span class="sxs-lookup"><span data-stu-id="ddc3b-128">However note that the protection `FilteredTextBox` provides is not bullet-proof: If JavaScript is enabled, any data may be entered in the text box, so you have to use additional validation means, i.e. ASP.NET's validation controls.</span></span>


<span data-ttu-id="ddc3b-129">[![Можно вводить только цифры](allowing-only-certain-characters-in-a-text-box-cs/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ddc3b-129">[![Only digits may be entered](allowing-only-certain-characters-in-a-text-box-cs/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-cs/_static/image1.png)</span></span>

<span data-ttu-id="ddc3b-130">Можно вводить только цифры ([Просмотр полноразмерное изображение](allowing-only-certain-characters-in-a-text-box-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="ddc3b-130">Only digits may be entered ([Click to view full-size image](allowing-only-certain-characters-in-a-text-box-cs/_static/image3.png))</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="ddc3b-131">Вперед</span><span class="sxs-lookup"><span data-stu-id="ddc3b-131">Next</span></span>](allowing-only-certain-characters-in-a-text-box-vb.md)