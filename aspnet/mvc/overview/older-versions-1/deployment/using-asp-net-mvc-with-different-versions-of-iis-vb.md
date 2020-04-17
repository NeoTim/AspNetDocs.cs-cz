---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
title: Použití ASP.NET MVC s různými verzemi služby IIS (VB) | Dokumenty společnosti Microsoft
author: rick-anderson
description: V tomto kurzu se dozvíte, jak používat ASP.NET MVC a směrování adres URL s různými verzemi Internetové informační služby. Naučíte se různé strategie...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 1c1283b2-6956-4937-b568-d30de432ce23
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
msc.type: authoredcontent
ms.openlocfilehash: 5e04ae14026e6d5dd1e603be6c52ff6876a468cf
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541998"
---
# <a name="using-aspnet-mvc-with-different-versions-of-iis-vb"></a>Použití ASP.NET MVC s různými verzemi služby IIS (VB)

podle [společnosti Microsoft](https://github.com/microsoft)

> V tomto kurzu se dozvíte, jak používat ASP.NET MVC a směrování adres URL s různými verzemi Internetové informační služby. Naučíte se různé strategie pro použití ASP.NET MVC se službou IIS 7.0 (klasický režim), službou IIS 6.0 a staršími verzemi služby IIS.

Rozhraní ASP.NET MVC závisí na ASP.NET směrování požadavků prohlížeče na akce řadiče. Chcete-li využít výhod ASP.NET směrování, bude pravděpodobně pravděpodobně muset provést další kroky konfigurace na webovém serveru. Vše závisí na verzi Internetové informační služby (IIS) a na režimu zpracování požadavků pro vaši aplikaci.

Zde je přehled různých verzí iis:

- Služba IIS 7.0 (integrovaný režim) – k použití ASP.NET směrování není nutná žádná zvláštní konfigurace.
- Služba IIS 7.0 (klasický režim) – chcete-li použít ASP.NET směrování, je třeba provést speciální konfiguraci.
- Služba IIS 6.0 nebo nižší – chcete-li použít ASP.NET směrování, je třeba provést speciální konfiguraci.

Nejnovější verze iis je verze 7.5 (na Win7). Služba IIS 7 služby IIS je součástí systému Windows Server 2008 a VISTA/SP1 a vyšší. Službu IIS 7.0 můžete také nainstalovat do libovolné verze [https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)operačního systému Vista s výjimkou jazyka Home Basic (viz ).

IIS 7.0 podporuje dva režimy pro zpracování požadavků. Můžete použít integrovaný režim nebo klasický režim. Při používání služby IIS 7.0 v integrovaném režimu není nutné provádět žádné speciální kroky konfigurace. Při použití služby IIS 7.0 v klasickém režimu je však nutné provést další konfiguraci.

Systém Microsoft Windows Server 2003 obsahuje službu IIS 6.0. Při použití operačního systému Windows Server 2003 nelze inovovat službu IIS 6.0 na službu IIS 7.0. Při používání služby IIS 6.0 je nutné provést další kroky konfigurace.

Systém Microsoft Windows XP Professional obsahuje službu IIS 5.1. Při používání služby IIS 5.1 je nutné provést další kroky konfigurace.

Konečně, Microsoft Windows 2000 a Microsoft Windows 2000 Professional obsahuje IIS 5.0. Při používání služby IIS 5.0 je nutné provést další kroky konfigurace.

## <a name="integrated-versus-classic-mode"></a>Integrovaný versus klasický režim

IIS 7.0 může zpracovávat požadavky pomocí dvou různých režimů zpracování požadavků: integrované a klasické. Integrovaný režim poskytuje lepší výkon a více funkcí. Klasický režim je součástí zpětné kompatibility s dřívějšími verzemi iis.

Režim zpracování požadavku je určen fondem aplikací. Můžete určit, který režim zpracování je používán konkrétní webové aplikace určením fondu aplikací přidružené k aplikaci. Postupujte následovně:

1. Spuštění Správce internetové informační služby
2. V okně Připojení vyberte aplikaci.
3. V okně Akce kliknutím na odkaz **Základní nastavení** otevřete dialogové okno Upravit aplikaci (viz obrázek 1).
4. Poznamenejte si vybraný fond aplikací.

Ve výchozím nastavení je služba IIS nakonfigurována tak, aby podporovala dva fondy aplikací: **DefaultAppPool** a **Classic .NET AppPool**. Pokud je vybrán DefaultAppPool, pak je aplikace spuštěna v režimu integrovaného zpracování požadavků. Pokud je vybrán klasický .NET AppPool, vaše aplikace běží v klasickém režimu zpracování požadavků.

[![Dialogové okno New Project (Nový projekt)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.png)

**Obrázek 1**: Detekce režimu zpracování[požadavku(Kliknutím zobrazíte obrázek v plné velikosti)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.png)

Všimněte si, že můžete upravit režim zpracování požadavku v dialogovém okně Upravit aplikaci. Klikněte na tlačítko Vybrat a změňte fond aplikací přidružený k aplikaci. Uvědomte si, že existují problémy s kompatibilitou při změně ASP.NET aplikace z klasického do integrovaného režimu. Další informace najdete v těchto článcích:

- Inovace ASP.NET 1.1 na službu IIS 7.0 v systémech Windows Vista a Windows Server 2008 --[https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)

- ASP.NET integrace se sišárnou 7.0 -[https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)

Pokud ASP.NET aplikace používá DefaultAppPool, pak není nutné provádět žádné další kroky, aby se ASP.NET Směrování (a proto ASP.NET MVC) do práce. Pokud je však aplikace ASP.NET nakonfigurována pro použití klasického fondu .NET AppPool, pak pokračujte ve čtení, máte více práce.

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a>Použití ASP.NET MVC se staršími verzemi služby IIS

Pokud potřebujete používat ASP.NET MVC se starší verzí iis než iIS 7.0 nebo potřebujete použít iIS 7.0 v klasickém režimu, máte dvě možnosti. Nejprve můžete upravit směrovací tabulku tak, aby používala přípony souborů. Například místo vyžádání adresy URL jako /Store/Details byste například požadovali adresu URL jako /Store.aspx/Details.

Druhou možností je vytvořit něco, čemu se říká *mapa skriptů se zástupnými symboly*. Mapa skriptů se zástupnými symboly umožňuje mapovat každý požadavek do ASP.NET rámci.

Pokud nemáte přístup k webovému serveru (například vaše ASP.NET aplikace MVC je hostována poskytovatelem internetových služeb), budete muset použít první možnost. Pokud nechcete měnit vzhled adres URL a máte přístup k webovému serveru, můžete použít druhou možnost.

Každou možnost podrobně zkoumáme v následujících částech.

## <a name="adding-extensions-to-the-route-table"></a>Přidání rozšíření do směrovací tabulky

Nejjednodušší způsob, jak získat ASP.NET směrování pro práci se staršími verzemi služby IIS, je upravit trasovací tabulku v souboru Global.asax. Výchozí a nezměněný soubor Global.asax v seznamu 1 konfiguruje jednu trasu s názvem Výchozí trasa.

**Výpis 1 - Global.asax (beze změny)**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample1.vb)]

