---
title: Statické soubory v ASP.NET Core
author: rick-anderson
description: Zjistěte, jak poskytovat zabezpečení statické soubory a konfigurace statického souboru hostování chování middlewaru ve webové aplikaci ASP.NET Core.
ms.author: riande
ms.custom: mvc
ms.date: 12/18/2018
uid: fundamentals/static-files
ms.openlocfilehash: e6bda5dd60c62c7bdbfa81f34c14cfcd07e8d700
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57071284"
---
# <a name="static-files-in-aspnet-core"></a><span data-ttu-id="4da01-103">Statické soubory v ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="4da01-103">Static files in ASP.NET Core</span></span>

<span data-ttu-id="4da01-104">Podle [Rick Anderson](https://twitter.com/RickAndMSFT) a [Scott Addie](https://twitter.com/Scott_Addie)</span><span class="sxs-lookup"><span data-stu-id="4da01-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Scott Addie](https://twitter.com/Scott_Addie)</span></span>

<span data-ttu-id="4da01-105">Statické soubory, jako jsou HTML, CSS, obrázky a JavaScript, představují majetek, který obsluhuje aplikace ASP.NET Core přímo pro klienty.</span><span class="sxs-lookup"><span data-stu-id="4da01-105">Static files, such as HTML, CSS, images, and JavaScript, are assets an ASP.NET Core app serves directly to clients.</span></span> <span data-ttu-id="4da01-106">Některé konfigurace je potřeba povolit poskytování obsahu těchto souborů.</span><span class="sxs-lookup"><span data-stu-id="4da01-106">Some configuration is required to enable serving of these files.</span></span>

<span data-ttu-id="4da01-107">[Zobrazení nebo stažení ukázkového kódu](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/static-files/samples) ([stažení](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="4da01-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/static-files/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="serve-static-files"></a><span data-ttu-id="4da01-108">Doručování statických souborů</span><span class="sxs-lookup"><span data-stu-id="4da01-108">Serve static files</span></span>

<span data-ttu-id="4da01-109">Statické soubory jsou uloženy v kořenovém adresáři vašeho projektu web.</span><span class="sxs-lookup"><span data-stu-id="4da01-109">Static files are stored within your project's web root directory.</span></span> <span data-ttu-id="4da01-110">Výchozí adresář je  *\<content_root > / wwwroot*, ale můžete změnit prostřednictvím [UseWebRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usewebroot#Microsoft_AspNetCore_Hosting_HostingAbstractionsWebHostBuilderExtensions_UseWebRoot_Microsoft_AspNetCore_Hosting_IWebHostBuilder_System_String_) metody.</span><span class="sxs-lookup"><span data-stu-id="4da01-110">The default directory is *\<content_root>/wwwroot*, but it can be changed via the [UseWebRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usewebroot#Microsoft_AspNetCore_Hosting_HostingAbstractionsWebHostBuilderExtensions_UseWebRoot_Microsoft_AspNetCore_Hosting_IWebHostBuilder_System_String_) method.</span></span> <span data-ttu-id="4da01-111">Zobrazit [obsahu kořenové](xref:fundamentals/index#content-root) a [kořenový adresář webové](xref:fundamentals/index#web-root) Další informace.</span><span class="sxs-lookup"><span data-stu-id="4da01-111">See [Content root](xref:fundamentals/index#content-root) and [Web root](xref:fundamentals/index#web-root) for more information.</span></span>

<span data-ttu-id="4da01-112">Hostitel webové aplikace musí být informováni obsahu kořenový adresář.</span><span class="sxs-lookup"><span data-stu-id="4da01-112">The app's web host must be made aware of the content root directory.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="4da01-113">`WebHost.CreateDefaultBuilder` Metoda nastaví kořenu obsahu do aktuálního adresáře:</span><span class="sxs-lookup"><span data-stu-id="4da01-113">The `WebHost.CreateDefaultBuilder` method sets the content root to the current directory:</span></span>

[!code-csharp[](../common/samples/WebApplication1DotNetCore2.0App/Program.cs?name=snippet_Main&highlight=9)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="4da01-114">Nastavení obsahu kořenovém adresáři aktuální adresář vyvoláním [UseContentRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usecontentroot#Microsoft_AspNetCore_Hosting_HostingAbstractionsWebHostBuilderExtensions_UseContentRoot_Microsoft_AspNetCore_Hosting_IWebHostBuilder_System_String_) uvnitř `Program.Main`:</span><span class="sxs-lookup"><span data-stu-id="4da01-114">Set the content root to the current directory by invoking [UseContentRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usecontentroot#Microsoft_AspNetCore_Hosting_HostingAbstractionsWebHostBuilderExtensions_UseContentRoot_Microsoft_AspNetCore_Hosting_IWebHostBuilder_System_String_) inside of `Program.Main`:</span></span>

[!code-csharp[](static-files/samples/1x/Program.cs?name=snippet_ProgramClass&highlight=7)]

::: moniker-end

<span data-ttu-id="4da01-115">Statické soubory jsou přístupné přes cestu relativní vzhledem k kořenový adresář webové.</span><span class="sxs-lookup"><span data-stu-id="4da01-115">Static files are accessible via a path relative to the web root.</span></span> <span data-ttu-id="4da01-116">Například **webovou aplikaci** šablonu projektu obsahuje několik složek v rámci *wwwroot* složky:</span><span class="sxs-lookup"><span data-stu-id="4da01-116">For example, the **Web Application** project template contains several folders within the *wwwroot* folder:</span></span>

* <span data-ttu-id="4da01-117">**wwwroot**</span><span class="sxs-lookup"><span data-stu-id="4da01-117">**wwwroot**</span></span>
  * <span data-ttu-id="4da01-118">**css**</span><span class="sxs-lookup"><span data-stu-id="4da01-118">**css**</span></span>
  * <span data-ttu-id="4da01-119">**Bitové kopie**</span><span class="sxs-lookup"><span data-stu-id="4da01-119">**images**</span></span>
  * <span data-ttu-id="4da01-120">**js**</span><span class="sxs-lookup"><span data-stu-id="4da01-120">**js**</span></span>

<span data-ttu-id="4da01-121">Formát identifikátoru URI pro přístup k souboru v *image* je podsložka *http://\<server_address > /images/\<image_file_name >*.</span><span class="sxs-lookup"><span data-stu-id="4da01-121">The URI format to access a file in the *images* subfolder is *http://\<server_address>/images/\<image_file_name>*.</span></span> <span data-ttu-id="4da01-122">Například *http://localhost:9189/images/banner3.svg*.</span><span class="sxs-lookup"><span data-stu-id="4da01-122">For example, *http://localhost:9189/images/banner3.svg*.</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="4da01-123">Pokud se zaměřujete na rozhraní .NET Framework, přidejte [Microsoft.AspNetCore.StaticFiles](https://www.nuget.org/packages/Microsoft.AspNetCore.StaticFiles/) do svého projektu balíček.</span><span class="sxs-lookup"><span data-stu-id="4da01-123">If targeting .NET Framework, add the [Microsoft.AspNetCore.StaticFiles](https://www.nuget.org/packages/Microsoft.AspNetCore.StaticFiles/) package to your project.</span></span> <span data-ttu-id="4da01-124">Pokud je zaměřen na .NET Core [Microsoft.AspNetCore.App Microsoft.aspnetcore.all](xref:fundamentals/metapackage-app) zahrnuje tento balíček.</span><span class="sxs-lookup"><span data-stu-id="4da01-124">If targeting .NET Core, the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) includes this package.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="4da01-125">Pokud se zaměřujete na rozhraní .NET Framework, přidejte [Microsoft.AspNetCore.StaticFiles](https://www.nuget.org/packages/Microsoft.AspNetCore.StaticFiles/) do svého projektu balíček.</span><span class="sxs-lookup"><span data-stu-id="4da01-125">If targeting .NET Framework, add the [Microsoft.AspNetCore.StaticFiles](https://www.nuget.org/packages/Microsoft.AspNetCore.StaticFiles/) package to your project.</span></span> <span data-ttu-id="4da01-126">Pokud je zaměřen na .NET Core [metabalíček Microsoft.aspnetcore.all](xref:fundamentals/metapackage) zahrnuje tento balíček.</span><span class="sxs-lookup"><span data-stu-id="4da01-126">If targeting .NET Core, the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage) includes this package.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="4da01-127">Přidat [Microsoft.AspNetCore.StaticFiles](https://www.nuget.org/packages/Microsoft.AspNetCore.StaticFiles/) do svého projektu balíček.</span><span class="sxs-lookup"><span data-stu-id="4da01-127">Add the [Microsoft.AspNetCore.StaticFiles](https://www.nuget.org/packages/Microsoft.AspNetCore.StaticFiles/) package to your project.</span></span>

::: moniker-end

<span data-ttu-id="4da01-128">Konfigurace [middleware](xref:fundamentals/middleware/index) umožňující poskytování obsahu statických souborů.</span><span class="sxs-lookup"><span data-stu-id="4da01-128">Configure the [middleware](xref:fundamentals/middleware/index) which enables the serving of static files.</span></span>

### <a name="serve-files-inside-of-web-root"></a><span data-ttu-id="4da01-129">Soubory v rámci kořenový adresář webové poskytovat</span><span class="sxs-lookup"><span data-stu-id="4da01-129">Serve files inside of web root</span></span>

<span data-ttu-id="4da01-130">Vyvolat [UseStaticFiles](/dotnet/api/microsoft.aspnetcore.builder.staticfileextensions.usestaticfiles#Microsoft_AspNetCore_Builder_StaticFileExtensions_UseStaticFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_) metody v rámci `Startup.Configure`:</span><span class="sxs-lookup"><span data-stu-id="4da01-130">Invoke the [UseStaticFiles](/dotnet/api/microsoft.aspnetcore.builder.staticfileextensions.usestaticfiles#Microsoft_AspNetCore_Builder_StaticFileExtensions_UseStaticFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_) method within `Startup.Configure`:</span></span>

[!code-csharp[](static-files/samples/1x/StartupStaticFiles.cs?name=snippet_ConfigureMethod&highlight=3)]

<span data-ttu-id="4da01-131">Bezparametrová `UseStaticFiles` soubory v kořenovém adresáři webové jako servable označí přetížení metody.</span><span class="sxs-lookup"><span data-stu-id="4da01-131">The parameterless `UseStaticFiles` method overload marks the files in web root as servable.</span></span> <span data-ttu-id="4da01-132">Následující odkazy na kód *wwwroot/images/banner1.svg*:</span><span class="sxs-lookup"><span data-stu-id="4da01-132">The following markup references *wwwroot/images/banner1.svg*:</span></span>

[!code-cshtml[](static-files/samples/1x/Views/Home/Index.cshtml?name=snippet_static_file_wwwroot)]

<span data-ttu-id="4da01-133">V předchozím kódu znak tilda `~/` odkazuje na webroot.</span><span class="sxs-lookup"><span data-stu-id="4da01-133">In the preceding code, the tilde character `~/` points to webroot.</span></span> <span data-ttu-id="4da01-134">Další informace najdete v tématu [kořenový adresář webové](xref:fundamentals/index#web-root).</span><span class="sxs-lookup"><span data-stu-id="4da01-134">For more information, see [Web root](xref:fundamentals/index#web-root).</span></span>

### <a name="serve-files-outside-of-web-root"></a><span data-ttu-id="4da01-135">Soubory mimo kořenový adresář webové poskytovat</span><span class="sxs-lookup"><span data-stu-id="4da01-135">Serve files outside of web root</span></span>

<span data-ttu-id="4da01-136">Vezměte v úvahu hierarchii adresářů, ve kterém se obsluhovat statické soubory nacházejí mimo kořenový adresář webové:</span><span class="sxs-lookup"><span data-stu-id="4da01-136">Consider a directory hierarchy in which the static files to be served reside outside of the web root:</span></span>

* <span data-ttu-id="4da01-137">**wwwroot**</span><span class="sxs-lookup"><span data-stu-id="4da01-137">**wwwroot**</span></span>
  * <span data-ttu-id="4da01-138">**css**</span><span class="sxs-lookup"><span data-stu-id="4da01-138">**css**</span></span>
  * <span data-ttu-id="4da01-139">**Bitové kopie**</span><span class="sxs-lookup"><span data-stu-id="4da01-139">**images**</span></span>
  * <span data-ttu-id="4da01-140">**js**</span><span class="sxs-lookup"><span data-stu-id="4da01-140">**js**</span></span>
* <span data-ttu-id="4da01-141">**MyStaticFiles**</span><span class="sxs-lookup"><span data-stu-id="4da01-141">**MyStaticFiles**</span></span>
  * <span data-ttu-id="4da01-142">**Bitové kopie**</span><span class="sxs-lookup"><span data-stu-id="4da01-142">**images**</span></span>
      * <span data-ttu-id="4da01-143">*banner1.svg*</span><span class="sxs-lookup"><span data-stu-id="4da01-143">*banner1.svg*</span></span>

<span data-ttu-id="4da01-144">Žádost o přístup *banner1.svg* souboru nakonfigurováním Middleware statické soubory:</span><span class="sxs-lookup"><span data-stu-id="4da01-144">A request can access the *banner1.svg* file by configuring the Static File Middleware as follows:</span></span>

[!code-csharp[](static-files/samples/1x/StartupTwoStaticFiles.cs?name=snippet_ConfigureMethod&highlight=5-10)]

<span data-ttu-id="4da01-145">V předchozím kódu *MyStaticFiles* hierarchii adresářů jsou veřejně dostupné prostřednictvím *StaticFiles* segment identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="4da01-145">In the preceding code, the *MyStaticFiles* directory hierarchy is exposed publicly via the *StaticFiles* URI segment.</span></span> <span data-ttu-id="4da01-146">Požadavek na *http://\<server_address > /StaticFiles/images/banner1.svg* slouží *banner1.svg* souboru.</span><span class="sxs-lookup"><span data-stu-id="4da01-146">A request to *http://\<server_address>/StaticFiles/images/banner1.svg* serves the *banner1.svg* file.</span></span>

<span data-ttu-id="4da01-147">Následující odkazy na kód *MyStaticFiles/images/banner1.svg*:</span><span class="sxs-lookup"><span data-stu-id="4da01-147">The following markup references *MyStaticFiles/images/banner1.svg*:</span></span>

[!code-cshtml[](static-files/samples/1x/Views/Home/Index.cshtml?name=snippet_static_file_outside)]

### <a name="set-http-response-headers"></a><span data-ttu-id="4da01-148">Nastavit hlavičky HTTP odpovědi</span><span class="sxs-lookup"><span data-stu-id="4da01-148">Set HTTP response headers</span></span>

<span data-ttu-id="4da01-149">A [StaticFileOptions](/dotnet/api/microsoft.aspnetcore.builder.staticfileoptions) objekt lze použít k nastavení hlavičky HTTP odpovědi.</span><span class="sxs-lookup"><span data-stu-id="4da01-149">A [StaticFileOptions](/dotnet/api/microsoft.aspnetcore.builder.staticfileoptions) object can be used to set HTTP response headers.</span></span> <span data-ttu-id="4da01-150">Kromě poskytování obsahu statického souboru z kořenový adresář webové konfigurace, následující kód nastaví `Cache-Control` hlavičky:</span><span class="sxs-lookup"><span data-stu-id="4da01-150">In addition to configuring static file serving from the web root, the following code sets the `Cache-Control` header:</span></span>

[!code-csharp[](static-files/samples/1x/StartupAddHeader.cs?name=snippet_ConfigureMethod)]

<span data-ttu-id="4da01-151">[HeaderDictionaryExtensions.Append](/dotnet/api/microsoft.aspnetcore.http.headerdictionaryextensions.append) metoda nachází [Microsoft.AspNetCore.Http](https://www.nuget.org/packages/Microsoft.AspNetCore.Http/) balíčku.</span><span class="sxs-lookup"><span data-stu-id="4da01-151">The [HeaderDictionaryExtensions.Append](/dotnet/api/microsoft.aspnetcore.http.headerdictionaryextensions.append) method exists in the [Microsoft.AspNetCore.Http](https://www.nuget.org/packages/Microsoft.AspNetCore.Http/) package.</span></span>

<span data-ttu-id="4da01-152">Soubory byly provedeny veřejně možné ukládat do mezipaměti po dobu 10 minut (600 sekund) ve vývojovém prostředí:</span><span class="sxs-lookup"><span data-stu-id="4da01-152">The files have been made publicly cacheable for 10 minutes (600 seconds) in the Development environment:</span></span>

![Byla přidána hlavičky odpovědi zobrazující hlavičku Cache-Control](static-files/_static/add-header.png)

## <a name="static-file-authorization"></a><span data-ttu-id="4da01-154">Statický soubor autorizace</span><span class="sxs-lookup"><span data-stu-id="4da01-154">Static file authorization</span></span>

<span data-ttu-id="4da01-155">Middleware statické soubory neposkytuje kontroly autorizace.</span><span class="sxs-lookup"><span data-stu-id="4da01-155">The Static File Middleware doesn't provide authorization checks.</span></span> <span data-ttu-id="4da01-156">Všechny soubory obsluhuje, včetně těch *wwwroot*, jsou veřejně přístupné.</span><span class="sxs-lookup"><span data-stu-id="4da01-156">Any files served by it, including those under *wwwroot*, are publicly accessible.</span></span> <span data-ttu-id="4da01-157">Poskytování souborů na základě autorizace:</span><span class="sxs-lookup"><span data-stu-id="4da01-157">To serve files based on authorization:</span></span>

* <span data-ttu-id="4da01-158">Store je mimo *wwwroot* a ke každému adresáři přístupné pro Middleware statické soubory.</span><span class="sxs-lookup"><span data-stu-id="4da01-158">Store them outside of *wwwroot* and any directory accessible to the Static File Middleware.</span></span>
* <span data-ttu-id="4da01-159">Zajišťovat obsluhu prostřednictvím metodu akce, pro které je použito autorizace.</span><span class="sxs-lookup"><span data-stu-id="4da01-159">Serve them via an action method to which authorization is applied.</span></span> <span data-ttu-id="4da01-160">Vrátit [FileResult](/dotnet/api/microsoft.aspnetcore.mvc.fileresult) objektu:</span><span class="sxs-lookup"><span data-stu-id="4da01-160">Return a [FileResult](/dotnet/api/microsoft.aspnetcore.mvc.fileresult) object:</span></span>

  [!code-csharp[](static-files/samples/1x/Controllers/HomeController.cs?name=snippet_BannerImageAction)]

## <a name="enable-directory-browsing"></a><span data-ttu-id="4da01-161">Povolí procházení adresáře</span><span class="sxs-lookup"><span data-stu-id="4da01-161">Enable directory browsing</span></span>

<span data-ttu-id="4da01-162">Procházení adresářů umožňuje uživatelům vaší webové aplikace najdete v seznamu adresářů a souborů v rámci zadaného adresáře.</span><span class="sxs-lookup"><span data-stu-id="4da01-162">Directory browsing allows users of your web app to see a directory listing and files within a specified directory.</span></span> <span data-ttu-id="4da01-163">Procházení adresářů je zakázané ve výchozím nastavení z bezpečnostních důvodů (viz [aspekty](#considerations)).</span><span class="sxs-lookup"><span data-stu-id="4da01-163">Directory browsing is disabled by default for security reasons (see [Considerations](#considerations)).</span></span> <span data-ttu-id="4da01-164">Povolit procházení vyvoláním adresářů [UseDirectoryBrowser](/dotnet/api/microsoft.aspnetcore.builder.directorybrowserextensions.usedirectorybrowser#Microsoft_AspNetCore_Builder_DirectoryBrowserExtensions_UseDirectoryBrowser_Microsoft_AspNetCore_Builder_IApplicationBuilder_Microsoft_AspNetCore_Builder_DirectoryBrowserOptions_) metoda ve `Startup.Configure`:</span><span class="sxs-lookup"><span data-stu-id="4da01-164">Enable directory browsing by invoking the [UseDirectoryBrowser](/dotnet/api/microsoft.aspnetcore.builder.directorybrowserextensions.usedirectorybrowser#Microsoft_AspNetCore_Builder_DirectoryBrowserExtensions_UseDirectoryBrowser_Microsoft_AspNetCore_Builder_IApplicationBuilder_Microsoft_AspNetCore_Builder_DirectoryBrowserOptions_) method in `Startup.Configure`:</span></span>

[!code-csharp[](static-files/samples/1x/StartupBrowse.cs?name=snippet_ConfigureMethod&highlight=12-17)]

<span data-ttu-id="4da01-165">Přidání požadovaných služeb vyvoláním [AddDirectoryBrowser](/dotnet/api/microsoft.extensions.dependencyinjection.directorybrowserserviceextensions.adddirectorybrowser#Microsoft_Extensions_DependencyInjection_DirectoryBrowserServiceExtensions_AddDirectoryBrowser_Microsoft_Extensions_DependencyInjection_IServiceCollection_) metodu z `Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="4da01-165">Add required services by invoking the [AddDirectoryBrowser](/dotnet/api/microsoft.extensions.dependencyinjection.directorybrowserserviceextensions.adddirectorybrowser#Microsoft_Extensions_DependencyInjection_DirectoryBrowserServiceExtensions_AddDirectoryBrowser_Microsoft_Extensions_DependencyInjection_IServiceCollection_) method from `Startup.ConfigureServices`:</span></span>

[!code-csharp[](static-files/samples/1x/StartupBrowse.cs?name=snippet_ConfigureServicesMethod&highlight=3)]

<span data-ttu-id="4da01-166">Předchozí kód umožňuje procházení adresáře *wwwroot/imagí* složky pomocí adresy URL *http://\<server_address > / MyImages*, s odkazy na všechny soubory a složky:</span><span class="sxs-lookup"><span data-stu-id="4da01-166">The preceding code allows directory browsing of the *wwwroot/images* folder using the URL *http://\<server_address>/MyImages*, with links to each file and folder:</span></span>

![procházení adresářů](static-files/_static/dir-browse.png)

<span data-ttu-id="4da01-168">Zobrazit [aspekty](#considerations) na bezpečnostní rizika při povolování procházení.</span><span class="sxs-lookup"><span data-stu-id="4da01-168">See [Considerations](#considerations) on the security risks when enabling browsing.</span></span>

<span data-ttu-id="4da01-169">Všimněte si, dvě `UseStaticFiles` volá v následujícím příkladu.</span><span class="sxs-lookup"><span data-stu-id="4da01-169">Note the two `UseStaticFiles` calls in the following example.</span></span> <span data-ttu-id="4da01-170">Umožňuje při obsluze statických souborů v prvním volání *wwwroot* složky.</span><span class="sxs-lookup"><span data-stu-id="4da01-170">The first call enables the serving of static files in the *wwwroot* folder.</span></span> <span data-ttu-id="4da01-171">Druhé volání povolí procházení adresáře *wwwroot/imagí* složky pomocí adresy URL *http://\<server_address > / MyImages*:</span><span class="sxs-lookup"><span data-stu-id="4da01-171">The second call enables directory browsing of the *wwwroot/images* folder using the URL *http://\<server_address>/MyImages*:</span></span>

[!code-csharp[](static-files/samples/1x/StartupBrowse.cs?name=snippet_ConfigureMethod&highlight=3,5)]

## <a name="serve-a-default-document"></a><span data-ttu-id="4da01-172">Výchozí dokument</span><span class="sxs-lookup"><span data-stu-id="4da01-172">Serve a default document</span></span>

<span data-ttu-id="4da01-173">Nastavení výchozí domovskou stránku poskytuje návštěvníků logické výchozí bod při návštěvě webu.</span><span class="sxs-lookup"><span data-stu-id="4da01-173">Setting a default home page provides visitors a logical starting point when visiting your site.</span></span> <span data-ttu-id="4da01-174">Chcete-li poskytovat výchozí stránku bez plně kvalifikovaného identifikátoru URI uživatele, zavolejte [UseDefaultFiles](/dotnet/api/microsoft.aspnetcore.builder.defaultfilesextensions.usedefaultfiles#Microsoft_AspNetCore_Builder_DefaultFilesExtensions_UseDefaultFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_) metodu z `Startup.Configure`:</span><span class="sxs-lookup"><span data-stu-id="4da01-174">To serve a default page without the user fully qualifying the URI, call the [UseDefaultFiles](/dotnet/api/microsoft.aspnetcore.builder.defaultfilesextensions.usedefaultfiles#Microsoft_AspNetCore_Builder_DefaultFilesExtensions_UseDefaultFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_) method from `Startup.Configure`:</span></span>

[!code-csharp[](static-files/samples/1x/StartupEmpty.cs?name=snippet_ConfigureMethod&highlight=3)]

> [!IMPORTANT]
> <span data-ttu-id="4da01-175">`UseDefaultFiles` musí být volána před `UseStaticFiles` poskytovat výchozí soubor.</span><span class="sxs-lookup"><span data-stu-id="4da01-175">`UseDefaultFiles` must be called before `UseStaticFiles` to serve the default file.</span></span> <span data-ttu-id="4da01-176">`UseDefaultFiles` je RW adresu URL, který bariéru ve skutečnosti soubor.</span><span class="sxs-lookup"><span data-stu-id="4da01-176">`UseDefaultFiles` is a URL rewriter that doesn't actually serve the file.</span></span> <span data-ttu-id="4da01-177">Povolit statický soubor Middleware prostřednictvím `UseStaticFiles` poskytovat souboru.</span><span class="sxs-lookup"><span data-stu-id="4da01-177">Enable Static File Middleware via `UseStaticFiles` to serve the file.</span></span>

<span data-ttu-id="4da01-178">S `UseDefaultFiles`, požadavky na složku vyhledávání:</span><span class="sxs-lookup"><span data-stu-id="4da01-178">With `UseDefaultFiles`, requests to a folder search for:</span></span>

* <span data-ttu-id="4da01-179">*default.htm*</span><span class="sxs-lookup"><span data-stu-id="4da01-179">*default.htm*</span></span>
* <span data-ttu-id="4da01-180">*default.html*</span><span class="sxs-lookup"><span data-stu-id="4da01-180">*default.html*</span></span>
* <span data-ttu-id="4da01-181">*index.htm*</span><span class="sxs-lookup"><span data-stu-id="4da01-181">*index.htm*</span></span>
* <span data-ttu-id="4da01-182">*index.html*</span><span class="sxs-lookup"><span data-stu-id="4da01-182">*index.html*</span></span>

<span data-ttu-id="4da01-183">První soubor nalezen v seznamu obsluhuje jakoby byly plně kvalifikovaného identifikátoru URI požadavku.</span><span class="sxs-lookup"><span data-stu-id="4da01-183">The first file found from the list is served as though the request were the fully qualified URI.</span></span> <span data-ttu-id="4da01-184">Adresa URL prohlížeče pokračuje tak, aby odrážely identifikátoru URI požadavku.</span><span class="sxs-lookup"><span data-stu-id="4da01-184">The browser URL continues to reflect the URI requested.</span></span>

<span data-ttu-id="4da01-185">Následující kód změní výchozí název souboru *mydefault.html*:</span><span class="sxs-lookup"><span data-stu-id="4da01-185">The following code changes the default file name to *mydefault.html*:</span></span>

[!code-csharp[](static-files/samples/1x/StartupDefault.cs?name=snippet_ConfigureMethod)]

## <a name="usefileserver"></a><span data-ttu-id="4da01-186">UseFileServer</span><span class="sxs-lookup"><span data-stu-id="4da01-186">UseFileServer</span></span>

<span data-ttu-id="4da01-187">[UseFileServer](/dotnet/api/microsoft.aspnetcore.builder.fileserverextensions.usefileserver#Microsoft_AspNetCore_Builder_FileServerExtensions_UseFileServer_Microsoft_AspNetCore_Builder_IApplicationBuilder_) kombinuje funkce `UseStaticFiles`, `UseDefaultFiles`, a `UseDirectoryBrowser`.</span><span class="sxs-lookup"><span data-stu-id="4da01-187">[UseFileServer](/dotnet/api/microsoft.aspnetcore.builder.fileserverextensions.usefileserver#Microsoft_AspNetCore_Builder_FileServerExtensions_UseFileServer_Microsoft_AspNetCore_Builder_IApplicationBuilder_) combines the functionality of `UseStaticFiles`, `UseDefaultFiles`, and `UseDirectoryBrowser`.</span></span>

<span data-ttu-id="4da01-188">Následující kód umožní obsluhující statické soubory a výchozí soubor.</span><span class="sxs-lookup"><span data-stu-id="4da01-188">The following code enables the serving of static files and the default file.</span></span> <span data-ttu-id="4da01-189">Procházení adresářů není povoleno.</span><span class="sxs-lookup"><span data-stu-id="4da01-189">Directory browsing isn't enabled.</span></span>

```csharp
app.UseFileServer();
```

<span data-ttu-id="4da01-190">Následující kód staví na bez parametrů přetížení tím, že procházení adresářů:</span><span class="sxs-lookup"><span data-stu-id="4da01-190">The following code builds upon the parameterless overload by enabling directory browsing:</span></span>

```csharp
app.UseFileServer(enableDirectoryBrowsing: true);
```

<span data-ttu-id="4da01-191">Vezměte v úvahu následující hierarchii adresářů:</span><span class="sxs-lookup"><span data-stu-id="4da01-191">Consider the following directory hierarchy:</span></span>

* <span data-ttu-id="4da01-192">**wwwroot**</span><span class="sxs-lookup"><span data-stu-id="4da01-192">**wwwroot**</span></span>
  * <span data-ttu-id="4da01-193">**css**</span><span class="sxs-lookup"><span data-stu-id="4da01-193">**css**</span></span>
  * <span data-ttu-id="4da01-194">**Bitové kopie**</span><span class="sxs-lookup"><span data-stu-id="4da01-194">**images**</span></span>
  * <span data-ttu-id="4da01-195">**js**</span><span class="sxs-lookup"><span data-stu-id="4da01-195">**js**</span></span>
* <span data-ttu-id="4da01-196">**MyStaticFiles**</span><span class="sxs-lookup"><span data-stu-id="4da01-196">**MyStaticFiles**</span></span>
  * <span data-ttu-id="4da01-197">**Bitové kopie**</span><span class="sxs-lookup"><span data-stu-id="4da01-197">**images**</span></span>
      * <span data-ttu-id="4da01-198">*banner1.svg*</span><span class="sxs-lookup"><span data-stu-id="4da01-198">*banner1.svg*</span></span>
  * <span data-ttu-id="4da01-199">*default.html*</span><span class="sxs-lookup"><span data-stu-id="4da01-199">*default.html*</span></span>

<span data-ttu-id="4da01-200">Následující kód umožní statické soubory, výchozí soubory a adresáře procházení `MyStaticFiles`:</span><span class="sxs-lookup"><span data-stu-id="4da01-200">The following code enables static files, default files, and directory browsing of `MyStaticFiles`:</span></span>

[!code-csharp[](static-files/samples/1x/StartupUseFileServer.cs?name=snippet_ConfigureMethod&highlight=5-11)]

<span data-ttu-id="4da01-201">`AddDirectoryBrowser` musí být voláno, když `EnableDirectoryBrowsing` hodnota vlastnosti je `true`:</span><span class="sxs-lookup"><span data-stu-id="4da01-201">`AddDirectoryBrowser` must be called when the `EnableDirectoryBrowsing` property value is `true`:</span></span>

[!code-csharp[](static-files/samples/1x/StartupUseFileServer.cs?name=snippet_ConfigureServicesMethod)]

<span data-ttu-id="4da01-202">Pomocí hierarchie souborů a předcházející kódu, adresy URL vyřešíte takto:</span><span class="sxs-lookup"><span data-stu-id="4da01-202">Using the file hierarchy and preceding code, URLs resolve as follows:</span></span>

| <span data-ttu-id="4da01-203">Identifikátor URI</span><span class="sxs-lookup"><span data-stu-id="4da01-203">URI</span></span>            |                             <span data-ttu-id="4da01-204">Odpověď</span><span class="sxs-lookup"><span data-stu-id="4da01-204">Response</span></span>  |
| ------- | ------|
| <span data-ttu-id="4da01-205">*http://\<server_address>/StaticFiles/images/banner1.svg*</span><span class="sxs-lookup"><span data-stu-id="4da01-205">*http://\<server_address>/StaticFiles/images/banner1.svg*</span></span>    |      <span data-ttu-id="4da01-206">MyStaticFiles/images/banner1.svg</span><span class="sxs-lookup"><span data-stu-id="4da01-206">MyStaticFiles/images/banner1.svg</span></span> |
| <span data-ttu-id="4da01-207">*http://\<server_address>/StaticFiles*</span><span class="sxs-lookup"><span data-stu-id="4da01-207">*http://\<server_address>/StaticFiles*</span></span>             |     <span data-ttu-id="4da01-208">MyStaticFiles/default.html</span><span class="sxs-lookup"><span data-stu-id="4da01-208">MyStaticFiles/default.html</span></span> |

<span data-ttu-id="4da01-209">Pokud neexistuje žádný soubor s názvem výchozí v *MyStaticFiles* adresáři *http://\<server_address > / StaticFiles* vrátí výpis s odkazy kliknout, čímž adresáře:</span><span class="sxs-lookup"><span data-stu-id="4da01-209">If no default-named file exists in the *MyStaticFiles* directory, *http://\<server_address>/StaticFiles* returns the directory listing with clickable links:</span></span>

![Seznam statické soubory](static-files/_static/db2.png)

> [!NOTE]
> <span data-ttu-id="4da01-211">`UseDefaultFiles` a `UseDirectoryBrowser` použijte adresu URL *http://\<server_address > / StaticFiles* bez do adresy koncové lomítko k aktivaci na straně klienta přesměrovat na *http://\<server_address > / StaticFiles /*.</span><span class="sxs-lookup"><span data-stu-id="4da01-211">`UseDefaultFiles` and `UseDirectoryBrowser` use the URL *http://\<server_address>/StaticFiles* without the trailing slash to trigger a client-side redirect to *http://\<server_address>/StaticFiles/*.</span></span> <span data-ttu-id="4da01-212">Všimněte si, že přidání do adresy koncové lomítko.</span><span class="sxs-lookup"><span data-stu-id="4da01-212">Notice the addition of the trailing slash.</span></span> <span data-ttu-id="4da01-213">Relativní adresy URL v rámci dokumenty jsou považovány za neplatné bez koncové lomítko.</span><span class="sxs-lookup"><span data-stu-id="4da01-213">Relative URLs within the documents are deemed invalid without a trailing slash.</span></span>

## <a name="fileextensioncontenttypeprovider"></a><span data-ttu-id="4da01-214">FileExtensionContentTypeProvider</span><span class="sxs-lookup"><span data-stu-id="4da01-214">FileExtensionContentTypeProvider</span></span>

<span data-ttu-id="4da01-215">[FileExtensionContentTypeProvider](/dotnet/api/microsoft.aspnetcore.staticfiles.fileextensioncontenttypeprovider) obsahuje třídy `Mappings` vlastnost slouží jako mapování přípony souborů pro typy MIME obsahu.</span><span class="sxs-lookup"><span data-stu-id="4da01-215">The [FileExtensionContentTypeProvider](/dotnet/api/microsoft.aspnetcore.staticfiles.fileextensioncontenttypeprovider) class contains a `Mappings` property serving as a mapping of file extensions to MIME content types.</span></span> <span data-ttu-id="4da01-216">V následujícím příkladu je několik přípony souborů zaregistrovaná známé typy MIME.</span><span class="sxs-lookup"><span data-stu-id="4da01-216">In the following sample, several file extensions are registered to known MIME types.</span></span> <span data-ttu-id="4da01-217">*.Rtf* nahrazuje rozšíření a *MP4* se odebere.</span><span class="sxs-lookup"><span data-stu-id="4da01-217">The *.rtf* extension is replaced, and *.mp4* is removed.</span></span>

[!code-csharp[](static-files/samples/1x/StartupFileExtensionContentTypeProvider.cs?name=snippet_ConfigureMethod&highlight=3-12,19)]

<span data-ttu-id="4da01-218">Zobrazit [typy MIME obsahu](http://www.iana.org/assignments/media-types/media-types.xhtml).</span><span class="sxs-lookup"><span data-stu-id="4da01-218">See [MIME content types](http://www.iana.org/assignments/media-types/media-types.xhtml).</span></span>

## <a name="non-standard-content-types"></a><span data-ttu-id="4da01-219">Nestandardní typy obsahu</span><span class="sxs-lookup"><span data-stu-id="4da01-219">Non-standard content types</span></span>

<span data-ttu-id="4da01-220">Middleware statické soubory rozumí téměř 400 souborů známých typů obsahu.</span><span class="sxs-lookup"><span data-stu-id="4da01-220">Static File Middleware understands almost 400 known file content types.</span></span> <span data-ttu-id="4da01-221">Pokud uživatel požaduje souboru se neznámý typ souborů, Middleware statické soubory požadavek předá do další middleware v kanálu.</span><span class="sxs-lookup"><span data-stu-id="4da01-221">If the user requests a file with an unknown file type, Static File Middleware passes the request to the next middleware in the pipeline.</span></span> <span data-ttu-id="4da01-222">Pokud žádné middleware zpracovává žádost, *404 Nenalezeno* vrátí odpověď.</span><span class="sxs-lookup"><span data-stu-id="4da01-222">If no middleware handles the request, a *404 Not Found* response is returned.</span></span> <span data-ttu-id="4da01-223">Pokud je povolené procházení adresáře, zobrazí se odkaz na soubor v seznamu adresářů.</span><span class="sxs-lookup"><span data-stu-id="4da01-223">If directory browsing is enabled, a link to the file is displayed in a directory listing.</span></span>

<span data-ttu-id="4da01-224">Následující kód umožní obsluhující neznámé typy a vykreslí Neznámý soubor jako image:</span><span class="sxs-lookup"><span data-stu-id="4da01-224">The following code enables serving unknown types and renders the unknown file as an image:</span></span>

[!code-csharp[](static-files/samples/1x/StartupServeUnknownFileTypes.cs?name=snippet_ConfigureMethod)]

<span data-ttu-id="4da01-225">Předchozí kód žádost o soubor s Neznámý typ obsahu se vrátí jako obrázek.</span><span class="sxs-lookup"><span data-stu-id="4da01-225">With the preceding code, a request for a file with an unknown content type is returned as an image.</span></span>

> [!WARNING]
> <span data-ttu-id="4da01-226">Povolení [ServeUnknownFileTypes](/dotnet/api/microsoft.aspnetcore.builder.staticfileoptions.serveunknownfiletypes#Microsoft_AspNetCore_Builder_StaticFileOptions_ServeUnknownFileTypes) představuje bezpečnostní riziko.</span><span class="sxs-lookup"><span data-stu-id="4da01-226">Enabling [ServeUnknownFileTypes](/dotnet/api/microsoft.aspnetcore.builder.staticfileoptions.serveunknownfiletypes#Microsoft_AspNetCore_Builder_StaticFileOptions_ServeUnknownFileTypes) is a security risk.</span></span> <span data-ttu-id="4da01-227">Ve výchozím nastavení je zakázána a jeho použití se nedoporučuje.</span><span class="sxs-lookup"><span data-stu-id="4da01-227">It's disabled by default, and its use is discouraged.</span></span> <span data-ttu-id="4da01-228">[FileExtensionContentTypeProvider](#fileextensioncontenttypeprovider) poskytuje bezpečnější alternativu se, že soubory se nestandardní rozšíření.</span><span class="sxs-lookup"><span data-stu-id="4da01-228">[FileExtensionContentTypeProvider](#fileextensioncontenttypeprovider) provides a safer alternative to serving files with non-standard extensions.</span></span>

### <a name="considerations"></a><span data-ttu-id="4da01-229">Požadavky</span><span class="sxs-lookup"><span data-stu-id="4da01-229">Considerations</span></span>

> [!WARNING]
> <span data-ttu-id="4da01-230">`UseDirectoryBrowser` a `UseStaticFiles` může způsobit únik těchto tajných kódů.</span><span class="sxs-lookup"><span data-stu-id="4da01-230">`UseDirectoryBrowser` and `UseStaticFiles` can leak secrets.</span></span> <span data-ttu-id="4da01-231">Důrazně doporučujeme zakázat procházení adresáře v produkčním prostředí.</span><span class="sxs-lookup"><span data-stu-id="4da01-231">Disabling directory browsing in production is highly recommended.</span></span> <span data-ttu-id="4da01-232">Pečlivě si prostudujte adresáře, které jsou povolené prostřednictvím `UseStaticFiles` nebo `UseDirectoryBrowser`.</span><span class="sxs-lookup"><span data-stu-id="4da01-232">Carefully review which directories are enabled via `UseStaticFiles` or `UseDirectoryBrowser`.</span></span> <span data-ttu-id="4da01-233">Celý adresář a jeho podadresářích stanou veřejně dostupné.</span><span class="sxs-lookup"><span data-stu-id="4da01-233">The entire directory and its sub-directories become publicly accessible.</span></span> <span data-ttu-id="4da01-234">Store soubory vhodný pro poskytování obsahu veřejně vyhrazené adresář, například  *\<content_root > / wwwroot*.</span><span class="sxs-lookup"><span data-stu-id="4da01-234">Store files suitable for serving to the public in a dedicated directory, such as *\<content_root>/wwwroot*.</span></span> <span data-ttu-id="4da01-235">Tyto soubory oddělte od zobrazení MVC Razor Pages (pouze 2.x), konfigurační soubory, atd.</span><span class="sxs-lookup"><span data-stu-id="4da01-235">Separate these files from MVC views, Razor Pages (2.x only), configuration files, etc.</span></span>

* <span data-ttu-id="4da01-236">Adresy URL pro obsah s `UseDirectoryBrowser` a `UseStaticFiles` musí dodržovat rozlišování velikosti písmen a omezení pro znaky základní systému souborů.</span><span class="sxs-lookup"><span data-stu-id="4da01-236">The URLs for content exposed with `UseDirectoryBrowser` and `UseStaticFiles` are subject to the case sensitivity and character restrictions of the underlying file system.</span></span> <span data-ttu-id="4da01-237">Například, velká a malá písmena Windows&mdash;macOS a Linux nejsou.</span><span class="sxs-lookup"><span data-stu-id="4da01-237">For example, Windows is case insensitive&mdash;macOS and Linux aren't.</span></span>

* <span data-ttu-id="4da01-238">Aplikace ASP.NET Core, které jsou hostované v IIS použít [modul ASP.NET Core](xref:host-and-deploy/aspnet-core-module) předávat všechny požadavky na aplikace, včetně žádostí o statický soubor.</span><span class="sxs-lookup"><span data-stu-id="4da01-238">ASP.NET Core apps hosted in IIS use the [ASP.NET Core Module](xref:host-and-deploy/aspnet-core-module) to forward all requests to the app, including static file requests.</span></span> <span data-ttu-id="4da01-239">Obslužná rutina statického souboru službě IIS se nepoužívá.</span><span class="sxs-lookup"><span data-stu-id="4da01-239">The IIS static file handler isn't used.</span></span> <span data-ttu-id="4da01-240">Nemá žádné riziko pro zpracování žádostí, než se zpracování modulem.</span><span class="sxs-lookup"><span data-stu-id="4da01-240">It has no chance to handle requests before they're handled by the module.</span></span>

* <span data-ttu-id="4da01-241">Proveďte následující kroky ve Správci služby IIS odebrat obslužnou rutinu statických souborů služby IIS na úrovni serveru nebo webu:</span><span class="sxs-lookup"><span data-stu-id="4da01-241">Complete the following steps in IIS Manager to remove the IIS static file handler at the server or website level:</span></span>
    1. <span data-ttu-id="4da01-242">Přejděte **moduly** funkce.</span><span class="sxs-lookup"><span data-stu-id="4da01-242">Navigate to the **Modules** feature.</span></span>
    1. <span data-ttu-id="4da01-243">Vyberte **iisver** v seznamu.</span><span class="sxs-lookup"><span data-stu-id="4da01-243">Select **StaticFileModule** in the list.</span></span>
    1. <span data-ttu-id="4da01-244">Klikněte na tlačítko **odebrat** v **akce** bočním panelu.</span><span class="sxs-lookup"><span data-stu-id="4da01-244">Click **Remove** in the **Actions** sidebar.</span></span>

> [!WARNING]
> <span data-ttu-id="4da01-245">Pokud je obslužná rutina statického souboru službě IIS povolená **a** modul ASP.NET Core není správně nakonfigurovaná, budou obsluhovat statické soubory.</span><span class="sxs-lookup"><span data-stu-id="4da01-245">If the IIS static file handler is enabled **and** the ASP.NET Core Module is configured incorrectly, static files are served.</span></span> <span data-ttu-id="4da01-246">K tomu dojde, například, pokud *web.config* soubor není nasazen.</span><span class="sxs-lookup"><span data-stu-id="4da01-246">This happens, for example, if the *web.config* file isn't deployed.</span></span>

* <span data-ttu-id="4da01-247">Umístěte soubory kódu (včetně *.cs* a *.cshtml*) mimo kořenový adresář webové aplikace projektu.</span><span class="sxs-lookup"><span data-stu-id="4da01-247">Place code files (including *.cs* and *.cshtml*) outside of the app project's web root.</span></span> <span data-ttu-id="4da01-248">Logické rozdělení se proto vytvoří mezi obsah na straně klienta a kód založený na server aplikace.</span><span class="sxs-lookup"><span data-stu-id="4da01-248">A logical separation is therefore created between the app's client-side content and server-based code.</span></span> <span data-ttu-id="4da01-249">To zabraňuje úniku kód na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="4da01-249">This prevents server-side code from being leaked.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4da01-250">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="4da01-250">Additional resources</span></span>

* [<span data-ttu-id="4da01-251">Middleware</span><span class="sxs-lookup"><span data-stu-id="4da01-251">Middleware</span></span>](xref:fundamentals/middleware/index)
* [<span data-ttu-id="4da01-252">Úvod do ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="4da01-252">Introduction to ASP.NET Core</span></span>](xref:index)
