---
uid: web-forms/overview/moving-to-aspnet-20/caching
title: Ukládání do mezipaměti | Dokumenty společnosti Microsoft
author: rick-anderson
description: Pochopení ukládání do mezipaměti je důležité pro dobře fungující ASP.NET aplikace. ASP.NET 1.x nabídl tři různé možnosti ukládání do mezipaměti; ukládání výstupu do mezipaměti,...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 2bb109d2-e299-46ea-9054-fa0263b59165
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/caching
msc.type: authoredcontent
ms.openlocfilehash: a199a9c0352dfb054e8d4e5e67652db9bd38851c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542934"
---
# <a name="caching"></a>Ukládání do mezipaměti

podle [společnosti Microsoft](https://github.com/microsoft)

> Pochopení ukládání do mezipaměti je důležité pro dobře fungující ASP.NET aplikace. ASP.NET 1.x nabídl tři různé možnosti ukládání do mezipaměti; ukládání výstupu do mezipaměti, ukládání fragmentů do mezipaměti a rozhraní API mezipaměti.

Pochopení ukládání do mezipaměti je důležité pro dobře fungující ASP.NET aplikace. ASP.NET 1.x nabídl tři různé možnosti ukládání do mezipaměti; ukládání výstupu do mezipaměti, ukládání fragmentů do mezipaměti a rozhraní API mezipaměti. ASP.NET 2.0 nabízí všechny tři tyto metody, ale přidává některé významné další funkce. Existuje několik nových závislostí mezipaměti a vývojáři mají nyní možnost vytvořit vlastní závislosti mezipaměti také. Konfigurace ukládání do mezipaměti byla také výrazně vylepšena v ASP.NET 2.0.

## <a name="new-features"></a>Nové funkce

## <a name="cache-profiles"></a>Profily mezipaměti

Profily mezipaměti umožňují vývojářům definovat konkrétní nastavení mezipaměti, které lze použít na jednotlivé stránky. Máte-li například některé stránky, jejichž platnost by měla po 12 hodinách vypršet z mezipaměti, můžete snadno vytvořit profil mezipaměti, který lze na tyto stránky použít. Chcete-li přidat nový profil &lt;mezipaměti, použijte oddíl outputCacheSettings&gt; v konfiguračním souboru. Níže je například konfigurace profilu mezipaměti s názvem *twoday,* která konfiguruje dobu trvání mezipaměti 12 hodin.

[!code-xml[Main](caching/samples/sample1.xml)]

Chcete-li použít tento profil mezipaměti na určitou stránku, použijte atribut CacheProfile direktivy @ OutputCache, jak je znázorněno níže:

[!code-aspx[Main](caching/samples/sample2.aspx)]

## <a name="custom-cache-dependencies"></a>Vlastní závislosti mezipaměti

ASP.NET vývojáři 1.x volali po závislostech vlastní mezipaměti. V ASP.NET 1.x byla zapečetěna třída CacheDependency, která zabránila vývojářům v odvození vlastních tříd. V ASP.NET 2.0 je toto omezení odebráno a vývojáři mohou volně vyvíjet vlastní závislosti mezipaměti. Třída CacheDependency umožňuje vytvoření vlastní závislosti mezipaměti založené na souborech, adresářích nebo klíčích mezipaměti.

Níže uvedený kód například vytvoří novou závislost vlastní mezipaměti založenou na souboru nazvaném stuff.xml umístěném v kořenovém adresáři webové aplikace:

[!code-csharp[Main](caching/samples/sample3.cs)]

V tomto scénáři při změně souboru stuff.xml je položka uložená v mezipaměti zrušena.

Je také možné vytvořit vlastní závislost mezipaměti pomocí klíčů mezipaměti. Při použití této metody odebrání klíče mezipaměti zruší platnost dat uložených v mezipaměti. Ilustruje to následující příklad:

[!code-csharp[Main](caching/samples/sample4.cs)]

Chcete-li zrušit platnost položky, která byla vložena výše, jednoduše odeberte položku, která byla vložena do mezipaměti, aby působila jako klíč mezipaměti.

[!code-csharp[Main](caching/samples/sample5.cs)]

Všimněte si, že klíč položky, která funguje jako klíč mezipaměti, musí být stejný jako hodnota přidaná do pole klíčů mezipaměti.

## <a name="polling-based-sql-cache-dependenciesalso-called-table-based-dependencies"></a>Závislosti mezipaměti SQL založené na dotazování (nazývané se také závislosti založené na tabulkách)

SQL Server 7 a 2000 použít model založený na dotazování pro sql mezipaměti závislosti. Model založený na dotazování používá aktivační událost v databázové tabulce, která se aktivuje při změně dat v tabulce. Tato aktivační událost aktualizuje **pole changeId** v tabulce oznámení, které ASP.NET pravidelně kontroluje. Pokud bylo pole **changeId** aktualizováno, ASP.NET ví, že se data změnila, a zruší platnost dat uložených v mezipaměti.

> [!NOTE]
> SQL Server 2005 můžete také použít model založený na dotazování, ale protože model založený na dotazování není nejúčinnější model, je vhodné použít model založený na dotazu (popsáno později) s SQL Server 2005.

Aby závislost mezipaměti SQL pomocí modelu založeného na dotazování fungovala správně, musí být v tabulkách povolena oznámení. Toho lze provést programově pomocí třídy SqlCacheDependencyAdmin nebo pomocí\_nástroje aspnet regsql.exe.

Následující příkazový řádek registruje tabulku Products v databázi Northwind umístěnou v instanci serveru SQL Server s názvem *dbase* pro závislost mezipaměti SQL.

[!code-console[Main](caching/samples/sample6.cmd)]

Následuje vysvětlení přepínačů příkazového řádku použitých ve výše uvedeném příkazu:

| **Přepínač příkazového řádku** | **Účel** |
| --- | --- |
| -S *server* | Určuje název serveru. |
| -ed | Určuje, že databáze by měla být povolena pro závislost mezipaměti SQL. |
| Název *databáze\_* -d | Určuje název databáze, který by měl být povolen pro závislost mezipaměti SQL. |
| -E | Určuje, že aspnet\_regsql by měl používat ověřování systému Windows při připojování k databázi. |
| -et | Určuje, že povolujeme databázovou tabulku pro závislost mezipaměti SQL. |
| -t *\_název tabulky* | Určuje název databázové tabulky, která má být povolena pro závislost mezipaměti SQL. |

> [!NOTE]
> Existují další přepínače k\_dispozici pro aspnet regsql.exe. Pro úplný seznam, spusťte aspnet\_regsql.exe -? z příkazového řádku.

Při spuštění tohoto příkazu jsou provedeny následující změny v databázi serveru SQL Server:

- Je přidána tabulka **AspNet\_SqlCacheTablesForChangeNotification.** Tato tabulka obsahuje jeden řádek pro každou tabulku v databázi, pro kterou byla povolena závislost mezipaměti SQL.
- Následující uložené procedury jsou vytvořeny uvnitř databáze:

| Postup aspnet\_SqlCachePollingStoredProcedure | Dotazuje aspNet\_SqlCacheTablesForChangeNotification tabulka a vrátí všechny tabulky, které jsou povoleny pro závislost mezipaměti SQL a hodnotu changeId pro každou tabulku. Tento uložený proc se používá pro dotazování k určení, zda se data změnila. |
| --- | --- |
| AspNet\_SqlCacheQueryRegisteredTablesStoredProcedure | Vrátí všechny tabulky povolené pro závislost mezipaměti SQL dotazem na tabulku AspNet\_SqlCacheTablesForChangeNotification a vrátí všechny tabulky povolené pro závislost mezipaměti SQL. |
| AspNet\_SqlCacheRegisterTableStoredProcedure | Zaregistruje tabulku pro závislost mezipaměti SQL přidáním potřebné položky v tabulce oznámení a přidá aktivační událost. |
| AspNet\_SqlCacheUnRegisterStoredProcedure | Zruší registraci tabulky pro závislost mezipaměti SQL odebráním položky v tabulce oznámení a odebere aktivační událost. |
| AspNet\_SqlCacheChangeIdStoredProcedure | Aktualizuje oznamovací tabulku zvýšením changeId pro změněnou tabulku. ASP.NET používá tuto hodnotu k určení, zda se data změnila. Jak je uvedeno níže, tento uložený proc je proveden aktivační událostí vytvořenou při povolení tabulky. |

- Pro tabulku je vytvořena aktivační událost serveru SQL Server s názvem ** _\__\_AspNet\_SqlCacheNotification\_Trigger.** Tato aktivační událost spustí\_proceduru AspNet SqlCacheChangeIdStoredProcedure při provedení příkazu INSERT, UPDATE nebo DELETE v tabulce.
- Do databáze je přidána role serveru SQL Server s názvem **aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess.**

Role **aspnet\_\_ChangeNotification ReceiveNotificationsOnlyAccess** SQL Server má oprávnění\_EXEC k postupu AspNet SqlCachePollingStoredProcedure. Aby model dotazování fungoval správně, je nutné přidat účet procesu do role aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess. Nástroj aspnet\_regsql.exe to za vás neudělá.

### <a name="configuring-polling-based-sql-cache-dependencies"></a>Konfigurace závislostí mezipaměti SQL založené na dotazování

Existuje několik kroků, které jsou nutné pro konfiguraci závislostí mezipaměti SQL založené na dotazování. Prvním krokem je povolit databázi a tabulku, jak je popsáno výše. Po dokončení tohoto kroku je zbytek konfigurace následující:

- Konfigurace konfiguračního souboru ASP.NET.
- Konfigurace sqlcachedependency

### <a name="configuring-the-aspnet-configuration-file"></a>Konfigurace konfiguračního souboru ASP.NET

Kromě přidání připojovacího řetězce, jak je popsáno &lt;&gt; v předchozím &lt;modulu,&gt; musíte také nakonfigurovat prvek mezipaměti s elementem sqlCacheDependency, jak je znázorněno níže:

[!code-xml[Main](caching/samples/sample7.xml)]

Tato konfigurace umožňuje závislost mezipaměti SQL v *databázi pubs.* Všimněte si, že &lt;atribut pollTime&gt; v elementu sqlCacheDependency je výchozí na 60000 milisekund nebo 1 minutu. (Tato hodnota nesmí být menší než 500 milisekund.) V tomto &lt;příkladu&gt; přidá prvek novou databázi a přepíše pollTime a nastaví ji na 9000000 milisekund.

#### <a name="configuring-the-sqlcachedependency"></a>Konfigurace sqlcachedependency

Dalším krokem je konfigurace SqlCacheDependency. Nejjednodušší způsob, jak dosáhnout, že je zadat hodnotu pro SqlDependency atribut v @ Outcache směrnice takto:

[!code-aspx[Main](caching/samples/sample8.aspx)]

Ve výše uvedené direktivě @ OutputCache je pro tabulku *autoři* v *databázi pubs* nakonfigurována závislost mezipaměti SQL. Více závislostí lze nakonfigurovat tak, že je oddělíte středníkem takto:

[!code-aspx[Main](caching/samples/sample9.aspx)]

Další metodou konfigurace SqlCacheDependency je tak učinit programově. Následující kód vytvoří novou závislost mezipaměti SQL na tabulka *autoři* v *databázi pubs.*

[!code-csharp[Main](caching/samples/sample10.cs)]

Jednou z výhod programového definování závislostí mezipaměti SQL je, že můžete zpracovat všechny výjimky, které mohou nastat. Pokud se například pokusíte definovat závislost mezipaměti SQL pro databázi, která nebyla povolena pro oznámení, bude vyvolána výjimka **DatabaseNotEnabledForNotificationException.** V takovém případě se můžete pokusit povolit databázi pro oznámení voláním **metody SqlCacheDependencyAdmin.EnableNotifications** a jejím předáním názvu databáze.

Podobně pokud se pokusíte definovat závislost mezipaměti SQL pro tabulku, která nebyla povolena pro oznámení, **tableNotNotEnabledForNotificationException** bude vyvolána. Potom můžete volat metodu **SqlCacheDependencyAdmin.EnableTableForNotifications,** která jí předává název databáze a název tabulky.

Následující ukázka kódu ukazuje, jak správně nakonfigurovat zpracování výjimek při konfiguraci závislosti mezipaměti SQL.

[!code-csharp[Main](caching/samples/sample11.cs)]

Více informací:[https://msdn.microsoft.com/library/t9x04ed2.aspx](https://msdn.microsoft.com/library/t9x04ed2.aspx)

## <a name="query-based-sql-cache-dependencies-sql-server-2005-only"></a>Závislosti mezipaměti SQL založené na dotazech (pouze SQL Server 2005)

Při použití sql server 2005 pro sql cache závislost, model založený na dotazování není nutné. Při použití se serverem SQL Server 2005 komunikují závislosti mezipaměti SQL přímo prostřednictvím připojení SQL k instanci serveru SQL Server (není nutná žádná další konfigurace) pomocí oznámení dotazu serveru SQL Server 2005.

Nejjednodušší způsob, jak povolit oznámení založené na dotazech, je provést deklarativně nastavením atributu **SqlCacheDependency** objektu zdroje dat na **Příkaz– a** nastavením atributu **EnableCaching** na **hodnotu true**. Pomocí této metody není vyžadován žádný kód. Pokud se výsledek příkazu provedeného proti zdroji dat změní, zruší platnost dat mezipaměti.

Následující příklad konfiguruje ovládací prvek zdroje dat pro závislost mezipaměti SQL:

[!code-aspx[Main](caching/samples/sample12.aspx)]

V tomto případě pokud dotaz zadaný v **SelectCommand** vrátí jiný výsledek, než tomu bylo původně, výsledky, které jsou uloženy v mezipaměti jsou zrušeny.

Můžete také určit, že všechny zdroje dat budou povoleny pro závislosti mezipaměti SQL nastavením atributu **SqlDependency** direktivy **@ OutputCache** na **CommandNotification**. Následující příklad to ilustruje.

[!code-aspx[Main](caching/samples/sample13.aspx)]

> [!NOTE]
> Další informace o oznámeních dotazů na serveru SQL Server 2005 naleznete v části SQL Server Books Online.

Další metodou konfigurace závislosti mezipaměti SQL založené na dotazu je programově použít třídu SqlCacheDependency. Následující ukázka kódu ukazuje, jak se to provádí.

[!code-csharp[Main](caching/samples/sample14.cs)]

Více informací:[https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp](https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp)

## <a name="post-cache-substitution"></a>Nahrazení po mezipaměti

Ukládání stránky do mezipaměti může výrazně zvýšit výkon webové aplikace. V některých případech však potřebujete většinu stránky, které mají být uloženy do mezipaměti a některé fragmenty v rámci stránky, které mají být dynamické. Pokud například vytvoříte stránku zpráv, která je po nastavená období zcela statická, můžete nastavit celou stránku tak, aby byla uložena do mezipaměti. Pokud jste chtěli zahrnout rotující reklamní banner, který se změnil na každé stránce žádosti, pak část stránky obsahující reklamu musí být dynamický. Chcete-li umožnit ukládání stránky do mezipaměti, ale dynamicky nahradit určitý obsah, můžete použít ASP.NET nahrazení po mezipaměti. Při nahrazování po mezipaměti je celá stránka uložena do mezipaměti s určitými částmi označenými jako osvobozené od ukládání do mezipaměti. V příkladu reklamních bannerů vám ovládací prvek AdRotator umožňuje využít výhod nahrazení po mezipaměti tak, aby reklamy byly dynamicky vytvořeny pro každého uživatele a pro každou aktualizaci stránky.

Existují tři způsoby, jak implementovat substituci po mezipaměti:

- Deklarativně pomocí substituční ho ovládacího prvku.
- Programově pomocí rozhraní API pro řízení substituce.
- Implicitně pomocí ovládacího prvku AdRotator.

### <a name="substitution-control"></a>Řízení substituce

Ovládací prvek ASP.NET Substituce určuje část stránky uložené v mezipaměti, která je vytvořena dynamicky, nikoli v mezipaměti. Ovládací prvek Substituce umístíte do umístění na stránce, kde se má dynamický obsah zobrazit. Za běhu substituční ovládací prvek volá metodu, kterou zadáte s MethodName vlastnost. Metoda musí vrátit řetězec, který pak nahradí obsah substituční ovládací prvek. Metoda musí být statickou metodou v ovládacím prvku obsahujícím stránku nebo usercontrol. Použití substitučního ovládacího prvku způsobí, že cacheability na straně klienta se změní na mezipaměti serveru, takže stránka nebude uložena do mezipaměti klienta. Tím je zajištěno, že budoucí požadavky na stránku znovu volají metodu ke generování dynamického obsahu.

### <a name="substitution-api"></a>Substituční rozhraní API

Chcete-li vytvořit dynamický obsah pro stránku uloženou v mezipaměti programově, můžete volat metodu [WriteSubstitution](https://msdn.microsoft.com/library/system.web.httpresponse.writesubstitution.aspx) v kódu stránky a předat jí název metody jako parametr. Metoda, která zpracovává vytvoření dynamického obsahu trvá jeden [Parametr HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.aspx) a vrátí řetězec. Návratový řetězec je obsah, který bude nahrazen v daném umístění. Výhodou volání WriteSubstitution metoda namísto použití substituční ovládací prvek deklarativně je, že můžete volat metodu libovolný objekt spíše než volání statické metody Page nebo UserControl objektu.

Volání WriteSubstitution metoda způsobí, že cacheability na straně klienta změnit cacheability serveru, takže stránka nebude uložena do mezipaměti na straně klienta. Tím je zajištěno, že budoucí požadavky na stránku znovu volají metodu ke generování dynamického obsahu.

### <a name="adrotator-control"></a>Ovládací prvek AdRotator

Serverový ovládací prvek AdRotator implementuje podporu pro nahrazení po mezipaměti interně. Pokud umístíte ovládací prvek AdRotator na stránce, vykreslí jedinečné reklamy na každý požadavek, bez ohledu na to, zda je nadřazená stránka uložena do mezipaměti. V důsledku toho je stránka, která obsahuje ovládací prvek AdRotator, pouze na straně serveru uložené v mezipaměti.

## <a name="controlcachepolicy-class"></a>Třída Policy controlCache

Třída ControlCachePolicy umožňuje programové řízení ukládání fragmentů do mezipaměti pomocí uživatelských ovládacích prvků. ASP.NET vloží uživatelské ovládací prvky do instance [BasePartialCachingControl.](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.aspx) Třída BasePartialCachingControl představuje uživatelský ovládací prvek, který má povoleno ukládání výstupu do mezipaměti.

Při přístupu [basePartialCachingControl.CachePolicy](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.cachepolicy.aspx) vlastnost [partialcachingcontrol](https://msdn.microsoft.com/library/system.web.ui.partialcachingcontrol.aspx) ovládacího prvku, vždy obdržíte platný ControlCachePolicy objektu. Pokud však přistupujete k vlastnosti [UserControl.CachePolicy](https://msdn.microsoft.com/library/system.web.ui.usercontrol.cachepolicy.aspx) ovládacího prvku [UserControl,](https://msdn.microsoft.com/library/system.web.ui.usercontrol.aspx) obdržíte platný objekt ControlCachePolicy pouze v případě, že uživatelský ovládací prvek je již zabalen ovládacím prvkem BasePartialCachingControl. Pokud není zabalen, ControlCachePolicy objekt vrácený vlastnost vyvolá výjimky při pokusu o manipulaci s ním, protože nemá přidružené BasePartialCachingControl. Chcete-li zjistit, zda instance UserControl podporuje ukládání do mezipaměti bez generování výjimek, zkontrolujte [vlastnost SupportsCaching.](https://msdn.microsoft.com/library/system.web.ui.controlcachepolicy.supportscaching.aspx)

Použití controlcachepolicy třídy je jedním z několika způsobů, jak povolit ukládání výstupu do mezipaměti. Následující seznam popisuje metody, které můžete použít k povolení ukládání výstupu do mezipaměti:

- Pomocí direktivy [@ OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx) povolte ukládání výstupu do mezipaměti v deklarativních scénářích.
- Pomocí atributu [PartialCachingAttribute](https://msdn.microsoft.com/library/system.web.ui.partialcachingattribute.aspx) povolte ukládání do mezipaměti pro uživatelský ovládací prvek v souboru s kódem na pozadí.
- Pomocí třídy ControlCachePolicy určete nastavení mezipaměti v programových scénářích, ve kterých pracujete s instancemi BasePartialCachingControl, které byly povoleny pro ukládání do mezipaměti pomocí jedné z předchozích metod a dynamicky načteny pomocí metody [System.Web.UI.TemplateControl.LoadControl.](https://msdn.microsoft.com/library/system.web.ui.templatecontrol.loadcontrol.aspx)

A ControlCachePolicy instance lze úspěšně manipulovat pouze mezi Init a PreRender fáze životního cyklu ovládacího prvku. Pokud změníte objekt ControlCachePolicy po fázi PreRender, ASP.NET vyvolá výjimku, protože všechny změny provedené po vykreslení ovládacího prvku nemohou ve skutečnosti ovlivnit nastavení mezipaměti (ovládací prvek je uložen do mezipaměti během fáze Vykreslení). Nakonec instance uživatelského ovládacího prvku (a proto jeho ControlCachePolicy objekt) je k dispozici pouze pro programovou manipulaci, když je skutečně vykreslen.

## <a name="changes-to-caching-configuration---the-ltcachinggt-element"></a>Změny konfigurace ukládání do &lt;mezipaměti&gt; – prvek ukládání do mezipaměti

V ASP.NET 2.0 došlo k několika změnám konfigurace ukládání do mezipaměti. Prvek &lt;ukládání&gt; do mezipaměti je nový v ASP.NET 2.0 a umožňuje provádět změny konfigurace ukládání do mezipaměti v konfiguračním souboru. K dispozici jsou následující atributy.

| **Prvek** | **Popis** |
| --- | --- |
| **Mezipaměti** | Volitelný element. Definuje globální nastavení mezipaměti aplikací. |
| **Outputcache** | Volitelný element. Určuje nastavení výstupní mezipaměti pro celou aplikaci. |
| **outputCacheSettings** | Volitelný element. Určuje nastavení výstupní mezipaměti, které lze použít na stránky v aplikaci. |
| **Sqlcachedependency** | Volitelný element. Konfiguruje závislosti mezipaměti SQL pro ASP.NET aplikaci. |

### <a name="the-ltcachegt-element"></a>Prvek &lt;&gt; mezipaměti

V elementu &lt;mezipaměti&gt; jsou k dispozici následující atributy:

| **Atribut** | **Popis** |
| --- | --- |
| **zakázatkolekcí paměti** | Volitelný **logický** atribut. Získá nebo nastaví hodnotu označující, zda je zakázána kolekce paměti mezipaměti, ke které dochází, když je počítač pod tlakem paměti. |
| **zakázat vypršení platnosti** | Volitelný **logický** atribut. Získá nebo nastaví hodnotu označující, zda je zakázáno vypršení platnosti mezipaměti. Pokud je zakázáno, položky uložené v mezipaměti nevyprší a nedojde k úklidu položek mezipaměti s ukončenou platností. |
| **privateBytesLimit** | Volitelný atribut **Int64.** Získá nebo nastaví hodnotu označující maximální velikost soukromých bajtů aplikace před spuštěním vyprázdnění položek, jejichž platnost vypršela, a pokusem o obnovení paměti. Toto omezení zahrnuje paměť používanou mezipamětí i normální režii paměti ze spuštěné aplikace. Nastavení nula označuje, že ASP.NET bude používat vlastní heuristiku pro určení, kdy začít rekultivovat paměť. |
| **percentagePhysicalMemoryUsedLimit** | Volitelný atribut **Int32.** Získá nebo nastaví hodnotu označující maximální procento fyzické paměti počítače, které může být spotřebováno aplikací před spuštěním vyprázdnění položek, jejichž platnost vypršela, a pokusem o vrácení paměti Toto využití paměti zahrnuje paměť používanou mezipamětí i normální využití paměti spuštěné aplikace. Nastavení nula označuje, že ASP.NET bude používat vlastní heuristiku pro určení, kdy začít rekultivovat paměť. |
| **privateBytesPollTime** | Volitelný atribut **TimeSpan.** Získá nebo nastaví hodnotu označující časový interval mezi dotazování pro využití paměti soukromé bajty aplikace. |

### <a name="the-ltoutputcachegt-element"></a>The &lt;outputCache&gt; Element

Následující atributy jsou k &lt;dispozici&gt; pro element outputCache.

|       <strong>Atribut</strong>        |                                                                                                                                                                                                                                                       <strong>Popis</strong>                                                                                                                                                                                                                                                       |
|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   <strong>enableOutputCache</strong>    |                                                                                                                                                          Volitelný <strong>logický</strong> atribut. Povolí/zakáže výstupní mezipaměť stránky. Pokud je zakázáno, žádné stránky jsou uloženy do mezipaměti bez ohledu na programové nebo deklarativní nastavení. Výchozí hodnota je <strong>true</strong>.                                                                                                                                                           |
|  <strong>enableFragmentCache</strong>   |                                                Volitelný <strong>logický</strong> atribut. Povolí/zakáže mezipaměť fragmentů aplikace. Pokud je zakázáno, žádné stránky jsou uloženy do mezipaměti bez ohledu na [@ OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx) směrnice nebo ukládání do mezipaměti profilu použít. Obsahuje hlavičku řízení mezipaměti, která označuje, že nadřazené proxy servery a klienti prohlížeče by se neměli pokoušet o ukládání výstupu stránky do mezipaměti. Výchozí hodnota je <strong>false</strong>.                                                 |
| <strong>sendCacheControlHeader</strong> |                                                                                                                                                      Volitelný <strong>logický</strong> atribut. Získá nebo nastaví hodnotu označující, zda je <strong>hlavička cache-control:private</strong> ve výchozím nastavení odesílána modulem výstupní mezipaměti. Výchozí hodnota je <strong>false</strong>.                                                                                                                                                      |
|      <strong>omitVaryStar</strong>      | Volitelný <strong>logický</strong> atribut. Povolí/zakáže odesílání<strong>hlavičky \<Http " Vary: /strong><em>" v odpovědi. Při výchozím nastavení false</em>je pro \*výstupní stránky uložené v mezipaměti odesláno záhlaví " *Vary: <strong>". Při odeslání hlavičky Vary umožňuje ukládání různých verzí do mezipaměti na základě toho, co je uvedeno v hlavičce Vary. <em>Například Vary:User-Agents</em> uloží různé verze stránky na základě uživatelského agenta, který žádost vydává. Výchozí hodnota je **false</strong>. |

### <a name="the-ltoutputcachesettingsgt-element"></a>The &lt;outputCacheSettings&gt; Element

Element &lt;outputCacheSettings&gt; umožňuje vytváření profilů mezipaměti, jak bylo popsáno dříve. Jediným podřízeným &lt;prvkem elementu outputCacheSettings&gt; je element &lt;outputCacheProfiles&gt; pro konfiguraci profilů mezipaměti.

### <a name="the-ltsqlcachedependencygt-element"></a>The &lt;sqlCacheDependency&gt; Element

Následující atributy jsou k &lt;dispozici pro&gt; element sqlCacheDependency.

| **Atribut** | **Popis** |
| --- | --- |
| **Povoleno** | Povinný **logický** atribut. Označuje, zda jsou změny dotazovány. |
| **pollTime** | Volitelný atribut **Int32.** Nastaví frekvenci, s jakou sqlcachedependency dotazuje databázové tabulky pro změny. Tato hodnota odpovídá počtu milisekund mezi po sobě jdoucími dotazováními. Nelze nastavit na méně než 500 milisekund. Výchozí hodnota je 1 minuta. |

### <a name="more-information"></a>Další informace

Existují některé další informace, které byste měli znát týkající se konfigurace mezipaměti.

- Pokud není nastaven limit soukromých bajtů pracovního procesu, bude mezipaměť používat jeden z následujících limitů: 

    - x86 2GB: 800 MB nebo 60 % fyzické paměti RAM, podle toho, která hodnota je nižší
    - x86 3GB: 1800MB nebo 60% fyzické paměti RAM, podle toho, co je méně
    - x64: 1 terabajt nebo 60 % fyzické paměti RAM, podle toho, která hodnota je nižší
- Pokud oba pracovní proces soukromé bajty limit a &lt;mezipaměti privateBytesLimit/&gt; jsou nastaveny, mezipaměti bude používat minimálně dva.
- Stejně jako v 1.x, jsme drop cache položky a volání GC. Sbírejte ze dvou důvodů: 

    - Jsme velmi blízko k limitu soukromých bajtů
    - Dostupná paměť je blízko nebo menší než 10%
- Můžete efektivně zakázat trim a cache pro &lt;podmínky nedostatku dostupné paměti&gt; nastavením cache percentagePhysicalMemoryUseLimit/ to 100.
- Na rozdíl od 1.x, 2.0 pozastaví trim a vybírat hovory, pokud poslední GC. Collect nezmenšil soukromé bajty nebo velikost spravovaných hromad o více než 1 % limitu paměti (mezipaměti).

## <a name="lab1-custom-cache-dependencies"></a>Lab1: Vlastní závislosti mezipaměti

1. Vytvořte nový web.
2. Přidejte nový soubor XML s názvem cache.xml a uložte jej do kořenového adresáře webové aplikace.
3. Přidejte následující kód\_do metody Načítání stránky v kódu na pozadí default.aspx: 

    [!code-csharp[Main](caching/samples/sample15.cs)]
4. Ve zdrojovém zobrazení přidejte následující text na začátek souboru default.aspx: 

    [!code-aspx[Main](caching/samples/sample16.aspx)]
5. Procházet default.aspx. Co říká čas?
6. Aktualizujte prohlížeč. Co říká čas?
7. Otevřete soubor cache.xml a přidejte následující kód: 

    [!code-xml[Main](caching/samples/sample17.xml)]
8. Uložit soubor cache.xml.
9. Aktualizujte si stránku v prohlížeči. Co říká čas?
10. Vysvětlete, proč se čas aktualizoval namísto zobrazení dříve uložených hodnot:

## <a name="lab-2-using-polling-based-cache-dependencies"></a>Lab 2: Použití závislostí mezipaměti založených na dotazování

Toto testovací prostředí používá projekt, který jste vytvořili v předchozím modulu, který umožňuje úpravy dat v databázi Northwind prostřednictvím ovládacího prvku GridView a DetailsView.

1. Otevřete projekt v sadě Visual Studio 2005.
2. Spusťte nástroj\_aspnet regsql proti databázi Northwind, abyste povolili databázi a tabulku Products. Použijte následující příkaz z příkazového řádku sady Visual Studio: 

    [!code-console[Main](caching/samples/sample18.cmd)]
3. Do souboru web.config přidejte následující: 

    [!code-xml[Main](caching/samples/sample19.xml)]
4. Přidejte nový webový formulář s názvem showdata.aspx.
5. Na stránku showdata.aspx přidejte následující direktivu @ outputcache: 

    [!code-aspx[Main](caching/samples/sample20.aspx)]
6. Přidejte následující kód\_do stránky Zatížení showdata.aspx: 

    [!code-html[Main](caching/samples/sample21.html)]
7. Přidejte nový ovládací prvek SqlDataSource pro showdata.aspx a nakonfigurujte jej tak, aby používal připojení databáze Northwind. Klikněte na Další.
8. Zaškrtněte políčka ProductName a ProductID a klikněte na Další.
9. Klikněte na Dokončit.
10. Přidejte nový GridView na stránku showdata.aspx.
11. Z rozevíracího souboru zvolte SqlDataSource1.
12. Uložit a procházet showdata.aspx. Poznamenejte si zobrazený čas.