Výchozí trasa nakonfigurovaná v seznamu 1 umožňuje směrovat adresy URL, které vypadají takto:

/Domů/Index

/Produkt/Podrobnosti/3

/Produkt

Starší verze služby IIS bohužel tyto požadavky nepředají do ASP.NET rámci. Proto tyto požadavky nebudou přesměrovány na řadič. Pokud například provedete požadavek prohlížeče na adresu URL /Home/Index, zobrazí se chybová stránka na obrázku 2.

[![Dialogové okno New Project (Nový projekt)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.png)

**Obrázek 2**: Příjem chyby 404 Not Found[(Kliknutím zobrazíte obrázek v plné velikosti)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.png)

Starší verze služby IIS mapují pouze určité požadavky na ASP.NET rámci. Požadavek musí být pro adresu URL se správnou příponou souboru. Například požadavek /SomePage.aspx získá namapovány na ASP.NET rámci. Požadavek na soubor /SomePage.htm však není.

Proto získat ASP.NET Směrování do práce, musíme upravit výchozí trasu tak, aby obsahuje příponu souboru, který je mapován na ASP.NET rámci.

To se provádí pomocí `registermvc.wsf`skriptu s názvem . To bylo součástí ASP.NET Vydání MVC 1 v `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`, ale od ASP.NET 2 tento [http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978)skript byl přesunut do ASP.NET Futures, k dispozici na .

Spuštění tohoto skriptu registruje nové rozšíření MVC se službou IIS. Po registraci přípony MVC můžete upravit trasy v souboru Global.asax tak, aby trasy používaly příponu MVC.

Upravený soubor Global.asax v seznamu 2 pracuje se staršími verzemi iis.

**Výpis 2 - Global.asax (upraveno s rozšířeními)**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample2.vb)]

