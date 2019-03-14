---
title: Identity vygenerované uživatelské rozhraní v projektech ASP.NET Core
author: rick-anderson
description: Zjistěte, jak automaticky vygenerovat identitu v projektu aplikace ASP.NET Core.
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.custom: mvc
ms.date: 10/24/2018
uid: security/authentication/scaffold-identity
ms.openlocfilehash: d86d3cab91e8f927db30767097a89a08cf358f06
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57076489"
---
# <a name="scaffold-identity-in-aspnet-core-projects"></a><span data-ttu-id="69d16-103">Identity vygenerované uživatelské rozhraní v projektech ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="69d16-103">Scaffold Identity in ASP.NET Core projects</span></span>

<span data-ttu-id="69d16-104">Podle [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="69d16-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="69d16-105">ASP.NET Core 2.1 nebo novější obsahuje [ASP.NET Core Identity](xref:security/authentication/identity) jako [knihovny tříd Razor](xref:razor-pages/ui-class).</span><span class="sxs-lookup"><span data-stu-id="69d16-105">ASP.NET Core 2.1 and later provides [ASP.NET Core Identity](xref:security/authentication/identity) as a [Razor Class Library](xref:razor-pages/ui-class).</span></span> <span data-ttu-id="69d16-106">Aplikace, které obsahují Identity můžete použít Generátor selektivně Přidání zdrojového kódu obsažen v knihovně Razor třídu (RCL) Identity.</span><span class="sxs-lookup"><span data-stu-id="69d16-106">Applications that include Identity can apply the scaffolder to selectively add the source code contained in the Identity Razor Class Library (RCL).</span></span> <span data-ttu-id="69d16-107">Můžete chtít vygenerování zdrojového kódu, abyste mohli upravit kód a změnit chování.</span><span class="sxs-lookup"><span data-stu-id="69d16-107">You might want to generate source code so you can modify the code and change the behavior.</span></span> <span data-ttu-id="69d16-108">Například může dát pokyn generátor pro generování kódu při registraci.</span><span class="sxs-lookup"><span data-stu-id="69d16-108">For example, you could instruct the scaffolder to generate the code used in registration.</span></span> <span data-ttu-id="69d16-109">Generovaného kódu mají přednost před stejný kód v Identity RCL.</span><span class="sxs-lookup"><span data-stu-id="69d16-109">Generated code takes precedence over the same code in the Identity RCL.</span></span> <span data-ttu-id="69d16-110">Získejte úplnou kontrolu nad uživatelského rozhraní a nepoužívat výchozí RCL, najdete v části [vytvořit úplnou identity uživatelského rozhraní zdroj](#full).</span><span class="sxs-lookup"><span data-stu-id="69d16-110">To gain full control of the UI and not use the default RCL, see the section [Create full identity UI source](#full).</span></span>

<span data-ttu-id="69d16-111">Aplikace, které provádějí **není** zahrnout ověřování můžete použít generátor a přidejte příslušný balíček RCL Identity.</span><span class="sxs-lookup"><span data-stu-id="69d16-111">Applications that do **not** include authentication can apply the scaffolder to add the RCL Identity package.</span></span> <span data-ttu-id="69d16-112">Máte možnost výběru Identity kód chcete vygenerovat.</span><span class="sxs-lookup"><span data-stu-id="69d16-112">You have the option of selecting Identity code to be generated.</span></span>

<span data-ttu-id="69d16-113">I když generátor generuje většinu kódu nezbytné, budete muset aktualizovat projekt proces dokončete.</span><span class="sxs-lookup"><span data-stu-id="69d16-113">Although the scaffolder generates most of the necessary code, you'll have to update your project to complete the process.</span></span> <span data-ttu-id="69d16-114">Tento dokument popisuje kroky potřebné k dokončení generování uživatelského rozhraní aktualizace Identity.</span><span class="sxs-lookup"><span data-stu-id="69d16-114">This document explains the steps needed to complete an Identity scaffolding update.</span></span>

<span data-ttu-id="69d16-115">Při spuštění generátor Identity *ScaffoldingReadme.txt* vytvoří soubor v adresáři projektu.</span><span class="sxs-lookup"><span data-stu-id="69d16-115">When the Identity scaffolder is run, a *ScaffoldingReadme.txt* file is created in the project directory.</span></span> <span data-ttu-id="69d16-116">*ScaffoldingReadme.txt* soubor obsahuje obecné pokyny, co je potřeba k dokončení generování uživatelského rozhraní aktualizace Identity.</span><span class="sxs-lookup"><span data-stu-id="69d16-116">The *ScaffoldingReadme.txt* file contains general instructions on what's needed to complete the Identity scaffolding update.</span></span> <span data-ttu-id="69d16-117">Tento dokument obsahuje podrobnější pokyny než *ScaffoldingReadme.txt* souboru.</span><span class="sxs-lookup"><span data-stu-id="69d16-117">This document contains more complete instructions than the *ScaffoldingReadme.txt* file.</span></span>

<span data-ttu-id="69d16-118">Doporučujeme používat systém správy zdrojového kódu, které jsou uvedeny rozdíly souborů a umožňuje zpět mimo změny.</span><span class="sxs-lookup"><span data-stu-id="69d16-118">We recommend using a source control system that shows file differences and allows you to back out of changes.</span></span> <span data-ttu-id="69d16-119">Zkontrolujte změny po spuštění generátor Identity.</span><span class="sxs-lookup"><span data-stu-id="69d16-119">Inspect the changes after running the Identity scaffolder.</span></span>

> [!NOTE]
> <span data-ttu-id="69d16-120">Při použití se vyžadují služby [dvoufaktorové ověřování](xref:security/authentication/identity-enable-qrcodes), [účtu potvrzení a heslo pro obnovení](xref:security/authentication/accconfirm)a další funkce zabezpečení s identitou.</span><span class="sxs-lookup"><span data-stu-id="69d16-120">Services are required when using [Two Factor Authentication](xref:security/authentication/identity-enable-qrcodes), [Account confirmation and password recovery](xref:security/authentication/accconfirm), and other security features with Identity.</span></span> <span data-ttu-id="69d16-121">Služby nebo zástupné procedury služby nejsou generovány při generování uživatelského rozhraní Identity.</span><span class="sxs-lookup"><span data-stu-id="69d16-121">Services or service stubs aren't generated when scaffolding Identity.</span></span> <span data-ttu-id="69d16-122">Služby a povolení těchto funkcí je nutné přidat ručně.</span><span class="sxs-lookup"><span data-stu-id="69d16-122">Services to enable these features must be added manually.</span></span> <span data-ttu-id="69d16-123">Viz například [vyžadují e-mailové potvrzení](xref:security/authentication/accconfirm#require-email-confirmation).</span><span class="sxs-lookup"><span data-stu-id="69d16-123">For example, see [Require Email Confirmation](xref:security/authentication/accconfirm#require-email-confirmation).</span></span>

## <a name="scaffold-identity-into-an-empty-project"></a><span data-ttu-id="69d16-124">Vygenerované uživatelské rozhraní identity do prázdného projektu</span><span class="sxs-lookup"><span data-stu-id="69d16-124">Scaffold identity into an empty project</span></span>

[!INCLUDE[](~/includes/scaffold-identity/id-scaffold-dlg.md)]

<span data-ttu-id="69d16-125">Přidejte následující zvýrazněný volání `Startup` třídy:</span><span class="sxs-lookup"><span data-stu-id="69d16-125">Add the following highlighted calls to the `Startup` class:</span></span>

[!code-csharp[](scaffold-identity/sample/StartupEmpty.cs?name=snippet1&highlight=5,20-23)]

[!INCLUDE[](~/includes/scaffold-identity/hsts.md)]

[!INCLUDE[](~/includes/scaffold-identity/migrations.md)]

## <a name="scaffold-identity-into-a-razor-project-without-existing-authorization"></a><span data-ttu-id="69d16-126">Vygenerované uživatelské rozhraní identity do projektu Razor bez existující autorizace</span><span class="sxs-lookup"><span data-stu-id="69d16-126">Scaffold identity into a Razor project without existing authorization</span></span>

<!--
set projNam=RPnoAuth
set projType=razor
set version=2.1.0

dotnet new %projType% -o %projNam%
cd %projNam%
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design -v %version%
dotnet restore
dotnet aspnet-codegenerator identity --useDefaultUI
dotnet ef migrations add CreateIdentitySchema
dotnet ef database update
-->

[!INCLUDE[](~/includes/scaffold-identity/id-scaffold-dlg.md)]

<span data-ttu-id="69d16-127">Identita je nakonfigurovaný v *Areas/Identity/IdentityHostingStartup.cs*.</span><span class="sxs-lookup"><span data-stu-id="69d16-127">Identity is configured in *Areas/Identity/IdentityHostingStartup.cs*.</span></span> <span data-ttu-id="69d16-128">Další informace najdete v tématu [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration).</span><span class="sxs-lookup"><span data-stu-id="69d16-128">for more information, see [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration).</span></span>

<a name="efm"></a>

### <a name="migrations-useauthentication-and-layout"></a><span data-ttu-id="69d16-129">Migrace, UseAuthentication a rozložení</span><span class="sxs-lookup"><span data-stu-id="69d16-129">Migrations, UseAuthentication, and layout</span></span>

[!INCLUDE[](~/includes/scaffold-identity/migrations.md)]

<a name="useauthentication"></a>

### <a name="enable-authentication"></a><span data-ttu-id="69d16-130">Povolení ověřování</span><span class="sxs-lookup"><span data-stu-id="69d16-130">Enable authentication</span></span>

<span data-ttu-id="69d16-131">V `Configure` metodu `Startup` třídy, zavolejte [UseAuthentication](/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_AuthAppBuilderExtensions_UseAuthentication_Microsoft_AspNetCore_Builder_IApplicationBuilder_) po `UseStaticFiles`:</span><span class="sxs-lookup"><span data-stu-id="69d16-131">In the `Configure` method of the `Startup` class, call [UseAuthentication](/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_AuthAppBuilderExtensions_UseAuthentication_Microsoft_AspNetCore_Builder_IApplicationBuilder_) after `UseStaticFiles`:</span></span>

[!code-csharp[](scaffold-identity/sample/StartupRPnoAuth.cs?name=snippet1&highlight=29)]

[!INCLUDE[](~/includes/scaffold-identity/hsts.md)]

### <a name="layout-changes"></a><span data-ttu-id="69d16-132">Změny rozložení</span><span class="sxs-lookup"><span data-stu-id="69d16-132">Layout changes</span></span>

<span data-ttu-id="69d16-133">Volitelné: Přidat částečné přihlášení (`_LoginPartial`) pro soubor rozložení:</span><span class="sxs-lookup"><span data-stu-id="69d16-133">Optional: Add the login partial (`_LoginPartial`) to the layout file:</span></span>

[!code-html[Main](scaffold-identity/sample/_Layout.cshtml?highlight=37)]

## <a name="scaffold-identity-into-a-razor-project-with-authorization"></a><span data-ttu-id="69d16-134">Vygenerované uživatelské rozhraní identity do projektu Razor s autorizací</span><span class="sxs-lookup"><span data-stu-id="69d16-134">Scaffold identity into a Razor project with authorization</span></span>

<!--
Use >=2.1: dotnet new webapp -au Individual -o RPauth
Use = 2.0: dotnet new razor -au Individual -o RPauth
uld option: Use Local DB, not SQLite

dotnet new webapp -au Individual -uld -o RPauth
cd RPauth
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet restore
dotnet aspnet-codegenerator identity -dc RPauth.Data.ApplicationDbContext --files Account.Register
-->

[!INCLUDE[](~/includes/scaffold-identity/id-scaffold-dlg-auth.md)]
<span data-ttu-id="69d16-135">Některé možnosti Identity jsou nakonfigurované v *Areas/Identity/IdentityHostingStartup.cs*.</span><span class="sxs-lookup"><span data-stu-id="69d16-135">Some Identity options are configured in *Areas/Identity/IdentityHostingStartup.cs*.</span></span> <span data-ttu-id="69d16-136">Další informace najdete v tématu [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration).</span><span class="sxs-lookup"><span data-stu-id="69d16-136">For more information, see [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration).</span></span>

## <a name="scaffold-identity-into-an-mvc-project-without-existing-authorization"></a><span data-ttu-id="69d16-137">Vygenerované uživatelské rozhraní identity do projektu aplikace MVC bez existující autorizace</span><span class="sxs-lookup"><span data-stu-id="69d16-137">Scaffold identity into an MVC project without existing authorization</span></span>

<!--
set projNam=MvcNoAuth
set projType=mvc
set version=2.1.0

dotnet new %projType% -o %projNam%
cd %projNam%
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design -v %version%
dotnet restore
dotnet aspnet-codegenerator identity --useDefaultUI
dotnet ef migrations add CreateIdentitySchema
dotnet ef database update
-->

[!INCLUDE[](~/includes/scaffold-identity/id-scaffold-dlg.md)]

<span data-ttu-id="69d16-138">Volitelné: Přidat částečné přihlášení (`_LoginPartial`) k *Views/Shared/_Layout.cshtml* souboru:</span><span class="sxs-lookup"><span data-stu-id="69d16-138">Optional: Add the login partial (`_LoginPartial`) to the *Views/Shared/_Layout.cshtml* file:</span></span>

[!code-html[](scaffold-identity/sample/_LayoutMvc.cshtml?highlight=37)]

* <span data-ttu-id="69d16-139">Přesunout *Pages/Shared/_LoginPartial.cshtml* do souboru *Views/Shared/_LoginPartial.cshtml*</span><span class="sxs-lookup"><span data-stu-id="69d16-139">Move the *Pages/Shared/_LoginPartial.cshtml* file to *Views/Shared/_LoginPartial.cshtml*</span></span>

<span data-ttu-id="69d16-140">Identita je nakonfigurovaný v *Areas/Identity/IdentityHostingStartup.cs*.</span><span class="sxs-lookup"><span data-stu-id="69d16-140">Identity is configured in *Areas/Identity/IdentityHostingStartup.cs*.</span></span> <span data-ttu-id="69d16-141">Další informace najdete v tématu IHostingStartup.</span><span class="sxs-lookup"><span data-stu-id="69d16-141">For more information, see IHostingStartup.</span></span>

[!INCLUDE[](~/includes/scaffold-identity/migrations.md)]

<span data-ttu-id="69d16-142">Volání [UseAuthentication](/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_AuthAppBuilderExtensions_UseAuthentication_Microsoft_AspNetCore_Builder_IApplicationBuilder_) po `UseStaticFiles`:</span><span class="sxs-lookup"><span data-stu-id="69d16-142">Call [UseAuthentication](/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_AuthAppBuilderExtensions_UseAuthentication_Microsoft_AspNetCore_Builder_IApplicationBuilder_) after `UseStaticFiles`:</span></span>

[!code-csharp[](scaffold-identity/sample/StartupMvcNoAuth.cs?name=snippet1&highlight=23)]

[!INCLUDE[](~/includes/scaffold-identity/hsts.md)]

## <a name="scaffold-identity-into-an-mvc-project-with-authorization"></a><span data-ttu-id="69d16-143">Vygenerované uživatelské rozhraní identity do projektu aplikace MVC s autorizací</span><span class="sxs-lookup"><span data-stu-id="69d16-143">Scaffold identity into an MVC project with authorization</span></span>

<!--
dotnet new mvc -au Individual -o MvcAuth
cd MvcAuth
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet restore
dotnet aspnet-codegenerator identity -dc MvcAuth.Data.ApplicationDbContext --files Account.Register
-->

[!INCLUDE[](~/includes/scaffold-identity/id-scaffold-dlg-auth.md)]

<span data-ttu-id="69d16-144">Odstranit *stránek/Shared* složky a soubory v této složce.</span><span class="sxs-lookup"><span data-stu-id="69d16-144">Delete the *Pages/Shared* folder and the files in that folder.</span></span>

<a name="full"></a>

## <a name="create-full-identity-ui-source"></a><span data-ttu-id="69d16-145">Vytvoření zdroje plnou identitou uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="69d16-145">Create full identity UI source</span></span>

<span data-ttu-id="69d16-146">Pokud chcete zachovat plnou kontrolu nad Identity uživatelského rozhraní, spusťte generátor Identity a vyberte **přepsat všechny soubory**.</span><span class="sxs-lookup"><span data-stu-id="69d16-146">To maintain full control of the Identity UI, run the Identity scaffolder and select **Override all files**.</span></span>

<span data-ttu-id="69d16-147">Následující zvýrazněný kód ukazuje změny nahraďte výchozí uživatelské rozhraní Identity Identity ve webové aplikaci ASP.NET Core 2.1.</span><span class="sxs-lookup"><span data-stu-id="69d16-147">The following highlighted code shows the changes to replace the default Identity UI with Identity in an ASP.NET Core 2.1 web app.</span></span> <span data-ttu-id="69d16-148">Můžete k tomu mají plnou kontrolu nad Identity uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="69d16-148">You might want to do this to have full control of the Identity UI.</span></span>

[!code-csharp[](scaffold-identity/sample/StartupFull.cs?name=snippet1&highlight=13-14,17-999)]

<span data-ttu-id="69d16-149">V následujícím kódu se nahradí výchozí Identity:</span><span class="sxs-lookup"><span data-stu-id="69d16-149">The default Identity is replaced in the following code:</span></span>

[!code-csharp[](scaffold-identity/sample/StartupFull.cs?name=snippet2)]

<span data-ttu-id="69d16-150">Následující kód nastaví [LoginPath](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.loginpath), [LogoutPath](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.logoutpath), a [AccessDeniedPath](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.accessdeniedpath):</span><span class="sxs-lookup"><span data-stu-id="69d16-150">The following the code sets the [LoginPath](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.loginpath), [LogoutPath](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.logoutpath), and [AccessDeniedPath](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.accessdeniedpath):</span></span>

[!code-csharp[](scaffold-identity/sample/StartupFull.cs?name=snippet3)]

<span data-ttu-id="69d16-151">Registrace `IEmailSender` implementace, například:</span><span class="sxs-lookup"><span data-stu-id="69d16-151">Register an `IEmailSender` implementation, for example:</span></span>

[!code-csharp[](scaffold-identity/sample/StartupFull.cs?name=snippet4)]

[!code-csharp[](scaffold-identity/sample/StartupFull.cs?name=snippet)]

## <a name="additional-resources"></a><span data-ttu-id="69d16-152">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="69d16-152">Additional resources</span></span>

* [<span data-ttu-id="69d16-153">Změny kódu ověřování ASP.NET Core 2.1 a vyšší</span><span class="sxs-lookup"><span data-stu-id="69d16-153">Changes to authentication code to ASP.NET Core 2.1 and later</span></span>](xref:migration/20_21#changes-to-authentication-code)
