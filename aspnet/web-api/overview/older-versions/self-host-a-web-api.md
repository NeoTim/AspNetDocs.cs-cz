---
uid: web-api/overview/older-versions/self-host-a-web-api
title: Self-Host ASP.NET Web API 1 (C#) - ASP.NET 4.x
author: MikeWasson
description: Kurz s kód ukazuje, jak hostování webového rozhraní API v konzolové aplikaci.
ms.author: riande
ms.date: 01/26/2012
ms.custom: seoapril2019
ms.assetid: be5ab1e2-4140-4275-ac59-ca82a1bac0c1
msc.legacyurl: /web-api/overview/older-versions/self-host-a-web-api
msc.type: authoredcontent
ms.openlocfilehash: 7c73bf4734f8ed8a1bf93595c0847f611ad9cc15
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59409600"
---
# <a name="self-host-aspnet-web-api-1-c"></a><span data-ttu-id="5c4e9-103">Self-Host ASP.NET Web API 1 (C#)</span><span class="sxs-lookup"><span data-stu-id="5c4e9-103">Self-Host ASP.NET Web API 1 (C#)</span></span>

<span data-ttu-id="5c4e9-104">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="5c4e9-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="5c4e9-105">Tento kurz ukazuje postupy při hostování webového rozhraní API v konzolové aplikaci.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-105">This tutorial shows how to host a web API inside a console application.</span></span> <span data-ttu-id="5c4e9-106">Rozhraní ASP.NET Web API nevyžaduje, aby služba IIS.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-106">ASP.NET Web API does not require IIS.</span></span> <span data-ttu-id="5c4e9-107">Webové rozhraní API můžete samoobslužné hostování ve vlastním procesu hostitele.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-107">You can self-host a web API in your own host process.</span></span> 
> 
> <span data-ttu-id="5c4e9-108">**Nová aplikace by měly používat OWIN k samoobslužnému hostování webového rozhraní API.**</span><span class="sxs-lookup"><span data-stu-id="5c4e9-108">**New applications should use OWIN to self-host Web API.**</span></span> <span data-ttu-id="5c4e9-109">Zobrazit [použití rozhraní OWIN k samoobslužnému hostování webového rozhraní API 2 ASP.NET](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="5c4e9-109">See [Use OWIN to Self-Host ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="5c4e9-110">V tomto kurzu použili verze softwaru</span><span class="sxs-lookup"><span data-stu-id="5c4e9-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="5c4e9-111">Webové rozhraní API 1</span><span class="sxs-lookup"><span data-stu-id="5c4e9-111">Web API 1</span></span>
> - <span data-ttu-id="5c4e9-112">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="5c4e9-112">Visual Studio 2012</span></span>


## <a name="create-the-console-application-project"></a><span data-ttu-id="5c4e9-113">Vytvořte projekt konzolové aplikace</span><span class="sxs-lookup"><span data-stu-id="5c4e9-113">Create the Console Application Project</span></span>

<span data-ttu-id="5c4e9-114">Spusťte sadu Visual Studio a vyberte **nový projekt** z **Start** stránky.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-114">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="5c4e9-115">Nebo z **souboru** nabídce vyberte možnost **nový** a potom **projektu**.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-115">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="5c4e9-116">V **šablony** vyberte **nainstalované šablony** a rozbalte **Visual C#** uzlu.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-116">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="5c4e9-117">V části **Visual C#** vyberte **Windows**.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-117">Under **Visual C#**, select **Windows**.</span></span> <span data-ttu-id="5c4e9-118">V seznamu šablon projektu vyberte **konzolovou aplikaci**.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-118">In the list of project templates, select **Console Application**.</span></span> <span data-ttu-id="5c4e9-119">Pojmenujte projekt &quot;SelfHost&quot; a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-119">Name the project &quot;SelfHost&quot; and click **OK**.</span></span>

![](self-host-a-web-api/_static/image1.png)

## <a name="set-the-target-framework-visual-studio-2010"></a><span data-ttu-id="5c4e9-120">Nastavit cílové rozhraní (Visual Studio 2010)</span><span class="sxs-lookup"><span data-stu-id="5c4e9-120">Set the Target Framework (Visual Studio 2010)</span></span>

<span data-ttu-id="5c4e9-121">Pokud používáte Visual Studio 2010, změňte cílovou architekturu na .NET Framework 4.0.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-121">If you are using Visual Studio 2010, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="5c4e9-122">(Ve výchozím nastavení šablona cíle projektu [rozhraní .net Framework Client Profile](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile).)</span><span class="sxs-lookup"><span data-stu-id="5c4e9-122">(By default, the project template targets the [.Net Framework Client Profile](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile).)</span></span>

<span data-ttu-id="5c4e9-123">V Průzkumníku řešení klikněte pravým tlačítkem myši na projekt a vyberte **vlastnosti**.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-123">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="5c4e9-124">V **Cílová architektura** rozevírací seznam, změnit cílovou architekturu na .NET Framework 4.0.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-124">In the **Target framework** dropdown list, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="5c4e9-125">Po zobrazení výzvy na použití změny, klikněte na tlačítko **Ano**.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-125">When prompted to apply the change, click **Yes**.</span></span>

![](self-host-a-web-api/_static/image2.png)

## <a name="install-nuget-package-manager"></a><span data-ttu-id="5c4e9-126">Instalace Správce balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="5c4e9-126">Install NuGet Package Manager</span></span>

<span data-ttu-id="5c4e9-127">Správce balíčků NuGet je nejjednodušší způsob, jak přidat sestavení webového rozhraní API do projektu – technologie ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-127">The NuGet Package Manager is the easiest way to add the Web API assemblies to a non-ASP.NET project.</span></span>

<span data-ttu-id="5c4e9-128">Pokud chcete zkontrolovat, jestli je nainstalovaný Správce balíčků NuGet, klikněte na tlačítko **nástroje** nabídky v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-128">To check if NuGet Package Manager is installed, click the **Tools** menu in Visual Studio.</span></span> <span data-ttu-id="5c4e9-129">Pokud se zobrazí nabídka položek volá **Správce balíčků NuGet**, pak máte Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-129">If you see a menu item called **NuGet Package Manager**, then you have NuGet Package Manager.</span></span>

<span data-ttu-id="5c4e9-130">Instalace Správce balíčků NuGet:</span><span class="sxs-lookup"><span data-stu-id="5c4e9-130">To install NuGet Package Manager:</span></span>

1. <span data-ttu-id="5c4e9-131">Spusťte Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-131">Start Visual Studio.</span></span>
2. <span data-ttu-id="5c4e9-132">Z **nástroje** nabídce vyberte možnost **rozšíření a aktualizace**.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-132">From the **Tools** menu, select **Extensions and Updates**.</span></span>
3. <span data-ttu-id="5c4e9-133">V **rozšíření a aktualizace** dialogového okna, vyberte **Online**.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-133">In the **Extensions and Updates** dialog, select **Online**.</span></span>
4. <span data-ttu-id="5c4e9-134">Pokud nevidíte "Správce balíčků NuGet", zadejte do vyhledávacího pole "Správce balíčků nuget".</span><span class="sxs-lookup"><span data-stu-id="5c4e9-134">If you don't see "NuGet Package Manager", type "nuget package manager" in the search box.</span></span>
5. <span data-ttu-id="5c4e9-135">Vyberte Správce balíčků NuGet a klikněte na tlačítko **Stáhnout**.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-135">Select the NuGet Package Manager and click **Download**.</span></span>
6. <span data-ttu-id="5c4e9-136">Až se stahování dokončí, zobrazí se výzva k instalaci.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-136">After the download completes, you will be prompted to install.</span></span>
7. <span data-ttu-id="5c4e9-137">Po dokončení instalace, vám může zobrazit výzva k restartování sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-137">After the installation completes, you might be prompted to restart Visual Studio.</span></span>

![](self-host-a-web-api/_static/image3.png)

## <a name="add-the-web-api-nuget-package"></a><span data-ttu-id="5c4e9-138">Přidat webový balíček NuGet rozhraní API</span><span class="sxs-lookup"><span data-stu-id="5c4e9-138">Add the Web API NuGet Package</span></span>

<span data-ttu-id="5c4e9-139">Po dokončení instalace Správce balíčků NuGet do projektu přidejte balíček Self-Host webové rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-139">After NuGet Package Manager is installed, add the Web API Self-Host package to your project.</span></span>

1. <span data-ttu-id="5c4e9-140">Z **nástroje** nabídce vyberte možnost **Správce balíčků NuGet**.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-140">From the **Tools** menu, select **NuGet Package Manager**.</span></span> <span data-ttu-id="5c4e9-141">*Poznámka:* Pokud se vám nezobrazí tato nabídka položek, ujistěte se, že tento správce balíčků NuGet správně nainstalován.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-141">*Note*: If do you not see this menu item, make sure that NuGet Package Manager installed correctly.</span></span>
2. <span data-ttu-id="5c4e9-142">Vyberte **spravovat balíčky NuGet pro řešení**</span><span class="sxs-lookup"><span data-stu-id="5c4e9-142">Select **Manage NuGet Packages for Solution**</span></span>
3. <span data-ttu-id="5c4e9-143">V **Správa balíčků Nuget** dialogového okna, vyberte **Online**.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-143">In the **Manage NugGet Packages** dialog, select **Online**.</span></span>
4. <span data-ttu-id="5c4e9-144">Do vyhledávacího pole zadejte &quot;Microsoft.AspNet.WebApi.SelfHost&quot;.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-144">In the search box, type &quot;Microsoft.AspNet.WebApi.SelfHost&quot;.</span></span>
5. <span data-ttu-id="5c4e9-145">Vyberte balíček ASP.NET Web API Self hostitele a klikněte na tlačítko **nainstalovat**.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-145">Select the ASP.NET Web API Self Host package and click **Install**.</span></span>
6. <span data-ttu-id="5c4e9-146">Po instalaci balíčku, klikněte na tlačítko **zavřete** zavřete dialogové okno.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-146">After the package installs, click **Close** to close the dialog.</span></span>

> [!NOTE]
> <span data-ttu-id="5c4e9-147">Ujistěte se, že k instalaci balíčku s názvem Microsoft.AspNet.WebApi.SelfHost, ne AspNetWebApi.SelfHost.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-147">Make sure to install the package named Microsoft.AspNet.WebApi.SelfHost, not AspNetWebApi.SelfHost.</span></span>

![](self-host-a-web-api/_static/image4.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="5c4e9-148">Vytvoření modelu a kontroler</span><span class="sxs-lookup"><span data-stu-id="5c4e9-148">Create the Model and Controller</span></span>

<span data-ttu-id="5c4e9-149">Tento kurz používá stejné třídy modelu a kontroler jako [Začínáme](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) kurzu.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-149">This tutorial uses the same model and controller classes as the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="5c4e9-150">Přidejte veřejnou třídu s názvem `Product`.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-150">Add a public class named `Product`.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample1.cs)]

<span data-ttu-id="5c4e9-151">Přidejte veřejnou třídu s názvem `ProductsController`.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-151">Add a public class named `ProductsController`.</span></span> <span data-ttu-id="5c4e9-152">Odvození z této třídy **System.Web.Http.ApiController**.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-152">Derive this class from **System.Web.Http.ApiController**.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample2.cs)]