Důležité: nezapomeňte znovu vytvořit ASP.NET aplikaci MVC po změně souboru Global.asax.

V seznamu 2 jsou v seznamu 2 dvě důležité změny souboru Global.asax. V souboru Global.asax jsou nyní definovány dvě trasy. Vzor adresy URL pro výchozí trasu, první trasu, nyní vypadá takto:

{controller}.mvc/{action}/{id}

Přidání přípony MVC změní typ souborů, které modul ASP.NET Routing zachytí. S touto změnou aplikace ASP.NET MVC nyní směruje požadavky takto:

/Úvod.mvc/Index/

/Product.mvc/Details/3

/Product.mvc/

Druhá trasa, Kořenová trasa, je nová. Tento vzor adresy URL pro kořenovou trasu je prázdný řetězec. Tato trasa je nezbytná pro odpovídající požadavky provedené proti kořenové aplikace. Kořenová trasa bude například odpovídat požadavku, který vypadá takto:

[http://www.YourApplication.com/](http://www.YourApplication.com/)

Po provedení těchto úprav směrovací tabulky se budete muset ujistit, že všechny odkazy v aplikaci jsou kompatibilní s těmito novými vzory adres URL. Jinými slovy, ujistěte se, že všechny odkazy obsahují rozšíření MVC. Pokud ke generování odkazů použijete pomocnou metodu Html.ActionLink(), neměli byste provádět žádné změny.

Namísto použití skriptu registermvc.wcf můžete do služby IIS přidat nové rozšíření, které je ručně mapováno na rozhraní ASP.NET. Při přidávání nové ho rozšíření sami zkontrolujte, zda není zaškrtnuto políčko **Ověřit, zda soubor existuje.**

## <a name="hosted-server"></a>Hostovaný server

Ne vždy máte přístup k webovému serveru. Pokud například hostujete aplikaci ASP.NET MVC pomocí poskytovatele internetového hostingu, nebudete mít nutně přístup ke službě IIS.

V takovém případě byste měli použít jednu z existujících přípon souborů, které jsou mapovány na ASP.NET rámci. Mezi přípony souborů mapované na ASP.NET patří přípony ASPX, AXD a ASHX.

Například upravený soubor Global.asax v listingu 3 používá místo přípony MVC příponu ASPX.

**Výpis 3 - Global.asax (upraveno s .aspx rozšíření)**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample3.vb)]

Soubor Global.asax v seznamu 3 je přesně stejný jako předchozí soubor Global.asax s výjimkou skutečnosti, že používá příponu ASPX namísto přípony MVC. Chcete-li použít rozšíření ASPX, nemusíte na vzdáleném webovém serveru provádět žádné nastavení.

## <a name="creating-a-wildcard-script-map"></a>Vytvoření mapy skriptů se zástupnými symboly

Pokud nechcete upravovat adresy URL pro ASP.NET aplikaci MVC a máte přístup k webovému serveru, máte další možnost. Můžete vytvořit mapu skriptů se zástupnými kódy, která mapuje všechny požadavky na webový server do ASP.NET rámci. Výchozím ASP.NET směrovací tabulky MVC tak to bude možné se systémem IIS 7.0 (v klasickém režimu) nebo i. 6.0.

Uvědomte si, že tato možnost způsobí, že služba IIS zachytit každý požadavek proti webovému serveru. To zahrnuje požadavky na obrázky, klasické stránky ASP a stránky HTML. Proto povolení mapy skriptu se zástupnými symboly ASP.NET má vliv na výkon.

