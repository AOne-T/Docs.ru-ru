---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
title: "Часть 7: Членство и авторизации | Документы Microsoft"
author: jongalloway
description: "Этот учебник ряд подробно описываются шаги, необходимые для построения образца приложения ASP.NET MVC Music Store. Часть 7 охватывает членства и авторизации."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/13/2010
ms.topic: article
ms.assetid: c8511ebe-68bc-4240-87c3-d5ced84a3f37
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
msc.type: authoredcontent
ms.openlocfilehash: 064f2d6eca087fae8c796d1dde78d5079d3803ca
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2017
---
<a name="part-7-membership-and-authorization"></a><span data-ttu-id="62f49-104">Часть 7: Членство и авторизации</span><span class="sxs-lookup"><span data-stu-id="62f49-104">Part 7: Membership and Authorization</span></span>
====================
<span data-ttu-id="62f49-105">по [Джон Гэллоуэй](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="62f49-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="62f49-106">MVC Music Store является учебное приложение, которое вводятся и описываются пошаговые способы использования Visual Studio и ASP.NET MVC для веб-разработки.</span><span class="sxs-lookup"><span data-stu-id="62f49-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="62f49-107">MVC Music Store показана реализация хранилища упрощенных образец продает велосипеды через Интернет альбомы, которое реализует Администрирование сайта основные, вход пользователей и функциональные возможности корзины покупок.</span><span class="sxs-lookup"><span data-stu-id="62f49-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="62f49-108">Этот учебник ряд подробно описываются шаги, необходимые для построения образца приложения ASP.NET MVC Music Store.</span><span class="sxs-lookup"><span data-stu-id="62f49-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="62f49-109">Часть 7 охватывает членства и авторизации.</span><span class="sxs-lookup"><span data-stu-id="62f49-109">Part 7 covers Membership and Authorization.</span></span>


<span data-ttu-id="62f49-110">Наш контроллера директор магазина в настоящее время доступен всем посетите наш сайт.</span><span class="sxs-lookup"><span data-stu-id="62f49-110">Our Store Manager controller is currently accessible to anyone visiting our site.</span></span> <span data-ttu-id="62f49-111">Позволяет изменить этот параметр, чтобы ограничить разрешения для администраторов сайтов.</span><span class="sxs-lookup"><span data-stu-id="62f49-111">Let's change this to restrict permission to site administrators.</span></span>

## <a name="adding-the-accountcontroller-and-views"></a><span data-ttu-id="62f49-112">Добавление AccountController и представления</span><span class="sxs-lookup"><span data-stu-id="62f49-112">Adding the AccountController and Views</span></span>

<span data-ttu-id="62f49-113">Одним из различий между полный шаблон веб-приложения ASP.NET MVC 3 и ASP.NET MVC 3 пустое веб-приложение является что пустой шаблон не включает контроллера учетных записей.</span><span class="sxs-lookup"><span data-stu-id="62f49-113">One difference between the full ASP.NET MVC 3 Web Application template and the ASP.NET MVC 3 Empty Web Application template is that the empty template doesn't include an Account Controller.</span></span> <span data-ttu-id="62f49-114">Мы добавим контроллера учетных записей, скопировав несколько файлов из нового приложения ASP.NET MVC на основе полного шаблона веб-приложение ASP.NET MVC 3.</span><span class="sxs-lookup"><span data-stu-id="62f49-114">We'll add an Account Controller by copying a few files from a new ASP.NET MVC application created from the full ASP.NET MVC 3 Web Application template.</span></span>

<span data-ttu-id="62f49-115">Создание нового приложения ASP.NET MVC с помощью полного шаблона веб-приложение ASP.NET MVC 3 и скопируйте следующие файлы в тех же каталогах, в данном проекте:</span><span class="sxs-lookup"><span data-stu-id="62f49-115">Create a new ASP.NET MVC application using the full ASP.NET MVC 3 Web Application template and copy the following files into the same directories in our project:</span></span>

1. <span data-ttu-id="62f49-116">Скопируйте AccountController.cs в каталоге контроллеры</span><span class="sxs-lookup"><span data-stu-id="62f49-116">Copy AccountController.cs in the Controllers directory</span></span>
2. <span data-ttu-id="62f49-117">Скопируйте AccountModels в каталоге моделей</span><span class="sxs-lookup"><span data-stu-id="62f49-117">Copy AccountModels in the Models directory</span></span>
3. <span data-ttu-id="62f49-118">Создайте каталог учетную запись в каталоге представлений и скопируйте все четыре представления в</span><span class="sxs-lookup"><span data-stu-id="62f49-118">Create an Account directory inside the Views directory and copy all four views in</span></span>

<span data-ttu-id="62f49-119">Измените пространство имен для классов контроллеров и модели, чтобы они начинаются с MvcMusicStore.</span><span class="sxs-lookup"><span data-stu-id="62f49-119">Change the namespace for the Controller and Model classes so they begin with MvcMusicStore.</span></span> <span data-ttu-id="62f49-120">Класс AccountController должен использовать пространство имен MvcMusicStore.Controllers и AccountModels класса следует использовать пространство имен MvcMusicStore.Models.</span><span class="sxs-lookup"><span data-stu-id="62f49-120">The AccountController class should use the MvcMusicStore.Controllers namespace, and the AccountModels class should use the MvcMusicStore.Models namespace.</span></span>

<span data-ttu-id="62f49-121">*Примечание: Эти файлы также доступны в MvcMusicStore Assets.zip загрузки, из которого мы наш сайт разработки файлы скопированы в начале этого учебника. Членство файлы расположены в каталоге кода.*</span><span class="sxs-lookup"><span data-stu-id="62f49-121">*Note: These files are also available in the MvcMusicStore-Assets.zip download from which we copied our site design files at the beginning of the tutorial. The Membership files are located in the Code directory.*</span></span>

<span data-ttu-id="62f49-122">Обновленное решение должно выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="62f49-122">The updated solution should look like the following:</span></span>

![](mvc-music-store-part-7/_static/image1.png)

## <a name="adding-an-administrative-user-with-the-aspnet-configuration-site"></a><span data-ttu-id="62f49-123">Добавление администратора с веб-сайт конфигурации ASP.NET</span><span class="sxs-lookup"><span data-stu-id="62f49-123">Adding an Administrative User with the ASP.NET Configuration site</span></span>

<span data-ttu-id="62f49-124">Прежде чем мы требуем авторизации в сайте, нам нужно будет создать пользователя с доступом.</span><span class="sxs-lookup"><span data-stu-id="62f49-124">Before we require Authorization in our website, we'll need to create a user with access.</span></span> <span data-ttu-id="62f49-125">Самый простой способ создать пользователя является использование встроенных веб-конфигурации ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="62f49-125">The easiest way to create a user is to use the built-in ASP.NET Configuration website.</span></span>

<span data-ttu-id="62f49-126">Запустите веб-сайта ASP.NET конфигурации, щелкнув следующий значок в обозревателе решений.</span><span class="sxs-lookup"><span data-stu-id="62f49-126">Launch the ASP.NET Configuration website by clicking following the icon in the Solution Explorer.</span></span>

![](mvc-music-store-part-7/_static/image2.png)

<span data-ttu-id="62f49-127">Будет запущен веб-сайт конфигурации.</span><span class="sxs-lookup"><span data-stu-id="62f49-127">This launches a configuration website.</span></span> <span data-ttu-id="62f49-128">Перейдите на вкладку "Безопасность" на начальном экране, а затем щелкните ссылку «Включение ролей» в центре экрана.</span><span class="sxs-lookup"><span data-stu-id="62f49-128">Click on the Security tab on the home screen, then click the "Enable roles" link in the center of the screen.</span></span>

![](mvc-music-store-part-7/_static/image3.png)

<span data-ttu-id="62f49-129">Щелкните ссылку «Создание и управление роли».</span><span class="sxs-lookup"><span data-stu-id="62f49-129">Click the "Create or Manage roles" link.</span></span>

![](mvc-music-store-part-7/_static/image4.png)

<span data-ttu-id="62f49-130">Введите в качестве имени роли «Администратор» и нажмите кнопку Добавить роль.</span><span class="sxs-lookup"><span data-stu-id="62f49-130">Enter "Administrator" as the role name and press the Add Role button.</span></span>

![](mvc-music-store-part-7/_static/image5.png)

<span data-ttu-id="62f49-131">Нажмите кнопку "Назад", а затем щелкните ссылку Создать пользователя с левой стороны.</span><span class="sxs-lookup"><span data-stu-id="62f49-131">Click the Back button, then click on the Create user link on the left side.</span></span>

![](mvc-music-store-part-7/_static/image6.png)

<span data-ttu-id="62f49-132">Заполните поля сведений пользователя в левой части экрана, используя следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="62f49-132">Fill in the user information fields on the left using the following information:</span></span>

| <span data-ttu-id="62f49-133">**Поле**</span><span class="sxs-lookup"><span data-stu-id="62f49-133">**Field**</span></span> | <span data-ttu-id="62f49-134">**Значение**</span><span class="sxs-lookup"><span data-stu-id="62f49-134">**Value**</span></span> |
| --- | --- |
| <span data-ttu-id="62f49-135">**Имя пользователя**</span><span class="sxs-lookup"><span data-stu-id="62f49-135">**User Name**</span></span> | <span data-ttu-id="62f49-136">Администратор</span><span class="sxs-lookup"><span data-stu-id="62f49-136">Administrator</span></span> |
| <span data-ttu-id="62f49-137">**Пароль**</span><span class="sxs-lookup"><span data-stu-id="62f49-137">**Password**</span></span> | <span data-ttu-id="62f49-138">password123!</span><span class="sxs-lookup"><span data-stu-id="62f49-138">password123!</span></span> |
| <span data-ttu-id="62f49-139">**Подтверждение пароля**</span><span class="sxs-lookup"><span data-stu-id="62f49-139">**Confirm Password**</span></span> | <span data-ttu-id="62f49-140">password123!</span><span class="sxs-lookup"><span data-stu-id="62f49-140">password123!</span></span> |
| <span data-ttu-id="62f49-141">**Электронная почта**</span><span class="sxs-lookup"><span data-stu-id="62f49-141">**E-mail**</span></span> | <span data-ttu-id="62f49-142">(любой адрес электронной почты будут работать)</span><span class="sxs-lookup"><span data-stu-id="62f49-142">(any e-mail address will work)</span></span> |
| <span data-ttu-id="62f49-143">**Контрольный вопрос**</span><span class="sxs-lookup"><span data-stu-id="62f49-143">**Security Question**</span></span> | <span data-ttu-id="62f49-144">(любым)</span><span class="sxs-lookup"><span data-stu-id="62f49-144">(whatever you like)</span></span> |
| <span data-ttu-id="62f49-145">**Ответ на контрольный вопрос**</span><span class="sxs-lookup"><span data-stu-id="62f49-145">**Security Answer**</span></span> | <span data-ttu-id="62f49-146">(любым)</span><span class="sxs-lookup"><span data-stu-id="62f49-146">(whatever you like)</span></span> |

<span data-ttu-id="62f49-147">*Примечание: Вы безусловно можно использовать любой пароль, которые будут отправлены. Параметры безопасности по умолчанию пароль требуется пароль, который имеет 7 символов и содержит один не буквенно-цифровых символов.*</span><span class="sxs-lookup"><span data-stu-id="62f49-147">*Note: You can of course use any password you'd like. The default password security settings require a password that is 7 characters long and contains one non-alphanumeric character.*</span></span>

<span data-ttu-id="62f49-148">Выберите роль администратора для этого пользователя и нажмите кнопку Создать пользователя.</span><span class="sxs-lookup"><span data-stu-id="62f49-148">Select the Administrator role for this user, and click the Create User button.</span></span>

![](mvc-music-store-part-7/_static/image7.png)

<span data-ttu-id="62f49-149">На этом этапе вы увидите сообщение, указывающее, что пользователь успешно создан.</span><span class="sxs-lookup"><span data-stu-id="62f49-149">At this point, you should see a message indicating that the user was created successfully.</span></span>

![](mvc-music-store-part-7/_static/image8.png)

<span data-ttu-id="62f49-150">Теперь можно закрыть окно браузера.</span><span class="sxs-lookup"><span data-stu-id="62f49-150">You can now close the browser window.</span></span>

## <a name="role-based-authorization"></a><span data-ttu-id="62f49-151">Авторизация на основе ролей</span><span class="sxs-lookup"><span data-stu-id="62f49-151">Role-based Authorization</span></span>

<span data-ttu-id="62f49-152">Теперь можно ограничить доступ к StoreManagerController, с помощью атрибута [Authorize], указывающего, пользователь должен быть в роль администратора для доступа к любой действия контроллера в классе.</span><span class="sxs-lookup"><span data-stu-id="62f49-152">Now we can restrict access to the StoreManagerController using the [Authorize] attribute, specifying that the user must be in the Administrator role to access any controller action in the class.</span></span>

[!code-csharp[Main](mvc-music-store-part-7/samples/sample1.cs)]

<span data-ttu-id="62f49-153">*Примечание: Атрибут [Authorize] может быть помещен в методах определенное действие, а также на уровне класса контроллера.*</span><span class="sxs-lookup"><span data-stu-id="62f49-153">*Note: The [Authorize] attribute can be placed on specific action methods as well as at the Controller class level.*</span></span>

<span data-ttu-id="62f49-154">Теперь перехода /StoreManager появляется диалоговое окно Вход в систему:</span><span class="sxs-lookup"><span data-stu-id="62f49-154">Now browsing to /StoreManager brings up a Log On dialog:</span></span>

![](mvc-music-store-part-7/_static/image9.png)

<span data-ttu-id="62f49-155">После входа в систему с нашей новой учетной записи администратора, мы можем перейти к экрану альбом изменять как до.</span><span class="sxs-lookup"><span data-stu-id="62f49-155">After logging on with our new Administrator account, we're able to go to the Album Edit screen as before.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="62f49-156">[Назад](mvc-music-store-part-6.md)
[Вперед](mvc-music-store-part-8.md)</span><span class="sxs-lookup"><span data-stu-id="62f49-156">[Previous](mvc-music-store-part-6.md)
[Next](mvc-music-store-part-8.md)</span></span>