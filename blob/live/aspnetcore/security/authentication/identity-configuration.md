---
title: "Настройка удостоверения ASP.NET Core"
author: AdrienTorris
description: "Значения по умолчанию ASP.NET Core Identity понять и настройки различных свойств Identity для использования пользовательских значений."
keywords: "Проверку подлинности ASP.NET Core, удостоверение,"
ms.author: scaddie
manager: wpickett
ms.date: 09/18/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authentication/identity-configuration
ms.openlocfilehash: 2861ca474e7e82da81943966394a92040ce96ab8
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2017
---
# <a name="configure-identity"></a><span data-ttu-id="a38d0-104">Настройка удостоверения</span><span class="sxs-lookup"><span data-stu-id="a38d0-104">Configure Identity</span></span>

<span data-ttu-id="a38d0-105">ASP.NET Core Identity имеет некоторые виды поведения по умолчанию, которые можно легко переопределить в вашем приложении `Startup` класса.</span><span class="sxs-lookup"><span data-stu-id="a38d0-105">ASP.NET Core Identity has some default behaviors that you can override easily in your application's `Startup` class.</span></span>

## <a name="passwords-policy"></a><span data-ttu-id="a38d0-106">Политики паролей</span><span class="sxs-lookup"><span data-stu-id="a38d0-106">Passwords policy</span></span>

<span data-ttu-id="a38d0-107">По умолчанию удостоверение требует, что пароли содержат символ верхнего регистра, строчные буквы, цифры и не алфавитно-цифровой символ.</span><span class="sxs-lookup"><span data-stu-id="a38d0-107">By default, Identity requires that passwords contain an uppercase character, lowercase character, a digit, and a non-alphanumeric character.</span></span> <span data-ttu-id="a38d0-108">Существуют также некоторые другие ограничения.</span><span class="sxs-lookup"><span data-stu-id="a38d0-108">There are also some other restrictions.</span></span> <span data-ttu-id="a38d0-109">Если вы хотите упростить ограничения для пароля, можно сделать это в `Startup` класса приложения.</span><span class="sxs-lookup"><span data-stu-id="a38d0-109">If you want to simplify password restrictions, you can do that in the `Startup` class of your application.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="a38d0-110">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="a38d0-110">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="a38d0-111">ASP.NET Core 2.0 добавлен `RequiredUniqueChars` свойство.</span><span class="sxs-lookup"><span data-stu-id="a38d0-111">ASP.NET Core 2.0 added the `RequiredUniqueChars` property.</span></span> <span data-ttu-id="a38d0-112">В противном случае параметры совпадают с ASP.NET Core 1.x.</span><span class="sxs-lookup"><span data-stu-id="a38d0-112">Otherwise, the options are the same from ASP.NET Core 1.x.</span></span>

[!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-37,50-52)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="a38d0-113">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="a38d0-113">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Startup.cs?range=58-65,84)]

---

