---
uid: mvc/overview/older-versions-1/overview/asp-net-mvc-overview
title: ASP.NET MVC Přehled | Dokumenty společnosti Microsoft
author: rick-anderson
description: Seznamte se s rozdíly mezi aplikacemi mvc ASP.NET a aplikacemi ASP.NET webových formulářů. Přečtěte si, jak se rozhodnout, kdy vytvořit ASP.NET aplikaci MVC.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 2dcb44a4-5cbf-4d62-b363-718104082d86
msc.legacyurl: /mvc/overview/older-versions-1/overview/asp-net-mvc-overview
msc.type: authoredcontent
ms.openlocfilehash: 84810f168faa2e79a65ff3fb75e3654828bdb58f
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541010"
---
# <a name="aspnet-mvc-overview"></a>ASP.NET MVC – přehled

podle [společnosti Microsoft](https://github.com/microsoft)

> Seznamte se s rozdíly mezi aplikacemi mvc ASP.NET a aplikacemi ASP.NET webových formulářů. Přečtěte si, jak se rozhodnout, kdy vytvořit ASP.NET aplikaci MVC.

Model-View-Controller (MVC) architektonický vzor odděluje aplikaci do tří hlavních součástí: model, pohled a řadič. Rozhraní ASP.NET MVC poskytuje alternativu k vzoru ASP.NET webových formulářů pro vytváření webových aplikací založených na MVC. Rozhraní ASP.NET MVC je odlehčený, vysoce testovatelný prezentační rámec, který je (stejně jako u aplikací založených na webových formulářích) integrován s existujícími ASP.NET funkcemi, jako jsou stránky předlohy a ověřování založené na členství. Rozhraní MVC je definováno v oboru názvů **System.Web.Mvc** a je základní podporovanou součástí oboru názvů **System.Web.**   
  
MVC je standardní návrhový vzor, který mnoho vývojářů zná. Některé typy webových aplikací budou mít prospěch z rozhraní MVC. Ostatní budou i nadále používat tradiční ASP.NET aplikační vzor, který je založen na webových formulářů a postbacks. Ostatní typy webových aplikací budou kombinovat dva přístupy; ani jeden přístup nevylučuje druhý.   
  
Rámec MVC zahrnuje následující součásti:

[![Vyvolání akce kontroleru, která očekává hodnotu parametru](asp-net-mvc-overview/_static/image1.jpg)](asp-net-mvc-overview/_static/image1.png)

**Obrázek 01**: Vyvolání akce kontroleru, která očekává hodnotu parametru[(Obrázek v plné velikosti klepnutím zobrazíte)](asp-net-mvc-overview/_static/image2.png)

- **Modely**. Objekty modelu jsou části aplikace, které implementují logiku pro datovou doménu aplikace s. Často objekty modelu načíst a uložit stav modelu v databázi. Například Product objekt může načíst informace z databáze, pracovat na něm a potom zapsat aktualizované informace zpět do tabulky Produkty v SQL Server.

V malých aplikacích je model často koncepční oddělení namísto fyzické. Například pokud aplikace pouze přečte sadu dat a odešle ji do zobrazení, aplikace nemá vrstvu fyzického modelu a přidružené třídy. V takovém případě přebírá sada dat roli objektu modelu.

- **Zobrazení**. Zobrazení jsou součásti, které zobrazují uživatelské rozhraní aplikace (UI). Toto unové nastavení se obvykle vytváří z dat modelu. Příkladem může být zobrazení úprav tabulky Produkty, která zobrazuje textová pole, rozevírací seznamy a zaškrtávací políčka na základě aktuálního stavu objektu Products.

- **Regulátory**. Řadiče jsou součásti, které zpracovávají interakci uživatele, pracují s modelem a nakonec vyberte zobrazení, které vykreslí uživatelské rozhraní. V aplikaci MVC zobrazení zobrazuje pouze informace; ovladač zpracovává a reaguje na vstup a interakci uživatele. Například řadič zpracovává hodnoty řetězce dotazu a předá tyto hodnoty modelu, který zase dotazuje databázi pomocí hodnot.

Vzor MVC pomáhá vytvářet aplikace, které oddělují různé aspekty aplikace (vstupní logika, obchodní logika a logika uživatelského rozhraní) a zároveň poskytují volné párování mezi těmito prvky. Vzor určuje, kde by měl být každý druh logiky umístěn v aplikaci. Logika ui patří do zobrazení. Vstupní logika patří do řadiče. Obchodní logika patří do modelu. Toto oddělení pomáhá spravovat složitost při vytváření aplikace, protože umožňuje zaměřit se na jeden aspekt implementace najednou. Můžete se například zaměřit na zobrazení bez závislosti na obchodní logice.   
  
Kromě správy složitosti, Vzor MVC usnadňuje testování aplikací, než je testování webových formulářů založené ASP.NET webové aplikace. Například ve webové aplikaci založené na webových formulářích ASP.NET se jedna třída používá jak k zobrazení výstupu, tak k reakci na vstup uživatele. Psaní automatizovaných testů pro aplikace ASP.NET založené na webových formulářích může být složité, protože chcete-li otestovat jednotlivé stránky, je nutné vytvořit instanci třídy stránky, všechny její podřízené ovládací prvky a další závislé třídy v aplikaci. Vzhledem k tomu, že tolik tříd jsou vytvořena instance ke spuštění stránky, může být obtížné psát testy, které se zaměřují výhradně na jednotlivé části aplikace. Testy pro webové formuláře založené ASP.NET aplikace proto může být obtížnější implementovat než testy v aplikaci MVC. Testy v aplikaci ASP.NET založené na webových formulářích navíc vyžadují webový server. Rozhraní MVC odděluje součásti a umožňuje velké využití rozhraní, což umožňuje testovat jednotlivé součásti izolovaně od zbytku rámce.   
  
Volná vazba mezi třemi hlavními součástmi aplikace MVC také podporuje paralelní vývoj. Například jeden vývojář může pracovat na zobrazení, druhý vývojář může pracovat na logice řadiče a třetí vývojář se může zaměřit na obchodní logiku v modelu.

## <a name="deciding-when-to-create-an-mvc-application"></a>Rozhodování o tom, kdy vytvořit aplikaci MVC

Je třeba pečlivě zvážit, zda chcete implementovat webovou aplikaci pomocí ASP.NET rozhraní MVC nebo modelu ASP.NET webových formulářů. Rozhraní MVC nenahrazuje model webových formulářů. můžete použít obě architektury pro webové aplikace. (Pokud máte existující aplikace založené na webových formulářích, budou nadále fungovat přesně tak, jak vždy.)   
  
Než se rozhodnete použít rozhraní MVC framework nebo model webových formulářů pro konkrétní web, zvažte výhody každého přístupu.

### <a name="advantages-of-an-mvc-based-web-application"></a>Výhody webové aplikace založené na MVC

ASP.NET MVC framework nabízí následující výhody:

- Usnadňuje správu složitosti rozdělením aplikace do modelu, zobrazení a kontroleru.
- Nepoužívá formuláře stavu zobrazení nebo formuláře založené na serveru. Díky rozhraní MVC ideální pro vývojáře, kteří chtějí plnou kontrolu nad chováním aplikace.
- Používá vzor předního řadiče, který zpracovává požadavky webových aplikací prostřednictvím jediného řadiče. To umožňuje navrhnout aplikaci, která podporuje bohatou infrastrukturu směrování. Další informace naleznete v tématu [Front Controller](https://go.microsoft.com/fwlink/?LinkId=106357 "Přední ovladač") na webu MSDN.
- Poskytuje lepší podporu pro vývoj řízený testováním (TDD).
- Funguje dobře pro webové aplikace, které jsou podporovány velké týmy vývojářů a webových návrhářů, kteří potřebují vysoký stupeň kontroly nad chováním aplikace.

### <a name="advantages-of-a-web-forms-based-web-application"></a>Výhody webové aplikace založené na webových formulářích

Rámec založený na webových formulářích nabízí následující výhody:

- Podporuje model událostí, který zachovává stav přes HTTP, který využívá vývoj obchodních webových aplikací. Aplikace založená na webových formulářích poskytuje desítky událostí, které jsou podporovány ve stovkách serverových ovládacích prvků.
- Používá vzor řadiče stránky, který přidává funkce pro jednotlivé stránky. Další informace naleznete [v tématu Page Controller](https://go.microsoft.com/fwlink/?LinkId=106359 "Řadič stránky") na webu MSDN.
- Používá formuláře stavu zobrazení nebo formuláře založené na serveru, které mohou usnadnit správu informací o stavu.
- Funguje dobře pro malé týmy webových vývojářů a návrhářů, kteří chtějí využít velkého počtu součástí, které jsou k dispozici pro rychlý vývoj aplikací.
- Obecně platí, že je méně složité pro vývoj aplikací, protože součásti **(Page** třídy, ovládací prvky a tak dále) jsou úzce integrované a obvykle vyžadují méně kódu než model MVC.

## <a name="features-of-the-aspnet-mvc-framework"></a>Vlastnosti ASP.NET MVC Framework

Rozhraní ASP.NET MVC poskytuje následující funkce:

- Oddělení aplikačních úloh (vstupní logika, obchodní logika a logika ui), testovatelnost a vývoj řízený testováním (TDD) ve výchozím nastavení. Všechny základní kontrakty v rámci MVC jsou založeny na rozhraní a lze je testovat pomocí mock objekty, které jsou simulované objekty, které napodobují chování skutečných objektů v aplikaci. Můžete jednotkový test aplikace bez nutnosti spouštět řadiče v procesu ASP.NET, což umožňuje testování částí rychlé a flexibilní. Můžete použít libovolnou architekturu testování částí, která je kompatibilní s rozhraním .NET Framework.
- Rozšiřitelný a zásuvný rámec. Součásti ASP.NET mvc frameworku jsou navrženy tak, aby je bylo možné snadno vyměnit nebo přizpůsobit. Můžete připojit vlastní modul zobrazení, zásady směrování adres URL, serializaci parametrů metody akce a další součásti. Rozhraní ASP.NET MVC také podporuje použití kontejnerů vkládání závislostí (DI) a inverze řízení (IOC). DI umožňuje vstřikovat objekty do třídy, namísto spoléhání se na třídu k vytvoření samotného objektu. IOC určuje, že pokud objekt vyžaduje jiný objekt, první objekty by měly získat druhý objekt z vnějšího zdroje, jako je například konfigurační soubor. To usnadňuje testování.
- Výkonná komponenta mapování adres URL, která umožňuje vytvářet aplikace, které mají srozumitelné a prohledávatelné adresy URL. Adresy URL nemusí obsahovat přípony názvů souborů a jsou navrženy tak, aby podporovaly vzory pojmenování adres URL, které dobře fungují pro optimalizaci pro vyhledávače (SEO) a reprezentační přenos stavu (REST).
- Podpora použití značek v existujících ASP.NET stránce (soubory aspx), uživatelského ovládacího prvku (soubory ascx) a vzorové stránky (.vzorové soubory) jako šablon zobrazení. Existující ASP.NET funkce můžete použít s ASP.NET mvc framework, jako jsou vnořené stránky předlohy, in-line výrazy (&lt;%= %&gt;), deklarativní serverové ovládací prvky, šablony, datová vazba, lokalizace a tak dále.
- Podpora stávajících ASP.NET funkcí. ASP.NET MVC umožňuje používat funkce, jako je ověřování pomocí formulářů a ověřování systému Windows, autorizace adres URL, členství a role, ukládání výstupu a dat do mezipaměti, správa stavu relací a profilu, monitorování stavu, konfigurační systém a architektura zprostředkovatele.
