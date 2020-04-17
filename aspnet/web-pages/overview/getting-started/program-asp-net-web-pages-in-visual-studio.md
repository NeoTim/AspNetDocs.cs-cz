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
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a>Programování ASP.NET webových stránek (Razor) pomocí sady Visual Studio

, autor: [Tom FitzMacken](https://github.com/tfitzmac)

> Tento článek vysvětluje, jak můžete pomocí sady Visual Studio nebo Visual Web Developer Express programovat webové stránky ASP.NET webových stránek (Razor).
>
> Co se dozvíte
>
> - Co je potřeba nainstalovat (pokud vůbec něco) pro práci s ASP.NET webových stránek ve vaší verzi sady Visual Studio.
> - Jak přidat podporu pro ASP.NET webových stránek do Visual Web Developer 2010 Express.
> - Použití funkcí v sadě Visual Studio pro práci se stránkami ASP.NET Razor, včetně technologie IntelliSense a ladicího programu.
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v kurzu
>
>
> - webové stránky ASP.NET (Břitva) 3
> - Visual Studio 2013
> - WebMatrix 3
>
>
> Tento kurz funguje také s ASP.NET webových stránek 2, Visual Studio 2012, Visual Studio 2010 a WebMatrix 2.

Webové stránky můžete naprogramovat ASP.NET pomocí syntaxe Razor pomocí WebMatrix nebo mnoha dalších editorů kódu. Můžete také použít sadu Microsoft Visual Studio, což je plně vybavené integrované vývojové prostředí (IDE), které poskytuje výkonnou sadu nástrojů pro vytváření mnoha typů aplikací (nejen webů). Chcete-li pracovat se stránkami ASP.NET Razor, můžete použít [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).

Dvě obzvláště užitečné funkce, které Visual Studio poskytuje pro programování s ASP.NET webových stránek Razor jsou:

- *Technologie IntelliSense*. Funkce IntelliSense integrovaná do sady Visual Studio je komplexnější než technologie IntelliSense ve službě WebMatrix.
- *Ladicí program*. Ladicí program umožňuje řešení potíží s kódem zastavením programu při jeho spuštění, zkoumáním proměnných a krokováním kódu řádek po řádku.

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a>Použití sady Visual Studio s různými verzemi ASP.NET webových stránek

Chcete-li vyvíjet ASP.NET webových aplikací ve Visual Studiu 2017, nainstalujte **úlohu ASP.NET a vývoje webu.**

Visual Studio 2012 a Visual Studio 2013 zahrnují podporu ASP.NET webových stránek. (Balíčky, které jsou požadovány pro podporu ASP.NET webových stránek jsou nainstalovány při instalaci sady Visual Studio.)

Visual Studio 2010 neobsahuje podporu ve výchozím nastavení pro ASP.NET webových stránek. Chcete-li používat ASP.NET webových stránek v sadě Visual Studio 2010, je nutné nainstalovat balíček mvc ASP.NET. Chcete-li získat ASP.NET webových stránek 2, nainstalujte ASP.NET MVC 4.

Následující tabulka shrnuje podporu ASP.NET webových stránek v různých verzích sady Visual Studio.

|  | Visual Studio 2010 | Visual Studio 2012 | Visual Studio 2013 |
| --- | --- | --- | --- |
| **ASP.NET – webové stránky 2** | Instalace ASP.NET MVC 4 | (Zahrnuto) | (Zahrnuto) |
| **ASP.NET – webové stránky 3** |  | Aktualizace na ASP.NET webových stránek 3 až NuGet | (Zahrnuto) |

Informace o práci s Visual Studio 2010 najdete [v tématu Instalace podpory pro ASP.NET webových stránek ve Visual Studiu 2010](#vs2010support).

## <a name="launching-visual-studio-from-webmatrix"></a>Spuštění sady Visual Studio z webmatrixu

Pokud jste spustili projekt v WebMatrix a chcete přepnout do sady Visual Studio, WebMatrix poskytuje tlačítko pro snadné otevření projektu v sadě Visual Studio. Aby bylo toto tlačítko povoleno, musí být v počítači nainstalována sada Visual Studio. Následující obrázek znázorňuje tlačítko v WebMatrix.

![spuštění sady Visual Studio](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

Po klepnutí na tlačítko se projekt otevře v sadě Visual Studio. Můžete přepínat tam a zpět mezi WebMatrix a Visual Studio bez problémů. Budete upozorněni, pokud se v jiném prostředí změnily nějaké soubory a je třeba je znovu načíst, abyste získali nejnovější změny.

## <a name="creating-aspnet-razor-site-in-visual-studio"></a>Vytvoření webu ASP.NET Razor v sadě Visual Studio

Vytvoření webu ASP.NET Razor v sadě Visual Studio:

1. Otevřete sadu Visual Studio.
2. V nabídce **Soubor** klepněte na **položku Nový web**.

    ![vytvořit nový web](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. V dialogovém okně **Nový web** vyberte jazyk, který chcete použít (Visual C# nebo Visual Basic).
4. Vyberte šablonu **ASP.NET webu (Razor).**

    ![holicí strojek stránky](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. Klikněte na tlačítko **OK**.

Váš nový projekt existuje a je naplněn některými výchozími webovými stránkami, které vám pomohou začít.

### <a name="using-intellisense"></a>Používání atributu IntelliSense

Teď, když jste vytvořili web, můžete vidět, jak funguje technologie IntelliSense v sadě Visual Studio.

1. Na právě vytvořeném webu otevřete stránku *Default.cshtml.*
2. Za `<h3>` značky na stránce `@ServerInfo.` zadejte (včetně tečky). Všimněte si, jak služba IntelliSense zobrazuje dostupné metody pomocníka `ServerInfo` v rozevíracím seznamu.

    ![Intellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. Vyberte `GetHtml` metodu ze seznamu a stiskněte Enter. IntelliSense automaticky vyplní metodu. (Stejně jako u jakékoli metody `()` v c#, musíte přidat znaky za metodu.) Vyplněný kód `GetHtml` metody vypadá jako následující příklad:

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. Stisknutím kláves Ctrl+F5 spusťte stránku. Takto vypadá stránka při zobrazení v prohlížeči:

    ![výchozí stránka v prohlížeči](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. Zavřete prohlížeč.

### <a name="using-the-debugger"></a>Použití ladicího programu

1. V horní části stránky *Default.cshtml* přidejte za `Page.Title`řádek začínající položkou následující řádek kódu:

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. V šedém okraji editoru nalevo od kódu klepněte vedle tohoto nového řádku, abyste přidali *zarážku*. Zarážka je značka, která říká ladicí program zastavit spuštění programu v tomto okamžiku, takže můžete vidět, co se děje.

    ![nastavit zarážku](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. Odeberte volání `ServerInfo.GetHtml` metody a přidejte `@myTime` volání proměnné na jejím místě. Toto volání zobrazí aktuální časovou hodnotu, která je vrácena novým řádkem kódu.
4. Stisknutím klávesy F5 spusťte stránku v ladicím programu. Stránka se zastaví na zarážky, kterou nastavíte. Následující obrázek ukazuje, jak stránka vypadá v editoru s zarážkou (žlutě).

    ![ladění zarážky](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. Na panelu nástrojů Ladění spusťte další řádek kódu klepnutím na tlačítko **Krok do** (nebo stisknutím klávesy F11). Pokaždé, když kliknete na toto tlačítko, přejdete spuštění na další řádek kódu.

    ![Tlačítko Krok do](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. Zkontrolujte hodnotu `myTime` proměnné podržením ukazatele myši nad ním nebo kontrolou hodnoty zobrazené v **locals** a **zásobníku volání** okna. Visual Studio zobrazit hodnotu proměnné.

    ![zobrazit hodnotu času](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. Po dokončení zkoumání proměnné a krokování kódu, stiskněte klávesu F5 pokračovat v běhu stránky bez zastavení na každém řádku. Po dokončení krokování přes všechny kód, prohlížeč zobrazí stránku.

Další informace o ladicím programu a o ladění kódu v sadě Visual Studio naleznete v [tématu Návod: Ladění webových stránek v aplikaci Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a>Použití razor v ASP.NET mvc projekty s Visual Studio

Syntaxe Razor se také široce používá v ASP.NET projektech MVC. MVC je výkonný způsob vytváření dynamických webových stránek založený na vzorcích. Pokud je obtížné udržovat web ASP.NET webových stránek, můžete zvážit jeho převod na ASP.NET aplikaci MVC. Příklad vytvoření aplikace MVC naleznete v tématu [Začínáme s ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a>Instalace podpory pro ASP.NET webových stránek v sadě Visual Studio 2010

Tato část ukazuje, jak nainstalovat aplikaci Visual Web Developer Express 2010 a nástroje ASP.NET webových stránek pro aplikaci Visual Studio.

1. Pokud ještě nemáte Instalační službu webové platformy, stáhněte si ji z následující adresy URL:

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. Spusťte Instalační službu webové platformy.
3. Klikněte na kartu **Produkty.**

    ![Karta Produkty WebPI](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. Vyhledejte **ASP.NET MVC 4** (pro ASP.NET webových stránek 2) a klepněte na tlačítko **Přidat**. Mezi tyto produkty patří nástroje visual studio pro vytváření ASP.NET weby Razor.

    ![Možnosti instalace webpi](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. Chcete-li dokončit instalaci, klepněte na tlačítko **Nainstalovat.**