<span data-ttu-id="a38d0-114">`IdentityOptions.Password`имеет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="a38d0-114">`IdentityOptions.Password` has the following properties:</span></span>
* <span data-ttu-id="a38d0-115">`RequireDigit`: Необходимо указать число от 0-9 и пароль.</span><span class="sxs-lookup"><span data-stu-id="a38d0-115">`RequireDigit`: Requires a number between 0-9 in the password.</span></span> <span data-ttu-id="a38d0-116">По умолчанию — true.</span><span class="sxs-lookup"><span data-stu-id="a38d0-116">Defaults to true.</span></span>
* <span data-ttu-id="a38d0-117">`RequiredLength`: Минимальная длина пароля.</span><span class="sxs-lookup"><span data-stu-id="a38d0-117">`RequiredLength`: The minimum length of the password.</span></span> <span data-ttu-id="a38d0-118">По умолчанию — 6.</span><span class="sxs-lookup"><span data-stu-id="a38d0-118">Defaults to 6.</span></span>
* <span data-ttu-id="a38d0-119">`RequireNonAlphanumeric`: Требуется не буквенно-цифровых символов в пароле.</span><span class="sxs-lookup"><span data-stu-id="a38d0-119">`RequireNonAlphanumeric`: Requires a non-alphanumeric character in the password.</span></span> <span data-ttu-id="a38d0-120">По умолчанию — true.</span><span class="sxs-lookup"><span data-stu-id="a38d0-120">Defaults to true.</span></span>
* <span data-ttu-id="a38d0-121">`RequireUppercase`: Требуется верхний регистр символов в пароле.</span><span class="sxs-lookup"><span data-stu-id="a38d0-121">`RequireUppercase`: Requires an upper case character in the password.</span></span> <span data-ttu-id="a38d0-122">По умолчанию — true.</span><span class="sxs-lookup"><span data-stu-id="a38d0-122">Defaults to true.</span></span>
* <span data-ttu-id="a38d0-123">`RequireLowercase`: Должен стоять символ нижнего регистра в пароле.</span><span class="sxs-lookup"><span data-stu-id="a38d0-123">`RequireLowercase`: Requires a lower case character in the password.</span></span> <span data-ttu-id="a38d0-124">По умолчанию — true.</span><span class="sxs-lookup"><span data-stu-id="a38d0-124">Defaults to true.</span></span>
* <span data-ttu-id="a38d0-125">`RequiredUniqueChars`: Требует количества уникальных символов в пароле.</span><span class="sxs-lookup"><span data-stu-id="a38d0-125">`RequiredUniqueChars`: Requires the number of distinct characters in the password.</span></span> <span data-ttu-id="a38d0-126">По умолчанию используется значение 1.</span><span class="sxs-lookup"><span data-stu-id="a38d0-126">Defaults to 1.</span></span>


## <a name="users-lockout"></a><span data-ttu-id="a38d0-127">Блокировки пользователя</span><span class="sxs-lookup"><span data-stu-id="a38d0-127">User's lockout</span></span>

[!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-30,39-42,50-52)]

<span data-ttu-id="a38d0-128">`IdentityOptions.Lockout`имеет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="a38d0-128">`IdentityOptions.Lockout` has the following properties:</span></span>
* <span data-ttu-id="a38d0-129">`DefaultLockoutTimeSpan`: Количество времени, пользователь будет заблокирован при возникновении блокировки.</span><span class="sxs-lookup"><span data-stu-id="a38d0-129">`DefaultLockoutTimeSpan`: The amount of time a user is locked out when a lockout occurs.</span></span> <span data-ttu-id="a38d0-130">Значение по умолчанию 5 минут.</span><span class="sxs-lookup"><span data-stu-id="a38d0-130">Defaults to 5 minutes.</span></span>
* <span data-ttu-id="a38d0-131">`MaxFailedAccessAttempts`: Число неудачных попыток доступа до пользователя будет заблокирована, если включена блокировка.</span><span class="sxs-lookup"><span data-stu-id="a38d0-131">`MaxFailedAccessAttempts`: The number of failed access attempts until a user is locked out, if lockout is enabled.</span></span> <span data-ttu-id="a38d0-132">По умолчанию — 5.</span><span class="sxs-lookup"><span data-stu-id="a38d0-132">Defaults to 5.</span></span>
* <span data-ttu-id="a38d0-133">`AllowedForNewUsers`: Определяет, если новый пользователь может быть заблокирован. По умолчанию — true.</span><span class="sxs-lookup"><span data-stu-id="a38d0-133">`AllowedForNewUsers`: Determines if a new user can be locked out. Defaults to true.</span></span>


## <a name="sign-in-settings"></a><span data-ttu-id="a38d0-134">Параметры входа</span><span class="sxs-lookup"><span data-stu-id="a38d0-134">Sign in settings</span></span>

[!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-30,44-46,50-52)]

<span data-ttu-id="a38d0-135">`IdentityOptions.SignIn`имеет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="a38d0-135">`IdentityOptions.SignIn` has the following properties:</span></span>
* <span data-ttu-id="a38d0-136">`RequireConfirmedEmail`: Требует подтверждения электронной почты для входа.</span><span class="sxs-lookup"><span data-stu-id="a38d0-136">`RequireConfirmedEmail`: Requires a confirmed email to sign in.</span></span> <span data-ttu-id="a38d0-137">По умолчанию используется значение false.</span><span class="sxs-lookup"><span data-stu-id="a38d0-137">Defaults to false.</span></span>
* <span data-ttu-id="a38d0-138">`RequireConfirmedPhoneNumber`: Требуется номер телефона, подтвержденной для входа.</span><span class="sxs-lookup"><span data-stu-id="a38d0-138">`RequireConfirmedPhoneNumber`: Requires a confirmed phone number to sign in.</span></span> <span data-ttu-id="a38d0-139">По умолчанию используется значение false.</span><span class="sxs-lookup"><span data-stu-id="a38d0-139">Defaults to false.</span></span>


