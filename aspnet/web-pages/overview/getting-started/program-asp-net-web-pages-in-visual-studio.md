---
uid: web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: Programování ASP.NET webových stránek (Razor) pomocí sady Visual Studio | Dokumenty společnosti Microsoft
author: Rick-Anderson
description: Tento dodatek vysvětluje, jak lze pomocí sady Visual Studio 2010 nebo Visual Web Developer 2010 Express programovat ASP.NET webových stránek pomocí syntaxe Razor.
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: e586a116fc48a797bdd40befad5851a548282ce6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542895"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a><span data-ttu-id="f1bb9-103">Programování ASP.NET webových stránek (Razor) pomocí sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f1bb9-103">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>

<span data-ttu-id="f1bb9-104">, autor: [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="f1bb9-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="f1bb9-105">Tento článek vysvětluje, jak můžete pomocí sady Visual Studio nebo Visual Web Developer Express programovat webové stránky ASP.NET webových stránek (Razor).</span><span class="sxs-lookup"><span data-stu-id="f1bb9-105">This article explains how you can use Visual Studio or Visual Web Developer Express to program ASP.NET Web Pages (Razor) websites.</span></span>
>
> <span data-ttu-id="f1bb9-106">Co se dozvíte</span><span class="sxs-lookup"><span data-stu-id="f1bb9-106">What you'll learn</span></span>
>
> - <span data-ttu-id="f1bb9-107">Co je potřeba nainstalovat (pokud vůbec něco) pro práci s ASP.NET webových stránek ve vaší verzi sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-107">What you need to install (if anything) to work with ASP.NET Web Pages in your version of Visual Studio.</span></span>
> - <span data-ttu-id="f1bb9-108">Jak přidat podporu pro ASP.NET webových stránek do Visual Web Developer 2010 Express.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-108">How to add support for ASP.NET Web Pages to Visual Web Developer 2010 Express.</span></span>
> - <span data-ttu-id="f1bb9-109">Použití funkcí v sadě Visual Studio pro práci se stránkami ASP.NET Razor, včetně technologie IntelliSense a ladicího programu.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-109">How to use features in Visual Studio to work with ASP.NET Razor pages, including IntelliSense and the debugger.</span></span>
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="f1bb9-110">Verze softwaru použité v kurzu</span><span class="sxs-lookup"><span data-stu-id="f1bb9-110">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="f1bb9-111">webové stránky ASP.NET (Břitva) 3</span><span class="sxs-lookup"><span data-stu-id="f1bb9-111">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="f1bb9-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="f1bb9-112">Visual Studio 2013</span></span>
> - <span data-ttu-id="f1bb9-113">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="f1bb9-113">WebMatrix 3</span></span>
>
>
> <span data-ttu-id="f1bb9-114">Tento kurz funguje také s ASP.NET webových stránek 2, Visual Studio 2012, Visual Studio 2010 a WebMatrix 2.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-114">This tutorial also works with ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010, and WebMatrix 2.</span></span>

<span data-ttu-id="f1bb9-115">Webové stránky můžete naprogramovat ASP.NET pomocí syntaxe Razor pomocí WebMatrix nebo mnoha dalších editorů kódu.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-115">You can program ASP.NET Web pages with Razor syntax using WebMatrix or many other code editors.</span></span> <span data-ttu-id="f1bb9-116">Můžete také použít sadu Microsoft Visual Studio, což je plně vybavené integrované vývojové prostředí (IDE), které poskytuje výkonnou sadu nástrojů pro vytváření mnoha typů aplikací (nejen webů).</span><span class="sxs-lookup"><span data-stu-id="f1bb9-116">You can also use Microsoft Visual Studio which is a full-featured integrated development environment (IDE) that provides a powerful set of tools for creating many types of applications (not just websites).</span></span> <span data-ttu-id="f1bb9-117">Chcete-li pracovat se stránkami ASP.NET Razor, můžete použít [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span><span class="sxs-lookup"><span data-stu-id="f1bb9-117">To work with ASP.NET Razor pages, you can use [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>

<span data-ttu-id="f1bb9-118">Dvě obzvláště užitečné funkce, které Visual Studio poskytuje pro programování s ASP.NET webových stránek Razor jsou:</span><span class="sxs-lookup"><span data-stu-id="f1bb9-118">Two particularly useful features that Visual Studio provides for programming with ASP.NET Razor web pages are:</span></span>

- <span data-ttu-id="f1bb9-119">*Technologie IntelliSense*.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-119">*IntelliSense*.</span></span> <span data-ttu-id="f1bb9-120">Funkce IntelliSense integrovaná do sady Visual Studio je komplexnější než technologie IntelliSense ve službě WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-120">The IntelliSense feature built into Visual Studio is more comprehensive than IntelliSense in WebMatrix.</span></span>
- <span data-ttu-id="f1bb9-121">*Ladicí program*.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-121">*Debugger*.</span></span> <span data-ttu-id="f1bb9-122">Ladicí program umožňuje řešení potíží s kódem zastavením programu při jeho spuštění, zkoumáním proměnných a krokováním kódu řádek po řádku.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-122">The debugger lets you troubleshoot your code by stopping a program while it's running, examining variables, and stepping through the code line by line.</span></span>

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a><span data-ttu-id="f1bb9-123">Použití sady Visual Studio s různými verzemi ASP.NET webových stránek</span><span class="sxs-lookup"><span data-stu-id="f1bb9-123">Using Visual Studio with Different Versions of ASP.NET Web Pages</span></span>

<span data-ttu-id="f1bb9-124">Chcete-li vyvíjet ASP.NET webových aplikací ve Visual Studiu 2017, nainstalujte **úlohu ASP.NET a vývoje webu.**</span><span class="sxs-lookup"><span data-stu-id="f1bb9-124">To develop ASP.NET web apps in Visual Studio 2017, install the **ASP.NET and web development** workload.</span></span>

<span data-ttu-id="f1bb9-125">Visual Studio 2012 a Visual Studio 2013 zahrnují podporu ASP.NET webových stránek.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-125">Visual Studio 2012 and Visual Studio 2013 include support for ASP.NET Web Pages.</span></span> <span data-ttu-id="f1bb9-126">(Balíčky, které jsou požadovány pro podporu ASP.NET webových stránek jsou nainstalovány při instalaci sady Visual Studio.)</span><span class="sxs-lookup"><span data-stu-id="f1bb9-126">(The packages that are required in order to support ASP.NET Web Pages are installed when you install Visual Studio.)</span></span>

<span data-ttu-id="f1bb9-127">Visual Studio 2010 neobsahuje podporu ve výchozím nastavení pro ASP.NET webových stránek.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-127">Visual Studio 2010 does not include support by default for ASP.NET Web Pages.</span></span> <span data-ttu-id="f1bb9-128">Chcete-li používat ASP.NET webových stránek v sadě Visual Studio 2010, je nutné nainstalovat balíček mvc ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-128">To use ASP.NET Web Pages with Visual Studio 2010, you must install the ASP.NET MVC package.</span></span> <span data-ttu-id="f1bb9-129">Chcete-li získat ASP.NET webových stránek 2, nainstalujte ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-129">To get ASP.NET Web Pages 2, you install ASP.NET MVC 4.</span></span>

<span data-ttu-id="f1bb9-130">Následující tabulka shrnuje podporu ASP.NET webových stránek v různých verzích sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-130">The following table summarizes the support for ASP.NET Web Pages in different versions of Visual Studio.</span></span>

|  | <span data-ttu-id="f1bb9-131">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="f1bb9-131">Visual Studio 2010</span></span> | <span data-ttu-id="f1bb9-132">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="f1bb9-132">Visual Studio 2012</span></span> | <span data-ttu-id="f1bb9-133">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="f1bb9-133">Visual Studio 2013</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f1bb9-134">**ASP.NET – webové stránky 2**</span><span class="sxs-lookup"><span data-stu-id="f1bb9-134">**ASP.NET Web Pages 2**</span></span> | <span data-ttu-id="f1bb9-135">Instalace ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="f1bb9-135">Install ASP.NET MVC 4</span></span> | <span data-ttu-id="f1bb9-136">(Zahrnuto)</span><span class="sxs-lookup"><span data-stu-id="f1bb9-136">(Included)</span></span> | <span data-ttu-id="f1bb9-137">(Zahrnuto)</span><span class="sxs-lookup"><span data-stu-id="f1bb9-137">(Included)</span></span> |
| <span data-ttu-id="f1bb9-138">**ASP.NET – webové stránky 3**</span><span class="sxs-lookup"><span data-stu-id="f1bb9-138">**ASP.NET Web Pages 3**</span></span> |  | <span data-ttu-id="f1bb9-139">Aktualizace na ASP.NET webových stránek 3 až NuGet</span><span class="sxs-lookup"><span data-stu-id="f1bb9-139">Update to ASP.NET Web Pages 3 through NuGet</span></span> | <span data-ttu-id="f1bb9-140">(Zahrnuto)</span><span class="sxs-lookup"><span data-stu-id="f1bb9-140">(Included)</span></span> |

<span data-ttu-id="f1bb9-141">Informace o práci s Visual Studio 2010 najdete [v tématu Instalace podpory pro ASP.NET webových stránek ve Visual Studiu 2010](#vs2010support).</span><span class="sxs-lookup"><span data-stu-id="f1bb9-141">To work with Visual Studio 2010, see [Installing Support for ASP.NET Web Pages in Visual Studio 2010](#vs2010support).</span></span>

## <a name="launching-visual-studio-from-webmatrix"></a><span data-ttu-id="f1bb9-142">Spuštění sady Visual Studio z webmatrixu</span><span class="sxs-lookup"><span data-stu-id="f1bb9-142">Launching Visual Studio from WebMatrix</span></span>

<span data-ttu-id="f1bb9-143">Pokud jste spustili projekt v WebMatrix a chcete přepnout do sady Visual Studio, WebMatrix poskytuje tlačítko pro snadné otevření projektu v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-143">If you have started a project in WebMatrix and want to switch to Visual Studio, WebMatrix provides a button to easily open the project in Visual Studio.</span></span> <span data-ttu-id="f1bb9-144">Aby bylo toto tlačítko povoleno, musí být v počítači nainstalována sada Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-144">You must have Visual Studio installed on your computer for this button to be enabled.</span></span> <span data-ttu-id="f1bb9-145">Následující obrázek znázorňuje tlačítko v WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-145">The following image shows the button in WebMatrix.</span></span>

![spuštění sady Visual Studio](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

<span data-ttu-id="f1bb9-147">Po klepnutí na tlačítko se projekt otevře v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-147">When you click the button, the project is opened in Visual Studio.</span></span> <span data-ttu-id="f1bb9-148">Můžete přepínat tam a zpět mezi WebMatrix a Visual Studio bez problémů.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-148">You can switch back and forth between WebMatrix and Visual Studio without any problems.</span></span> <span data-ttu-id="f1bb9-149">Budete upozorněni, pokud se v jiném prostředí změnily nějaké soubory a je třeba je znovu načíst, abyste získali nejnovější změny.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-149">You will be notified if any files have changed in the other environment and need to be reloaded to get the latest changes.</span></span>

## <a name="creating-aspnet-razor-site-in-visual-studio"></a><span data-ttu-id="f1bb9-150">Vytvoření webu ASP.NET Razor v sadě Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f1bb9-150">Creating ASP.NET Razor Site in Visual Studio</span></span>

<span data-ttu-id="f1bb9-151">Vytvoření webu ASP.NET Razor v sadě Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="f1bb9-151">To create an ASP.NET Razor website in Visual Studio:</span></span>

1. <span data-ttu-id="f1bb9-152">Otevřete sadu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-152">Open Visual Studio.</span></span>
2. <span data-ttu-id="f1bb9-153">V nabídce **Soubor** klepněte na **položku Nový web**.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-153">In the **File** menu, click **New Web Site**.</span></span>

    ![vytvořit nový web](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. <span data-ttu-id="f1bb9-155">V dialogovém okně **Nový web** vyberte jazyk, který chcete použít (Visual C# nebo Visual Basic).</span><span class="sxs-lookup"><span data-stu-id="f1bb9-155">In the **New Web Site** dialog box, select the language to use (Visual C# or Visual Basic).</span></span>
4. <span data-ttu-id="f1bb9-156">Vyberte šablonu **ASP.NET webu (Razor).**</span><span class="sxs-lookup"><span data-stu-id="f1bb9-156">Select the **ASP.NET Web Site (Razor)** template.</span></span>

    ![holicí strojek stránky](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. <span data-ttu-id="f1bb9-158">Klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-158">Click **OK**.</span></span>

<span data-ttu-id="f1bb9-159">Váš nový projekt existuje a je naplněn některými výchozími webovými stránkami, které vám pomohou začít.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-159">Your new project exists and is populated with some default web pages to help you get started.</span></span>

### <a name="using-intellisense"></a><span data-ttu-id="f1bb9-160">Používání atributu IntelliSense</span><span class="sxs-lookup"><span data-stu-id="f1bb9-160">Using IntelliSense</span></span>

<span data-ttu-id="f1bb9-161">Teď, když jste vytvořili web, můžete vidět, jak funguje technologie IntelliSense v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-161">Now that you've created a site, you can see how IntelliSense works in Visual Studio.</span></span>

1. <span data-ttu-id="f1bb9-162">Na právě vytvořeném webu otevřete stránku *Default.cshtml.*</span><span class="sxs-lookup"><span data-stu-id="f1bb9-162">In the website you just created, open the *Default.cshtml* page.</span></span>
2. <span data-ttu-id="f1bb9-163">Za `<h3>` značky na stránce `@ServerInfo.` zadejte (včetně tečky).</span><span class="sxs-lookup"><span data-stu-id="f1bb9-163">After the `<h3>` tags in the page, type `@ServerInfo.` (including the dot).</span></span> <span data-ttu-id="f1bb9-164">Všimněte si, jak služba IntelliSense zobrazuje dostupné metody pomocníka `ServerInfo` v rozevíracím seznamu.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-164">Notice how IntelliSense displays the available methods for the `ServerInfo` helper in a drop-down list.</span></span>

    ![Intellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. <span data-ttu-id="f1bb9-166">Vyberte `GetHtml` metodu ze seznamu a stiskněte Enter.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-166">Select the `GetHtml` method from the list and then press Enter.</span></span> <span data-ttu-id="f1bb9-167">IntelliSense automaticky vyplní metodu.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-167">IntelliSense automatically fills in the method.</span></span> <span data-ttu-id="f1bb9-168">(Stejně jako u jakékoli metody `()` v c#, musíte přidat znaky za metodu.) Vyplněný kód `GetHtml` metody vypadá jako následující příklad:</span><span class="sxs-lookup"><span data-stu-id="f1bb9-168">(As with any method in C#, you must add `()` characters after the method.) The completed code for the `GetHtml` method looks like the following example:</span></span>

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. <span data-ttu-id="f1bb9-169">Stisknutím kláves Ctrl+F5 spusťte stránku.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-169">Press Ctrl+F5 to run the page.</span></span> <span data-ttu-id="f1bb9-170">Takto vypadá stránka při zobrazení v prohlížeči:</span><span class="sxs-lookup"><span data-stu-id="f1bb9-170">This is what the page looks like when displayed in a browser:</span></span>

    ![výchozí stránka v prohlížeči](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. <span data-ttu-id="f1bb9-172">Zavřete prohlížeč.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-172">Close the browser.</span></span>

### <a name="using-the-debugger"></a><span data-ttu-id="f1bb9-173">Použití ladicího programu</span><span class="sxs-lookup"><span data-stu-id="f1bb9-173">Using the Debugger</span></span>

1. <span data-ttu-id="f1bb9-174">V horní části stránky *Default.cshtml* přidejte za `Page.Title`řádek začínající položkou následující řádek kódu:</span><span class="sxs-lookup"><span data-stu-id="f1bb9-174">At the top of the *Default.cshtml* page, after the line that begins with `Page.Title`, add the following line of code:</span></span>

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. <span data-ttu-id="f1bb9-175">V šedém okraji editoru nalevo od kódu klepněte vedle tohoto nového řádku, abyste přidali *zarážku*.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-175">In the gray margin of the editor to the left of the code, click next to this new line in order to add a *breakpoint*.</span></span> <span data-ttu-id="f1bb9-176">Zarážka je značka, která říká ladicí program zastavit spuštění programu v tomto okamžiku, takže můžete vidět, co se děje.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-176">A breakpoint is a marker that tells the debugger to stop running the program at that point so you can see what's happening.</span></span>

    ![nastavit zarážku](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. <span data-ttu-id="f1bb9-178">Odeberte volání `ServerInfo.GetHtml` metody a přidejte `@myTime` volání proměnné na jejím místě.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-178">Remove the call to the `ServerInfo.GetHtml` method, and add a call to the `@myTime` variable in its place.</span></span> <span data-ttu-id="f1bb9-179">Toto volání zobrazí aktuální časovou hodnotu, která je vrácena novým řádkem kódu.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-179">This call displays the current time value that's returned by the new line of code.</span></span>
4. <span data-ttu-id="f1bb9-180">Stisknutím klávesy F5 spusťte stránku v ladicím programu.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-180">Press F5 to run the page in the debugger.</span></span> <span data-ttu-id="f1bb9-181">Stránka se zastaví na zarážky, kterou nastavíte.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-181">The page stops on the breakpoint that you set.</span></span> <span data-ttu-id="f1bb9-182">Následující obrázek ukazuje, jak stránka vypadá v editoru s zarážkou (žlutě).</span><span class="sxs-lookup"><span data-stu-id="f1bb9-182">The following image shows what the page looks like in the editor with the breakpoint (in yellow).</span></span>

    ![ladění zarážky](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. <span data-ttu-id="f1bb9-184">Na panelu nástrojů Ladění spusťte další řádek kódu klepnutím na tlačítko **Krok do** (nebo stisknutím klávesy F11).</span><span class="sxs-lookup"><span data-stu-id="f1bb9-184">In the Debug toolbar, click the **Step Into** button (or press F11) to run the next line of code.</span></span> <span data-ttu-id="f1bb9-185">Pokaždé, když kliknete na toto tlačítko, přejdete spuštění na další řádek kódu.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-185">Each time you click this button, you advance the execution to the next line of code.</span></span>

    ![Tlačítko Krok do](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. <span data-ttu-id="f1bb9-187">Zkontrolujte hodnotu `myTime` proměnné podržením ukazatele myši nad ním nebo kontrolou hodnoty zobrazené v **locals** a **zásobníku volání** okna.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-187">Examine the value of the `myTime` variable by holding your mouse pointer over it or by inspecting the values displayed in the **Locals** and **Call Stack** windows.</span></span> <span data-ttu-id="f1bb9-188">Visual Studio zobrazit hodnotu proměnné.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-188">Visual Studio display the value of the variable.</span></span>

    ![zobrazit hodnotu času](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. <span data-ttu-id="f1bb9-190">Po dokončení zkoumání proměnné a krokování kódu, stiskněte klávesu F5 pokračovat v běhu stránky bez zastavení na každém řádku.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-190">When you're done examining the variable and stepping through code, press F5 to continue running the page without stopping at each line.</span></span> <span data-ttu-id="f1bb9-191">Po dokončení krokování přes všechny kód, prohlížeč zobrazí stránku.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-191">When you've finished stepping through all the code, the browser displays the page.</span></span>

<span data-ttu-id="f1bb9-192">Další informace o ladicím programu a o ladění kódu v sadě Visual Studio naleznete v [tématu Návod: Ladění webových stránek v aplikaci Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1bb9-192">To learn more about the debugger and about how to debug code in Visual Studio, see [Walkthrough: Debugging Web Pages in Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span></span>

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a><span data-ttu-id="f1bb9-193">Použití razor v ASP.NET mvc projekty s Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f1bb9-193">Using Razor in ASP.NET MVC projects with Visual Studio</span></span>

<span data-ttu-id="f1bb9-194">Syntaxe Razor se také široce používá v ASP.NET projektech MVC.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-194">The Razor syntax is also used extensively in ASP.NET MVC projects.</span></span> <span data-ttu-id="f1bb9-195">MVC je výkonný způsob vytváření dynamických webových stránek založený na vzorcích.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-195">MVC is a powerful, patterns-based way to build dynamic websites.</span></span> <span data-ttu-id="f1bb9-196">Pokud je obtížné udržovat web ASP.NET webových stránek, můžete zvážit jeho převod na ASP.NET aplikaci MVC.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-196">If your ASP.NET Web Pages site becomes difficult to maintain, you might want to consider converting it to an ASP.NET MVC application.</span></span> <span data-ttu-id="f1bb9-197">Příklad vytvoření aplikace MVC naleznete v tématu [Začínáme s ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="f1bb9-197">For an example of creating an MVC application, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a><span data-ttu-id="f1bb9-198">Instalace podpory pro ASP.NET webových stránek v sadě Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="f1bb9-198">Installing Support for ASP.NET Web Pages in Visual Studio 2010</span></span>

<span data-ttu-id="f1bb9-199">Tato část ukazuje, jak nainstalovat aplikaci Visual Web Developer Express 2010 a nástroje ASP.NET webových stránek pro aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-199">This section shows how to install Visual Web Developer Express 2010 and the ASP.NET Web Pages Tools for Visual Studio.</span></span>

1. <span data-ttu-id="f1bb9-200">Pokud ještě nemáte Instalační službu webové platformy, stáhněte si ji z následující adresy URL:</span><span class="sxs-lookup"><span data-stu-id="f1bb9-200">If you don't already have the Web Platform Installer, download it from the following URL:</span></span>

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. <span data-ttu-id="f1bb9-201">Spusťte Instalační službu webové platformy.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-201">Run the Web Platform Installer.</span></span>
3. <span data-ttu-id="f1bb9-202">Klikněte na kartu **Produkty.**</span><span class="sxs-lookup"><span data-stu-id="f1bb9-202">Click the **Products** tab.</span></span>

    ![Karta Produkty WebPI](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. <span data-ttu-id="f1bb9-204">Vyhledejte **ASP.NET MVC 4** (pro ASP.NET webových stránek 2) a klepněte na tlačítko **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-204">Search for **ASP.NET MVC 4** (for ASP.NET Web Pages 2) and then click **Add**.</span></span> <span data-ttu-id="f1bb9-205">Mezi tyto produkty patří nástroje visual studio pro vytváření ASP.NET weby Razor.</span><span class="sxs-lookup"><span data-stu-id="f1bb9-205">These products include Visual Studio tools for building ASP.NET Razor websites.</span></span>

    ![Možnosti instalace webpi](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. <span data-ttu-id="f1bb9-207">Chcete-li dokončit instalaci, klepněte na tlačítko **Nainstalovat.**</span><span class="sxs-lookup"><span data-stu-id="f1bb9-207">Click **Install** to complete the installation.</span></span>