Zde je návod, jak povolit mapu skriptů se zástupnými symboly pro službu IIS 7.0:

1. Výběr aplikace v okně Připojení
2. Zkontrolujte, zda je vybrané zobrazení **Funkce.**
3. Poklepejte na tlačítko **Mapování obslužné rutiny**
4. Klikněte na odkaz Přidat mapu **skriptů se zástupnými místy** (viz obrázek 3)
5. Zadejte cestu k souboru aspnet\_isapi.dll (Tuto cestu můžete zkopírovat z mapy skriptu PageHandlerFactory)
6. Zadejte název MVC.
7. Klikněte na tlačítko **OK.**

[![Dialogové okno New Project (Nový projekt)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.png)

**Obrázek 3**: Vytvoření mapy skriptů se zástupnými symboly se službou IIS 7.0([Klepnutím zobrazíte obrázek v plné velikosti)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image6.png)

Následujícím postupem vytvořte mapu se zástupnými symboly se službou IIS 6.0:

1. Klikněte pravým tlačítkem myši na web a vyberte Vlastnosti.
2. Výběr karty **Domovský adresář**
3. Klikněte na tlačítko **Konfigurace**
4. Výběr karty **Mapování**
5. Klikněte na tlačítko **Vložit** (viz obrázek 4)
6. Vložit cestu k souboru\_aspnet isapi.dll do pole Spustitelný soubor (tuto cestu můžete zkopírovat z mapy skriptů pro soubory ASPX).
7. Zrušení zaškrtnutí políčka s popiskem **Ověřit, zda soubor existuje.**
8. Klikněte na tlačítko **OK.**

[![Dialogové okno New Project (Nový projekt)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image7.png)

**Obrázek 4**: Vytvoření mapy skriptů se zástupnými symboly se službou IIS 6.0([Klepnutím zobrazíte obrázek v plné velikosti)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image8.png)

Po povolení map skriptů se zástupnými symboly je třeba upravit směrovací tabulku v souboru Global.asax tak, aby zahrnovala kořenovou trasu. V opačném případě se chybová stránka zobrazí na obrázku 5, když vytvoříte žádost o kořenovou stránku aplikace. Upravený soubor Global.asax můžete použít v seznamu 4.

[![Dialogové okno New Project (Nový projekt)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image9.png)

**Obrázek 5**: Chybějící chyba kořenové trasy[(Kliknutím zobrazíte obrázek v plné velikosti)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image10.png)

**Výpis 4 - Global.asax (upraveno pomocí kořenové trasy)**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample4.vb)]

Po povolení mapy skriptů se zástupnými kódy pro službu IIS 7.0 nebo službu IIS 6.0 můžete vytvořit požadavky, které pracují s výchozí směrovací tabulkou, která vypadá takto:

/

/Domů/Index

/Produkt/Podrobnosti/3

/Produkt

## <a name="summary"></a>Souhrn

Cílem tohoto kurzu bylo vysvětlit, jak můžete použít ASP.NET MVC při použití starší verze služby IIS (nebo služby IIS 7.0 v klasickém režimu). Probrali jsme dva způsoby, jak získat ASP.NET směrování pro práci se staršími verzemi služby IIS: Upravte výchozí směrovací tabulku nebo vytvořte mapu skriptů se zástupnými kódy.

První možnost vyžaduje úpravu adres URL používaných v aplikaci ASP.NET MVC. Jednou z velmi významných výhod této první možnosti je, že nepotřebujete přístup k webovému serveru, abyste mohli upravit směrovací tabulku. To znamená, že můžete použít tuto první možnost i při hostování ASP.NET aplikace MVC s internethostingovou společností.

Druhou možností je vytvoření mapy skriptů se zástupnými kódy. Výhodou této druhé možnosti je, že není nutné upravovat adresy URL. Nevýhodou této druhé možnosti je, že může ovlivnit výkon vaší aplikace ASP.NET MVC.

> [!div class="step-by-step"]
> [Předchozí](using-asp-net-mvc-with-different-versions-of-iis-cs.md)
