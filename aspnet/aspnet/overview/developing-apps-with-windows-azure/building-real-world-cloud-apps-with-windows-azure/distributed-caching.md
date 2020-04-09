---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
title: Distribuované ukládání do mezipaměti (vytváření cloudových aplikací v reálném světě s Azure) | Dokumenty společnosti Microsoft
author: MikeWasson
description: Cloudová kniha Building Real World S Azure vychází z prezentace vyvinuté Scottem Guthriem. Vysvětluje to 13 vzorů a postupů, které může...
ms.author: riande
ms.date: 07/20/2015
ms.assetid: 406518e9-3817-49ce-8b90-e82bc461e2c0
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
msc.type: authoredcontent
ms.openlocfilehash: 87a7516415895e761d1589fd459b93e5c15c0f85
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676018"
---
# <a name="distributed-caching-building-real-world-cloud-apps-with-azure"></a>Distribuované ukládání do mezipaměti (vytváření reálných cloudových aplikací s Azure)

od [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), Tom [Dykstra](https://github.com/tdykstra)

[Stáhnout Fix It Project](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) nebo [stáhnout E-knihy](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **Cloudová kniha Building Real World S Azure** vychází z prezentace vyvinuté Scottem Guthriem. Vysvětluje 13 vzorů a postupů, které vám mohou pomoci úspěšně vyvíjet webové aplikace pro cloud. Informace o e-knize najdete [v první kapitole](introduction.md).

Předchozí kapitola se zabývala přechodnou manipulací s chybami a jako strategií jističe uvedla ukládání do mezipaměti. Tato kapitola poskytuje další informace o ukládání do mezipaměti, včetně toho, kdy ji použít, běžné vzory pro jeho použití a jak ji implementovat v Azure.

## <a name="what-is-distributed-caching"></a>Co je distribuováno ukládání do mezipaměti

Mezipaměť poskytuje vysokou propustnost, přístup s nízkou latencí k běžně přistupovaným datům aplikací uložením dat do paměti. Pro cloudovou aplikaci je nejužitečnějším typem mezipaměti distribuovaná mezipaměť, což znamená, že data nejsou uložena v paměti jednotlivých webových serverů, ale na jiných cloudových prostředcích, a data uložená v mezipaměti jsou k dispozici všem webovým serverům aplikace (nebo jiným cloudovým virtuálním počítačům používaným aplikací).

![Diagram znázorňující více webových serverů přistupujících ke stejným serverům mezipaměti](distributed-caching/_static/image1.png)

Při škálování aplikace přidáním nebo odebráním serverů nebo při výměně serverů z důvodu upgradů nebo chyb zůstanou data uložená v mezipaměti přístupná všem serverům, na kterých je aplikace spuštěna.

Tím, že se vyhnete přístupu k datům s vysokou latencí v trvalém úložišti dat, ukládání do mezipaměti může výrazně zlepšit odezvu aplikací. Například načítání dat z mezipaměti je mnohem rychlejší než načítání z relační databáze.

Vedlejší výhodou ukládání do mezipaměti je snížení provozu na trvalé úložiště dat, což může mít za následek nižší náklady, pokud jsou poplatky za odchozí data pro úložiště trvalých dat.

## <a name="when-to-use-distributed-caching"></a>Kdy použít distribuované ukládání do mezipaměti

Ukládání do mezipaměti funguje nejlépe pro úlohy aplikací, které více čtou než psaní dat a když datový model podporuje organizaci klíč/hodnota, kterou používáte k ukládání a načítání dat v mezipaměti. Je také užitečnější, když uživatelé aplikací sdílejí velké množství běžných dat; například mezipaměť by neposkytovala tolik výhod, pokud každý uživatel obvykle načítá data jedinečná pro tohoto uživatele. Příkladem, kde ukládání do mezipaměti může být velmi prospěšné, je katalog produktů, protože data se často nemění a všichni zákazníci se dívají na stejná data.

Výhody ukládání do mezipaměti se stává stále měřitelnější, čím více se škáluje velikost aplikace, protože omezení propustnosti a zpoždění latence trvalého úložiště dat se stávají spíše limitem celkového výkonu aplikace. Ukládání do mezipaměti však můžete implementovat i z jiných důvodů než výkonu. Pro data, která nemusí být dokonale aktuální při zobrazení uživateli, může přístup do mezipaměti sloužit jako jistič, když trvalé úložiště dat neodpovídá nebo není k dispozici.

## <a name="popular-cache-population-strategies"></a>Populární strategie populace mezipaměti

Aby bylo možné načíst data z mezipaměti, musíte je nejprve uložit. Existuje několik strategií pro získávání dat, které potřebujete do mezipaměti:

- Na vyžádání / Cache Stranou

    Aplikace se pokusí načíst data z mezipaměti a pokud mezipaměť nemá data ("miss"), aplikace uloží data do mezipaměti tak, aby byla k dispozici příště. Při příštím pokusu aplikace získat stejná data, najde to, co hledá v mezipaměti ("přístupů"). Chcete-li zabránit načítání dat uložených v mezipaměti, která se v databázi změnila, zrušíte platnost mezipaměti při provádění změn v úložišti dat.
- Nabízení dat na pozadí

    Služby na pozadí nabízená data do mezipaměti v pravidelných intervalech a aplikace vždy vytáhne z mezipaměti. Tento přístup funguje skvěle se zdroji dat s vysokou latencí, které nevyžadují vždy vrátit nejnovější data.
- Circuit Breaker

    Aplikace obvykle komunikuje přímo s trvalým úložištěm dat, ale když má trvalé úložiště dat problémy s dostupností, aplikace načte data z mezipaměti. Data mohla být vložena do mezipaměti pomocí strategie nabízení dat v mezipaměti nebo pomocí strategie nabízení dat na pozadí. Jedná se o strategii zpracování chyb spíše než strategie zvyšující výkon.

Chcete-li zachovat data v aktuální mezipaměti, můžete odstranit související položky mezipaměti, když aplikace vytvoří, aktualizuje nebo odstraní data. Pokud je v pořádku, aby vaše aplikace někdy získala data, která jsou mírně zastaralá, můžete se spolehnout na konfigurovatelný čas vypršení platnosti, který vám nastaví limit na to, jak stará data mezipaměti mohou být.

Můžete nakonfigurovat absolutní vypršení platnosti (dobu od vytvoření položky mezipaměti) nebo klouzavé vypršení platnosti (doba od posledního přístupu k položce mezipaměti). Absolutní vypršení platnosti se používá, pokud jste v závislosti na mechanismu vypršení platnosti mezipaměti zabránit data stanou příliš zastaralé. V aplikaci Fix It ručně vyřazujeme zastaralé položky mezipaměti a použijeme klouzavé vypršení platnosti, abychom udrželi nejaktuálnější data v mezipaměti. Bez ohledu na zásady vypršení platnosti, které zvolíte, bude mezipaměti automaticky vyřadit nejstarší (nejméně naposledy použité nebo LRU) položky při dosažení limitu paměti mezipaměti.

## <a name="sample-cache-aside-code-for-fix-it-app"></a>Ukázkový kód stranou mezipaměti pro aplikaci Fix It

V následujícím ukázkovém kódu nejprve zkontrolujeme mezipaměť při načítání úlohy Fix It. Pokud je úloha nalezena v mezipaměti, vrátíme ji; pokud není nalezen, dostaneme ji z databáze a uložit ji do mezipaměti. Změny, které byste provést přidat ukládání `FindTaskByIdAsync` do mezipaměti k metodě jsou zvýrazněny.

[!code-csharp[Main](distributed-caching/samples/sample1.cs?highlight=5,9-11,13-15,19)]

Při aktualizaci nebo odstranění úkolu Opravit je nutné úlohu uloženou v mezipaměti zrušit(odstranit). V opačném případě budou budoucí pokusy o čtení této úlohy nadále získat stará data z mezipaměti.

[!code-csharp[Main](distributed-caching/samples/sample2.cs?highlight=7)]

Jedná se o ukázky pro ilustraci jednoduchého kódu ukládání do mezipaměti; ukládání do mezipaměti nebylo implementováno v projektu Fix It ke stažení.

## <a name="azure-caching-services"></a>Služby ukládání do mezipaměti Azure

Azure nabízí následující služby ukládání do mezipaměti: [Azure Redis Cache](https://msdn.microsoft.com/library/dn690523.aspx) a [Azure Managed Cache](https://msdn.microsoft.com/library/dn386094.aspx). Mezipaměť Azure Redis je založená na oblíbené [open source mezipaměti Redis](http://redis.io/) a je první volbou pro většinu scénářů ukládání do mezipaměti.

<a id="sessionstate"></a>
## <a name="aspnet-session-state-using-a-cache-provider"></a>ASP.NET stavu relace pomocí zprostředkovatele mezipaměti

Jak je uvedeno v [kapitole osvědčených postupů pro vývoj webových aplikací](web-development-best-practices.md), osvědčeným postupem je vyhnout se použití stavu relace. Pokud vaše aplikace vyžaduje stav relace, dalším osvědčeným postupem je vyhnout se výchozímu zprostředkovateli v paměti, protože to neumožňuje horizontální navýšení kapacity (více instancí webového serveru). Poskytovatel stavu relace ASP.NET serveru SQL Server umožňuje webu, který běží na více webových serverech, používat stav relace, ale ve srovnání s poskytovatelem v paměti mu vznikají vysoké náklady na latenci. Nejlepším řešením, pokud máte použít stav relace je použít zprostředkovatele mezipaměti, jako je [například zprostředkovatel stavu relace pro Azure Cache](https://msdn.microsoft.com/library/windowsazure/gg185668.aspx).

## <a name="summary"></a>Souhrn

Viděli jste, jak opravit it aplikace může implementovat ukládání do mezipaměti s cílem zlepšit dobu odezvy a škálovatelnost a povolit aplikaci i nadále reagovat pro operace čtení, když databáze není k dispozici. V [další kapitole](queue-centric-work-pattern.md) vám ukážeme, jak dále zlepšit škálovatelnost a aby aplikace i nadále reagovala na operace zápisu.

## <a name="resources"></a>Zdroje a prostředky

Další informace o ukládání do mezipaměti naleznete v následujících zdrojích.

Dokumentace

- [Mezipaměť Azure](https://msdn.microsoft.com/library/gg278356.aspx). Oficiální dokumentace MSDN o ukládání do mezipaměti v Azure.
- [Vzory a postupy microsoftu – pokyny k Azure](https://msdn.microsoft.com/library/dn568099.aspx). Viz Ukládání do mezipaměti navádění a Cache-Aside vzor.
- [Failsafe: Pokyny pro odolné cloudové architektury](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx). Bílá kniha Marc Mercuri, Ulrich Homann, a Andrew Townhill. Podívejte se na sekci Caching.
- [Doporučené postupy pro návrh rozsáhlých služeb ve cloudových službách Azure](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx). W. Bílá kniha Marka Simmse a Michaela Thomassyho. Viz část o distribuovaném ukládání do mezipaměti.
- [Distribuované ukládání do mezipaměti na cestě k škálovatelnosti](https://msdn.microsoft.com/magazine/dd942840.aspx). Starší (2009) MSDN Časopis článek, ale jasně napsaný úvod do distribuované ukládání do mezipaměti obecně; jde do větší hloubky než ukládání do mezipaměti oddíly FailSafe a doporučené postupy bílé knihy.

Videa

- [FailSafe: Vytváření škálovatelných, odolných cloudových služeb](https://channel9.msdn.com/Series/FailSafe). Devítidílný seriál Ulricha Homanna, Marca Mercuriho a Marka Simmse. Představuje 400-level zobrazení, jak architekt cloudové aplikace. Tato série se zaměřuje na teorii a důvody, proč; Další podrobnosti najdete v tématu Building Big series od Marka Simmse. Podívejte se na diskuzi o ukládání do mezipaměti v epizodě 3 od 1:24:14.
- [Building Big: Poučení od zákazníků Azure – část I](https://channel9.msdn.com/Events/Build/2012/3-029). Simon Davies diskutuje distribuované ukládání do mezipaměti od 46:00. Podobně jako série Failsafe, ale jde do více jak-na detaily. Prezentace byla dána 31 října 2012, takže se nevztahuje na ukládání do mezipaměti služby Webových aplikací ve službě Azure App Service, která byla zavedena v 2013.

Ukázka kódu

- [Základy cloudových služeb v Azure](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649). Ukázková aplikace, která implementuje distribuované ukládání do mezipaměti. Podívejte se na doprovodný blogový příspěvek [Základy cloudových služeb – Základy ukládání do mezipaměti](https://blogs.msdn.com/b/windowsazure/archive/2013/10/03/cloud-service-fundamentals-caching-basics.aspx).

> [!div class="step-by-step"]
> [Předchozí](transient-fault-handling.md)
> [další](queue-centric-work-pattern.md)