## <a name="user-validation-settings"></a><span data-ttu-id="a38d0-140">Параметры проверки пользователя</span><span class="sxs-lookup"><span data-stu-id="a38d0-140">User validation settings</span></span>

[!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-30,48-52)]

<span data-ttu-id="a38d0-141">`IdentityOptions.User`имеет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="a38d0-141">`IdentityOptions.User` has the following properties:</span></span>
* <span data-ttu-id="a38d0-142">`RequireUniqueEmail`: Требуется каждому пользователю иметь уникальный адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="a38d0-142">`RequireUniqueEmail`: Requires each User to have a unique email.</span></span> <span data-ttu-id="a38d0-143">По умолчанию используется значение false.</span><span class="sxs-lookup"><span data-stu-id="a38d0-143">Defaults to false.</span></span>
* <span data-ttu-id="a38d0-144">`AllowedUserNameCharacters`: Допустимые символы в имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="a38d0-144">`AllowedUserNameCharacters`: Allowed characters in the username.</span></span> <span data-ttu-id="a38d0-145">Значение по умолчанию abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789-._@+.</span><span class="sxs-lookup"><span data-stu-id="a38d0-145">Defaults to abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789-._@+.</span></span>

## <a name="applications-cookie-settings"></a><span data-ttu-id="a38d0-146">Параметры файлов cookie приложения</span><span class="sxs-lookup"><span data-stu-id="a38d0-146">Application's cookie settings</span></span>

<span data-ttu-id="a38d0-147">Все параметры файла cookie приложения как политика паролей, можно изменить в `Startup` класса.</span><span class="sxs-lookup"><span data-stu-id="a38d0-147">Like the passwords policy, all the settings of the application's cookie can be changed in the `Startup` class.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="a38d0-148">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="a38d0-148">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="a38d0-149">В разделе `ConfigureServices` в `Startup` класса, можно настроить куки-файл приложения.</span><span class="sxs-lookup"><span data-stu-id="a38d0-149">Under `ConfigureServices` in the `Startup` class, you can configure the application's cookie.</span></span>

[!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?name=snippet_configurecookie)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="a38d0-150">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="a38d0-150">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Startup.cs?range=58-59,72-80,84)]

--- 