<span data-ttu-id="5c4e9-153">Další informace o kódu v tomto kontroleru, najdete v článku [Začínáme](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) kurzu.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-153">For more information about the code in this controller, see the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span> <span data-ttu-id="5c4e9-154">Tento kontroler definuje tři akce GET:</span><span class="sxs-lookup"><span data-stu-id="5c4e9-154">This controller defines three GET actions:</span></span>

| <span data-ttu-id="5c4e9-155">Identifikátor URI</span><span class="sxs-lookup"><span data-stu-id="5c4e9-155">URI</span></span> | <span data-ttu-id="5c4e9-156">Popis</span><span class="sxs-lookup"><span data-stu-id="5c4e9-156">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5c4e9-157">/ api/produkty</span><span class="sxs-lookup"><span data-stu-id="5c4e9-157">/api/products</span></span> | <span data-ttu-id="5c4e9-158">Získání seznamu všech produktů.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-158">Get a list of all products.</span></span> |
| <span data-ttu-id="5c4e9-159">/ webové rozhraníAPI/produkty/*id*</span><span class="sxs-lookup"><span data-stu-id="5c4e9-159">/api/products/*id*</span></span> | <span data-ttu-id="5c4e9-160">Získání produktu podle ID.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-160">Get a product by ID.</span></span> |
| <span data-ttu-id="5c4e9-161">/api/products/?category=*category*</span><span class="sxs-lookup"><span data-stu-id="5c4e9-161">/api/products/?category=*category*</span></span> | <span data-ttu-id="5c4e9-162">Získáte seznam produktů podle kategorie.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-162">Get a list of products by category.</span></span> |

## <a name="host-the-web-api"></a><span data-ttu-id="5c4e9-163">Hostování webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="5c4e9-163">Host the Web API</span></span>

<span data-ttu-id="5c4e9-164">Otevřete soubor Program.cs a přidejte následující příkazy using:</span><span class="sxs-lookup"><span data-stu-id="5c4e9-164">Open the file Program.cs and add the following using statements:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample3.cs)]

<span data-ttu-id="5c4e9-165">Přidejte následující kód, který **Program** třídy.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-165">Add the following code to the **Program** class.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample4.cs)]

## <a name="optional-add-an-http-url-namespace-reservation"></a><span data-ttu-id="5c4e9-166">(Volitelné) Přidat rezervaci Namespace adresy URL protokolu HTTP</span><span class="sxs-lookup"><span data-stu-id="5c4e9-166">(Optional) Add an HTTP URL Namespace Reservation</span></span>

<span data-ttu-id="5c4e9-167">Tato aplikace naslouchá na `http://localhost:8080/`.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-167">This application listens to `http://localhost:8080/`.</span></span> <span data-ttu-id="5c4e9-168">Ve výchozím nastavení naslouchání na konkrétní adrese HTTP vyžaduje oprávnění správce.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-168">By default, listening at a particular HTTP address requires administrator privileges.</span></span> <span data-ttu-id="5c4e9-169">Při spuštění tohoto kurzu, proto může získat tuto chybu: "Protokol HTTP nemohl zaregistrovat adresu URL http://+:8080/" existují dva způsoby, jak se vyhnout se této chybě:</span><span class="sxs-lookup"><span data-stu-id="5c4e9-169">When you run the tutorial, therefore, you may get this error: "HTTP could not register URL http://+:8080/" There are two ways to avoid this error:</span></span>

- <span data-ttu-id="5c4e9-170">Spuštění sady Visual Studio s oprávněními zvýšenými na úroveň správce, nebo</span><span class="sxs-lookup"><span data-stu-id="5c4e9-170">Run Visual Studio with elevated administrator permissions, or</span></span>
- <span data-ttu-id="5c4e9-171">Pomocí Netsh.exe udělte vašeho účtu oprávnění k rezervaci adresy URL.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-171">Use Netsh.exe to give your account permissions to reserve the URL.</span></span>

<span data-ttu-id="5c4e9-172">Pokud chcete použít Netsh.exe, otevřete příkazový řádek s oprávněními správce a zadejte následující příkaz: následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="5c4e9-172">To use Netsh.exe, open a command prompt with administrator privileges and enter the following command:following command:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample5.cmd)]

<span data-ttu-id="5c4e9-173">kde *počítač\uživatelské_jméno* je váš uživatelský účet.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-173">where *machine\username* is your user account.</span></span>

<span data-ttu-id="5c4e9-174">Až budete hotovi s vlastním hostováním, je potřeba odstranit rezervaci:</span><span class="sxs-lookup"><span data-stu-id="5c4e9-174">When you are finished self-hosting, be sure to delete the reservation:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample6.cmd)]

## <a name="call-the-web-api-from-a-client-application-c"></a><span data-ttu-id="5c4e9-175">Volání webového rozhraní API z klientské aplikace (C#)</span><span class="sxs-lookup"><span data-stu-id="5c4e9-175">Call the Web API from a Client Application (C#)</span></span>

<span data-ttu-id="5c4e9-176">Napíšeme jednoduchou konzolovou aplikaci, která volá webové rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-176">Let's write a simple console application that calls the web API.</span></span>

<span data-ttu-id="5c4e9-177">Přidáte do řešení nový projekt konzolové aplikace:</span><span class="sxs-lookup"><span data-stu-id="5c4e9-177">Add a new console application project to the solution:</span></span>

- <span data-ttu-id="5c4e9-178">V Průzkumníku řešení klikněte pravým tlačítkem myši na řešení a vyberte **přidat nový projekt**.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-178">In Solution Explorer, right-click the solution and select **Add New Project**.</span></span>
- <span data-ttu-id="5c4e9-179">Vytvořte novou konzolovou aplikaci s názvem &quot;ClientApp&quot;.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-179">Create a new console application named &quot;ClientApp&quot;.</span></span>

![](self-host-a-web-api/_static/image5.png)

<span data-ttu-id="5c4e9-180">Použití Správce balíčků NuGet pro přidání balíčku ASP.NET Web API základní knihovny:</span><span class="sxs-lookup"><span data-stu-id="5c4e9-180">Use NuGet Package Manager to add the ASP.NET Web API Core Libraries package:</span></span>

- <span data-ttu-id="5c4e9-181">V nabídce Nástroje vyberte **Správce balíčků NuGet**.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-181">From the Tools menu, select **NuGet Package Manager**.</span></span>
- <span data-ttu-id="5c4e9-182">Vyberte **spravovat balíčky NuGet pro řešení**</span><span class="sxs-lookup"><span data-stu-id="5c4e9-182">Select **Manage NuGet Packages for Solution**</span></span>
- <span data-ttu-id="5c4e9-183">V **spravovat balíčky NuGet** dialogového okna, vyberte **Online**.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-183">In the **Manage NuGet Packages** dialog, select **Online**.</span></span>
- <span data-ttu-id="5c4e9-184">Do vyhledávacího pole zadejte &quot;Microsoft.AspNet.WebApi.Client&quot;.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-184">In the search box, type &quot;Microsoft.AspNet.WebApi.Client&quot;.</span></span>
- <span data-ttu-id="5c4e9-185">Vyberte balíček Microsoft ASP.NET Web API klientské knihovny a klikněte na tlačítko **nainstalovat**.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-185">Select the Microsoft ASP.NET Web API Client Libraries package and click **Install**.</span></span>

<span data-ttu-id="5c4e9-186">Přidáte odkaz v ClientApp do projektu hostitel ve vlastním procesu:</span><span class="sxs-lookup"><span data-stu-id="5c4e9-186">Add a reference in ClientApp to the SelfHost project:</span></span>

- <span data-ttu-id="5c4e9-187">V Průzkumníku řešení klikněte pravým tlačítkem na projekt ClientApp.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-187">In Solution Explorer, right-click the ClientApp project.</span></span>
- <span data-ttu-id="5c4e9-188">Vyberte **přidat odkaz na**.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-188">Select **Add Reference**.</span></span>
- <span data-ttu-id="5c4e9-189">V **správce odkazů** dialogového okna, v části **řešení**vyberte **projekty**.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-189">In the **Reference Manager** dialog, under **Solution**, select **Projects**.</span></span>
- <span data-ttu-id="5c4e9-190">Vyberte projekt, hostitel ve vlastním procesu.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-190">Select the SelfHost project.</span></span>
- <span data-ttu-id="5c4e9-191">Klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-191">Click **OK**.</span></span>

![](self-host-a-web-api/_static/image6.png)

<span data-ttu-id="5c4e9-192">Otevřete soubor Client/Program.cs.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-192">Open the Client/Program.cs file.</span></span> <span data-ttu-id="5c4e9-193">Přidejte následující **pomocí** – příkaz:</span><span class="sxs-lookup"><span data-stu-id="5c4e9-193">Add the following **using** statement:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample7.cs)]

<span data-ttu-id="5c4e9-194">Přidání statického **HttpClient** instance:</span><span class="sxs-lookup"><span data-stu-id="5c4e9-194">Add a static **HttpClient** instance:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample8.cs)]

<span data-ttu-id="5c4e9-195">Přidejte následující metody, které jsou uvedeny všechny produkty, seznam produktů podle ID a seznam produktů podle kategorie.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-195">Add the following methods to list all products, list a product by ID, and list products by category.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample9.cs)]

<span data-ttu-id="5c4e9-196">Každá z těchto metod používá stejný vzor:</span><span class="sxs-lookup"><span data-stu-id="5c4e9-196">Each of these methods follows the same pattern:</span></span>

1. <span data-ttu-id="5c4e9-197">Volání **HttpClient.GetAsync** odešlete požadavek GET na odpovídající identifikátor URI.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-197">Call **HttpClient.GetAsync** to send a GET request to the appropriate URI.</span></span>
2. <span data-ttu-id="5c4e9-198">Volání **HttpResponseMessage.EnsureSuccessStatusCode**.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-198">Call **HttpResponseMessage.EnsureSuccessStatusCode**.</span></span> <span data-ttu-id="5c4e9-199">Tato metoda vyvolá výjimku, pokud je stav odpovědi HTTP chybový kód.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-199">This method throws an exception if the HTTP response status is an error code.</span></span>
3. <span data-ttu-id="5c4e9-200">Volání **ReadAsAsync&lt;T&gt;**  deserializovat typ CLR z odpovědi HTTP.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-200">Call **ReadAsAsync&lt;T&gt;** to deserialize a CLR type from the HTTP response.</span></span> <span data-ttu-id="5c4e9-201">Tato metoda je metoda rozšiřující, definované v **System.Net.Http.HttpContentExtensions**.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-201">This method is an extension method, defined in **System.Net.Http.HttpContentExtensions**.</span></span>

<span data-ttu-id="5c4e9-202">**GetAsync** a **ReadAsAsync** metody jsou asynchronní.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-202">The **GetAsync** and **ReadAsAsync** methods are both asynchronous.</span></span> <span data-ttu-id="5c4e9-203">Vrátí **úloh** objekty, které představují asynchronní operace.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-203">They return **Task** objects that represent the asynchronous operation.</span></span> <span data-ttu-id="5c4e9-204">Začínáme **výsledek** vlastnost blokuje vlákno, dokud se operace dokončí.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-204">Getting the **Result** property blocks the thread until the operation completes.</span></span>

<span data-ttu-id="5c4e9-205">Další informace o používání HttpClient, včetně postupu provádění neblokující volání, naleznete v tématu [volání webového rozhraní API z klienta .NET](../advanced/calling-a-web-api-from-a-net-client.md).</span><span class="sxs-lookup"><span data-stu-id="5c4e9-205">For more information about using HttpClient, including how to make non-blocking calls, see [Calling a Web API From a .NET Client](../advanced/calling-a-web-api-from-a-net-client.md).</span></span>

<span data-ttu-id="5c4e9-206">Před voláním těchto metod, nastavte vlastnost BaseAddress nastavte na instanci HttpClient "`http://localhost:8080`".</span><span class="sxs-lookup"><span data-stu-id="5c4e9-206">Before calling these methods, set the BaseAddress property on the HttpClient instance to "`http://localhost:8080`".</span></span> <span data-ttu-id="5c4e9-207">Příklad:</span><span class="sxs-lookup"><span data-stu-id="5c4e9-207">For example:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample10.cs)]

<span data-ttu-id="5c4e9-208">To by měl výstupu následující.</span><span class="sxs-lookup"><span data-stu-id="5c4e9-208">This should output the following.</span></span> <span data-ttu-id="5c4e9-209">(Nezapomeňte nejprve spusťte aplikaci SelfHost).</span><span class="sxs-lookup"><span data-stu-id="5c4e9-209">(Remember to run the SelfHost application first.)</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample11.cmd)]

![](self-host-a-web-api/_static/image7.png)
