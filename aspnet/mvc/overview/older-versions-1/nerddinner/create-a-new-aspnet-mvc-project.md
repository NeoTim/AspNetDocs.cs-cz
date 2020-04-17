---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: Vytvoření nového projektu ASP.NET MVC | Dokumenty společnosti Microsoft
author: rick-anderson
description: Krok 1 ukazuje, jak umístit základní strukturu aplikace NerdDinner na místě.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 240c8a04cec3c07f434182775d1c519aab029761
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541478"
---
# <a name="create-a-new-aspnet-mvc-project"></a>Vytvoření nového projektu ASP.NET MVC

podle [společnosti Microsoft](https://github.com/microsoft)

[Stáhnout PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Toto je krok 1 zdarma ["NerdDinner" aplikační kurz,](introducing-the-nerddinner-tutorial.md) který prochází, jak vytvořit malé, ale kompletní, webové aplikace pomocí ASP.NET MVC 1.
> 
> Krok 1 ukazuje, jak umístit základní strukturu aplikace NerdDinner na místě.
> 
> Pokud používáte ASP.NET MVC 3, doporučujeme postupovat podle kurzů [Začínáme s MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) nebo [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)

## <a name="nerddinner-step-1-file-gtnew-project"></a>NerdDinner Krok 1:&gt;Soubor- Nový projekt

Začneme naše aplikace NerdDinner výběrem **file-new&gt;project** položky nabídky v rámci aplikace Visual Studio 2008 nebo zdarma Visual Web Developer 2008 Express.

Tím se zobrazí dialogové okno Nový projekt. Chcete-li vytvořit novou aplikaci ASP.NET MVC, vybereme uzel "Web" na levé straně dialogového okna a pak zvolíme šablonu projektu "ASP.NET MVC Web Application" vpravo:

![](create-a-new-aspnet-mvc-project/_static/image1.png)

*Důležité: Ujistěte se, že jste stáhli a nainstalovali ASP.NET MVC - jinak se nezobrazí v dialogovém okně Nový projekt. V2 Instalační služby [webové platformy Společnosti Microsoft](https://www.microsoft.com/web/downloads/platform.aspx) můžete použít, pokud jste jej ještě nenainstalovali&gt;(ASP.NET MVC je k dispozici v části "Rozhraní webové platformy a runtimes").*

Pojmenujeme nový projekt, který vytvoříme "NerdDinner" a poté jej vytvoříte kliknutím na tlačítko "ok".

Po kliknutí na tlačítko "ok" Visual Studio vyvolá další dialogové okno, které nás vyzve k volitelně vytvořit projekt testování částí pro novou aplikaci také. Tento projekt testování částí nám umožňuje vytvářet automatizované testy, které ověřují funkčnost a chování naší aplikace (něco, co budeme pokrývat, jak to udělat později v tomto kurzu).

![](create-a-new-aspnet-mvc-project/_static/image2.png)

Rozbalovací seznam "Test Framework" ve výše uvedeném dialogovém okně je naplněn všemi dostupnými ASP.NET šablonprojektů projektu testování částí MVC nainstalovaných v počítači. Verze lze stáhnout pro NUnit, MBUnit a XUnit. Integrované visual studio testování jednotky rozhraní je také podporována.

*Poznámka: Visual Studio Unit Test Framework je k dispozici pouze s Visual Studio 2008 Professional a vyšší verze. Pokud používáte vs 2008 Standard Edition nebo Visual Web Developer 2008 Express, budete muset stáhnout a nainstalovat nunit, MBUnit nebo XUnit rozšíření pro ASP.NET MVC, aby se toto dialogové okno zobrazí. Dialogové okno se nezobrazí, pokud nejsou nainstalovány žádné testovací architektury.*

Použijeme výchozí název "NerdDinner.Tests" pro testovací projekt, který vytvoříme, a použijeme možnost rozhraní "Visual Studio Unit Test". Po kliknutí na tlačítko "ok" Visual Studio vytvoří řešení pro nás se dvěma projekty v něm - jeden pro naši webovou aplikaci a jeden pro naše testování částí:

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a>Zkoumání struktury adresáře NerdDinner

Když vytvoříte novou aplikaci ASP.NET MVC pomocí sady Visual Studio, automaticky přidá do projektu několik souborů a adresářů:

![](create-a-new-aspnet-mvc-project/_static/image4.png)

ASP.NET projekty MVC mají ve výchozím nastavení šest adresářů nejvyšší úrovně:

| **Adresář** | **Účel** |
| --- | --- |
| **/Kontrolory** | Kde umístit Controller třídy, které zpracovávají požadavky URL |
| **/Modely** | Kam umístit třídy, které představují a manipulovat s daty |
| **/Zobrazení** | Kam umístit soubory šablon uživatelského počítače, které jsou zodpovědné za vykreslování výstupu |
| **/Skripty** | Kam vložíte soubory a skripty knihovny JavaScriptu (.js) |
| **/Obsah** | Kam vložíte CSS a obrazové soubory a další nedynamický/nejavascriptový obsah |
| **/Data\_aplikace** | Kde ukládáte datové soubory, které chcete číst/zapisovat. |

ASP.NET MVC tuto strukturu nevyžaduje. Ve skutečnosti vývojáři pracující na velkých aplikacích obvykle rozdělí aplikaci na příčku více projektů, aby byla lépe zvládnutelná (například: třídy datového modelu často přejdou do projektu samostatné knihovny tříd z webové aplikace). Výchozí struktura projektu však poskytuje pěknou výchozí konvenci adresářů, kterou můžeme použít k udržení našich aplikací v čistotě.

Když rozbalíme adresář /Controllers, zjistíme, že Visual Studio přidalo do projektu ve výchozím nastavení dvě třídy řadiče – HomeController a AccountController:

![](create-a-new-aspnet-mvc-project/_static/image5.png)

Když rozbalíme adresář /Views, najdeme tři podadresáře – /Home, /Account a /Shared – a ve výchozím nastavení byly do projektu přidány také několik souborů šablon:

![](create-a-new-aspnet-mvc-project/_static/image6.png)

Když jsme se rozbalit / Obsah a / Skripty adresáře, najdeme Site.css soubor, který se používá k stylu všech HTML na webu, stejně jako JavaScript knihovny, které mohou povolit ASP.NET AJAX a jQuery podporu v rámci aplikace:

![](create-a-new-aspnet-mvc-project/_static/image7.png)

Když jsme se rozšířit NerdDinner.Tests projektu najdeme dvě třídy, které obsahují testy částí pro naše třídy kontroleru:

![](create-a-new-aspnet-mvc-project/_static/image8.png)

Tyto výchozí soubory přidané visual studio nám poskytují základní strukturu pro pracovní aplikaci - kompletní s domovskou stránkou, o stránce, přihlašovacími / odhlašovacími / registračními stránkami účtu a neošetřenou chybovou stránkou (všechny kabelové a pracující po vybalení z krabice).

### <a name="running-the-nerddinner-application"></a>Spuštění aplikace NerdDinner

Projekt můžeme spustit výběrem **ladicího systému-&gt;Start Ladění** nebo **Ladění-&gt;Start bez ladění** položek nabídky:

![](create-a-new-aspnet-mvc-project/_static/image9.png)

Tím se spustí předdefinovaný ASP.NET webový server, který je dodáván s Visual Studio, a spustí te naši aplikaci:

![](create-a-new-aspnet-mvc-project/_static/image10.png)

Níže je domovská stránka pro náš nový projekt (URL: "/"), když běží:

![](create-a-new-aspnet-mvc-project/_static/image11.png)

Kliknutím na kartu "O aplikaci" se zobrazí ostránce (URL: "/Home/About"):

![](create-a-new-aspnet-mvc-project/_static/image12.png)

Kliknutím na odkaz "Přihlásit se" vpravo nahoře nás přeneseme na přihlašovací stránku (URL: "/Account/LogOn")

![](create-a-new-aspnet-mvc-project/_static/image13.png)

Pokud nemáme přihlašovací účet, můžeme kliknout na odkaz registru (URL: "/Account/Register") a vytvořit si ho:

![](create-a-new-aspnet-mvc-project/_static/image14.png)

Kód pro implementaci výše uvedené funkce domů, o aplikaci a odhlášení / registrace byl přidán ve výchozím nastavení, když jsme vytvořili náš nový projekt. Použijeme ji jako výchozí bod naší aplikace.

### <a name="testing-the-nerddinner-application"></a>Testování aplikace NerdDinner

Pokud používáme Professional Edition nebo vyšší verzi sady Visual Studio 2008, můžeme použít integrovanou podporu testování částí IDE v rámci sady Visual Studio k testování projektu:

![](create-a-new-aspnet-mvc-project/_static/image15.png)

Výběrem jedné z výše uvedených možností se otevře podokno "Výsledky testů" v rámci integrovaného rozhraní IDE a poskytnete nám stav vyhovění/selhání v testech 27 jednotek zahrnutých v našem novém projektu, které pokrývají vestavěné funkce:

![](create-a-new-aspnet-mvc-project/_static/image16.png)

Později v tomto kurzu budeme hovořit více o automatizované testování a přidat další testy částí, které pokrývají funkce aplikace, které implementujeme.

### <a name="next-step"></a>Další krok

Nyní máme základní strukturu aplikací na místě. Nyní [vytvoříme databázi pro ukládání dat našich aplikací](create-a-database.md).

> [!div class="step-by-step"]
> [Předchozí](introducing-the-nerddinner-tutorial.md)
> [další](create-a-database.md)