<span data-ttu-id="a38d0-151">`CookieAuthenticationOptions`имеет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="a38d0-151">`CookieAuthenticationOptions` has the following properties:</span></span>
* <span data-ttu-id="a38d0-152">`Cookie.Name`: Имя файла cookie.</span><span class="sxs-lookup"><span data-stu-id="a38d0-152">`Cookie.Name`: The name of the cookie.</span></span> <span data-ttu-id="a38d0-153">Значение по умолчанию. AspNetCore.Cookies.</span><span class="sxs-lookup"><span data-stu-id="a38d0-153">Defaults to .AspNetCore.Cookies.</span></span>
* <span data-ttu-id="a38d0-154">`Cookie.HttpOnly`: Если значение равно true, куки-файл недоступен из скриптов на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="a38d0-154">`Cookie.HttpOnly`: When true, the cookie is not accessible from client-side scripts.</span></span> <span data-ttu-id="a38d0-155">По умолчанию — true.</span><span class="sxs-lookup"><span data-stu-id="a38d0-155">Defaults to true.</span></span>
* <span data-ttu-id="a38d0-156">`ExpireTimeSpan`: Определяет, сколько времени хранится билет проверки подлинности в файл cookie будет оставаться действительным с момента его создания.</span><span class="sxs-lookup"><span data-stu-id="a38d0-156">`ExpireTimeSpan`: Controls how much time the authentication ticket stored in the cookie will remain valid from the point it is created.</span></span> <span data-ttu-id="a38d0-157">По умолчанию — 14 дней.</span><span class="sxs-lookup"><span data-stu-id="a38d0-157">Defaults to 14 days.</span></span>
* <span data-ttu-id="a38d0-158">`LoginPath`: Если пользователь не авторизован, они будут перенаправляться к этому пути с именем входа.</span><span class="sxs-lookup"><span data-stu-id="a38d0-158">`LoginPath`: When a user is unauthorized, they will be redirected to this path to login.</span></span> <span data-ttu-id="a38d0-159">Значение по умолчанию или учетной записи или имени входа.</span><span class="sxs-lookup"><span data-stu-id="a38d0-159">Defaults to /Account/Login.</span></span>
* <span data-ttu-id="a38d0-160">`LogoutPath`: При выходе пользователя он будет перенаправлен по этому пути.</span><span class="sxs-lookup"><span data-stu-id="a38d0-160">`LogoutPath`: When a user is logged out, they will be redirected to this path.</span></span> <span data-ttu-id="a38d0-161">Значение по умолчанию или учетной записи и выхода из системы.</span><span class="sxs-lookup"><span data-stu-id="a38d0-161">Defaults to /Account/Logout.</span></span>
* <span data-ttu-id="a38d0-162">`AccessDeniedPath`: Если пользователь не может выполнить проверку авторизации, они будут перенаправляться к этому пути.</span><span class="sxs-lookup"><span data-stu-id="a38d0-162">`AccessDeniedPath`: When a user fails an authorization check, they will be redirected to this path.</span></span> <span data-ttu-id="a38d0-163">Значение по умолчанию или учетной записи или доступ запрещен.</span><span class="sxs-lookup"><span data-stu-id="a38d0-163">Defaults to /Account/AccessDenied.</span></span>
* <span data-ttu-id="a38d0-164">`SlidingExpiration`: Если значение равно true, новый файл cookie будет выдан с новым окончанием срока действия текущего файла cookie при более половины срока.</span><span class="sxs-lookup"><span data-stu-id="a38d0-164">`SlidingExpiration`: When true, a new cookie will be issued with a new expiration time when the current cookie is more than halfway through the expiration window.</span></span> <span data-ttu-id="a38d0-165">По умолчанию — true.</span><span class="sxs-lookup"><span data-stu-id="a38d0-165">Defaults to true.</span></span>
* <span data-ttu-id="a38d0-166">`ReturnUrlParameter`: ReturnUrlParameter определяет имя параметра строки запроса, который добавляется по промежуточного слоя, когда код состояния 401 несанкционированный изменяется на перенаправление 302 пути входа.</span><span class="sxs-lookup"><span data-stu-id="a38d0-166">`ReturnUrlParameter`: The ReturnUrlParameter determines the name of the query string parameter which is appended by the middleware when a 401 Unauthorized status code is changed to a 302 redirect onto the login path.</span></span>
* <span data-ttu-id="a38d0-167">`AuthenticationScheme`: Это относится только к ASP.NET Core 1.x.</span><span class="sxs-lookup"><span data-stu-id="a38d0-167">`AuthenticationScheme`: This is only relevant for ASP.NET Core 1.x.</span></span> <span data-ttu-id="a38d0-168">Логическое имя для проверки подлинности конкретной схемы.</span><span class="sxs-lookup"><span data-stu-id="a38d0-168">The logical name for a particular authentication scheme.</span></span>
* <span data-ttu-id="a38d0-169">`AutomaticAuthenticate`: Этот флаг относится только к ASP.NET Core 1.x.</span><span class="sxs-lookup"><span data-stu-id="a38d0-169">`AutomaticAuthenticate`: This flag is only relevant for ASP.NET Core 1.x.</span></span> <span data-ttu-id="a38d0-170">Если значение равно true, файл cookie проверки подлинности запустите при каждом запросе и попытка проверки и воссоздания любому участнику сериализованный она создана.</span><span class="sxs-lookup"><span data-stu-id="a38d0-170">When true, cookie authentication should run on every request and attempt to validate and reconstruct any serialized principal it created.</span></span>
