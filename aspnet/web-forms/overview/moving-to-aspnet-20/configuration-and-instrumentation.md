---
uid: web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
title: Konfigurace a přístrojové vybavení | Dokumenty společnosti Microsoft
author: rick-anderson
description: V ASP.NET 2.0 došlo k významným změnám v konfiguraci a instrumentaci. Nové konfigurační rozhraní API ASP.NET umožňuje provést změny konfigurace pr...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 21ebbaee-7ed8-45ae-b6c1-c27c88342e48
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
msc.type: authoredcontent
ms.openlocfilehash: 30ea2ffd3d055c5373a33615bc19a8f68fb568ab
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543051"
---
# <a name="configuration-and-instrumentation"></a>Konfigurace a instrumentace

podle [společnosti Microsoft](https://github.com/microsoft)

> V ASP.NET 2.0 došlo k významným změnám v konfiguraci a instrumentaci. Nové konfigurační rozhraní API ASP.NET umožňuje provádění změn konfigurace programově. Kromě toho existuje mnoho nových nastavení konfigurace umožňují nové konfigurace a instrumentace.

V ASP.NET 2.0 došlo k významným změnám v konfiguraci a instrumentaci. Nové konfigurační rozhraní API ASP.NET umožňuje provádění změn konfigurace programově. Kromě toho existuje mnoho nových nastavení konfigurace umožňují nové konfigurace a instrumentace.

V tomto modulu budeme diskutovat ASP.NET konfiguračníapi, protože se týká čtení a zápisu do ASP.NET konfiguračních souborů, a budeme také zahrnovat ASP.NET instrumentace. Budeme také zahrnovat nové funkce, které jsou k dispozici v ASP.NET trasování.

## <a name="aspnet-configuration-api"></a>ASP.NET konfigurační rozhraní API

Konfigurační rozhraní API ASP.NET umožňuje vyvíjet, nasazovat a spravovat konfigurační data aplikací pomocí jediného programovacího rozhraní. Konfigurační rozhraní API můžete použít k vývoji a úpravám kompletních konfigurací ASP.NET programově bez přímé úpravy xml v konfiguračních souborech. Kromě toho můžete konfigurační rozhraní API používat v konzolových aplikacích a skriptech, které vyvíjíte, v nástrojích pro správu na webu a v modulech snap-in konzoly MMC (MMC).

Následující dva nástroje pro správu konfigurace používají konfigurační rozhraní API a jsou součástí rozhraní .NET Framework verze 2.0:

- Modul snap-in ASP.NET MMC, který používá konfigurační rozhraní API ke zjednodušení úloh správy a poskytuje integrované zobrazení místních konfiguračních dat ze všech úrovní hierarchie konfigurace.
- Nástroj pro správu webu, který umožňuje spravovat nastavení konfigurace místních a vzdálených aplikací, včetně hostovaných webů.

Konfigurační rozhraní API ASP.NET obsahuje sadu objektů pro správu ASP.NET, které lze použít k programové konfiguraci webových serverů a aplikací. Objekty správy jsou implementovány jako knihovna tříd rozhraní .NET Framework. Konfigurační programovací model rozhraní API pomáhá zajistit konzistenci kódu a spolehlivost vynucením datových typů v době kompilace. Chcete-li usnadnit správu konfigurací aplikací, konfigurační rozhraní API umožňuje zobrazit data, která jsou sloučena ze všech bodů v hierarchii konfigurace jako jednu kolekci, namísto zobrazení dat jako samostatné kolekce z různých konfiguračních souborů. Konfigurační rozhraní API navíc umožňuje manipulovat s celými konfiguracemi aplikací bez přímé úpravy xml v konfiguračních souborech. A konečně rozhraní API zjednodušuje úlohy konfigurace podporou nástrojů pro správu, jako je například Nástroj pro správu webu. Konfigurační rozhraní API zjednodušuje nasazení podporou vytváření konfiguračních souborů v počítači a spouštěním konfiguračních skriptů ve více počítačích.

> [!NOTE]
> Konfigurační rozhraní API nepodporuje vytváření aplikací služby IIS.

## <a name="working-with-local-and-remote-configuration-settings"></a>Práce s místním a vzdáleným nastavením konfigurace

Objekt Configuration představuje sloučené zobrazení nastavení konfigurace, které se vztahuje na určitou fyzickou entitu, například počítač, nebo na logickou entitu, například na aplikaci nebo web. Zadaná logická entita může existovat v místním počítači nebo na vzdáleném serveru. Pokud pro zadanou entitu neexistuje žádný konfigurační soubor, představuje objekt Configuration výchozí nastavení konfigurace definované souborem Machine.config.

Objekt Configuration můžete získat pomocí jedné z metod otevřené konfigurace z následujících tříd:

1. Třída ConfigurationManager, pokud je vaše entita klientskou aplikací.
2. Třída WebConfigurationManager, pokud je vaše entita webovou aplikací.

Tyto metody vrátí Configuration objektu, který zase poskytuje požadované metody a vlastnosti pro zpracování základních konfiguračních souborů. K těmto souborům můžete přistupovat pro čtení nebo zápis.

### <a name="reading"></a>Čtení

Ke čtení informací o konfiguraci slouží metoda GetSection nebo GetSectionGroup. Uživatel nebo proces, který čte, musí mít oprávnění ke čtení pro všechny konfigurační soubory v hierarchii.

> [!NOTE]
> Pokud používáte statickou metodu GetSection, která přebírá parametr cesty, musí parametr cesty odkazovat na aplikaci, ve které je kód spuštěn. V opačném případě je parametr ignorován a jsou vráceny informace o konfiguraci aktuálně spuštěné aplikace.

### <a name="writing"></a>Psaní

K zápisu informací o konfiguraci použijte jednu z metod Save. Uživatel nebo proces, který zapisuje, musí mít oprávnění k zápisu do konfiguračního souboru a adresáře na aktuální úrovni hierarchie konfigurace a také oprávnění ke čtení pro všechny konfigurační soubory v hierarchii.

Chcete-li vygenerovat konfigurační soubor, který představuje zděděné nastavení konfigurace pro zadanou entitu, použijte jednu z následujících metod konfigurace ukládání:

1. Metoda Save pro vytvoření nového konfiguračního souboru.
2. SaveAs Metoda generovat nový konfigurační soubor v jiném umístění.

## <a name="configuration-classes-and-namespaces"></a>Třídy konfigurace a obory názvů

Mnoho konfiguračních tříd a metod jsou navzájem podobné. Následující tabulka popisuje nejčastěji používané konfigurační třídy a obory názvů.

| **Třída konfigurace nebo obor názvů** | **Popis** |
| --- | --- |
| Obor názvů [System.Configuration](https://msdn.microsoft.com/library/system.configuration.aspx) | Obsahuje hlavní třídy konfigurace pro všechny aplikace rozhraní .NET Framework. Třídy obslužné rutiny oddílu se používají k získání konfiguračních dat pro oddíl z metod, jako je například GetSection a GetSectionGroup. Tyto dvě metody jsou nestatické. |
| Třída System.Configuration.Configuration | Představuje sadu konfiguračních dat pro počítač, aplikaci, webový adresář nebo jiný prostředek. Tato třída obsahuje užitečné metody, jako je například GetSection a GetSectionGroup, pro aktualizaci nastavení konfigurace a získání odkazů na oddíly a skupiny oddílů. Tato třída se používá jako návratový typ pro metody, které získávají konfigurační data návrhu, jako jsou například metody tříd WebConfigurationManager a ConfigurationManager. |
| Obor názvů System.Web.Configuration | Obsahuje třídy obslužné rutiny oddílu pro oddíly konfigurace ASP.NET definované v [ASP.NET Nastavení konfigurace](https://msdn.microsoft.com/library/b5ysx397.aspx). Třídy obslužné rutiny oddílu se používají k získání konfiguračních dat pro oddíl z metod, jako je například GetSection a GetSectionGroup. |
| Třída System.Web.Configuration.WebConfigurationManager | Poskytuje užitečné metody pro získání odkazů na nastavení konfigurace za běhu a návrhu. Tyto metody používají třídu System.Configuration.Configuration jako návratový typ. Můžete použít statickou metodu GetSection této třídy nebo nestatickou metodu GetSection třídy System.Configuration.ConfigurationManager zaměnitelně. Pro konfigurace webových aplikací se místo třídy System.Configuration.Configuration.WebConfigurationManager doporučuje třída System.Web.Configuration.WebConfigurationManager. |
| Obor názvů [System.Configuration.Provider](https://msdn.microsoft.com/library/system.configuration.provider.aspx) | Poskytuje způsob, jak přizpůsobit a rozšířit zprostředkovatele konfigurace. Toto je základní třída pro všechny třídy zprostředkovatele v konfiguračním systému. |
| Obor názvů [System.Web.Management](https://msdn.microsoft.com/library/system.web.management.aspx) | Obsahuje třídy a rozhraní pro správu a sledování stavu webových aplikací. Přísně vzato, tento obor názvů není považován za součást konfiguračního rozhraní API. Například trasování a spouštění událostí je provedeno třídv tomto oboru názvů. |
| Obor názvů [System.Management.Instrumentation](https://msdn.microsoft.com/library/system.management.instrumentation.aspx) | Poskytuje třídy nezbytné pro instrumentaci aplikací vystavit jejich informace o správě a události prostřednictvím služby WMI (WMI) potenciálním spotřebitelům. ASP.NET monitorování stavu používá službu WMI k doručování událostí. Přísně vzato, tento obor názvů není považován za součást konfiguračního rozhraní API. |

## <a name="reading-from-aspnet-configuration-files"></a>Čtení z ASP.NET konfiguračních souborů

Třída WebConfigurationManager je základní třídou pro čtení z ASP.NET konfiguračních souborů. Existují v podstatě tři kroky ke čtení ASP.NET konfiguračních souborů:

1. Získejte objekt Configuration pomocí metody OpenWebConfiguration.
2. Získejte odkaz na požadovaný oddíl v konfiguračním souboru.
3. Přečtěte si požadované informace z konfiguračního souboru.

Konfigurační objekt představuje nepředstavuje konkrétní konfigurační soubor. Místo toho představuje sloučené zobrazení konfigurace počítače, aplikace nebo webu. Následující ukázka kódu instancije objekt Configuration představující konfiguraci webové aplikace s názvem *ProductInfo*.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample1.cs)]

> [!NOTE]
> Všimněte si, že pokud cesta /ProductInfo neexistuje, výše uvedený kód vrátí výchozí konfiguraci, jak je zadáno v souboru machine.config.

Jakmile budete mít configuration objekt, pak můžete použít GetSection nebo GetSectionGroup metoda přejít k podrobnostem nastavení konfigurace. Následující příklad získá odkaz na nastavení zosobnění pro výše uvedenou aplikaci ProductInfo:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample2.cs)]

## <a name="writing-to-aspnet-configuration-files"></a>Zápis do konfiguračních souborů ASP.NET

Stejně jako při čtení z konfiguračních souborů je třída WebConfigurationManager jádrem pro zápis do konfiguračních souborů Asp.NET. Existují také tři kroky k zápisu do ASP.NET konfiguračních souborů.

1. Získejte objekt Configuration pomocí metody OpenWebConfiguration.
2. Získejte odkaz na požadovaný oddíl v konfiguračním souboru.
3. Napište požadované informace z konfiguračního souboru pomocí metody Save nebo SaveAs.

Následující kód změní atribut **ladění** &lt;elementu kompilace&gt; na false:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample3.cs)]

Při spuštění tohoto kódu **debug** bude atribut ladění &lt;&gt; elementu kompilace nastaven na hodnotu false pro soubor web.config aplikace *webApp.*

## <a name="systemwebmanagement-namespace"></a>Obor názvů System.Web.Management

Obor názvů System.Web.Management poskytuje třídy a rozhraní pro správu a sledování stavu ASP.NET aplikací.

Protokolování se provádí definováním pravidla, které přidružuje události k poskytovateli. Pravidlo definuje typ událostí, které jsou odesílány zprostředkovateli. K dispozici jsou následující základní události, které můžete protokolovat:

| **Webbaseevent** | Základní třída událostí pro všechny události. Obsahuje požadované vlastnosti pro všechny události, jako je například kód události, kód podrobností události, datum a čas, kdy byla událost vyvolána, pořadové číslo, zpráva události a podrobnosti události. |
| --- | --- |
| **Událost WebManagementEvent** | Základní třída událostí pro události správy, jako je například životnost aplikace, požadavek, chyba a události auditu. |
| **Událost webheartbeat** | Událost generovaná aplikací v pravidelných intervalech pro zachycení užitečných informací o stavu za běhu. |
| **Událost WebAuditEvent** | Základní třída pro události auditu zabezpečení, které se používají k označení podmínek, jako je selhání autorizace, selhání dešifrování *atd.* |
| **WebRequestEvent** | Základní třída pro všechny události informačních požadavků. |
| **WebBaseErrorEvent** | Základní třída pro všechny události označující chybové stavy. |

Typy dostupných zprostředkovatelů umožňují odesílat výstup událostí do Prohlížeče událostí, serveru SQL Server, nástroje WMI (WMI) systému Windows a e-mailu. Předem nakonfigurované zprostředkovatele a mapování událostí snížit množství práce potřebné k získání výstup u událostí zaznamenány.

ASP.NET 2.0 používá zprostředkovatele protokolu událostí out-of-the-box protokolovat události na základě spuštění a zastavení aplikačních domén, stejně jako protokolování všechny neošetřené výjimky. To pomáhá pokrýt některé základní scénáře. Řekněme například, že vaše aplikace vyvolá výjimku, ale uživatel chybu neuloží a nemůžete ji reprodukovat. S výchozím pravidlem protokolu událostí byste mohli shromáždit informace o výjimce a zásobníku, abyste získali lepší představu o tom, k jaké chybě došlo. Jiný příklad platí, pokud vaše aplikace ztrácí stav relace. V takovém případě můžete v protokolu událostí zjistit, zda doména aplikace je recyklace a proč doména aplikace zastavena na prvním místě.

Také systém sledování stavu je rozšiřitelný. Můžete například definovat vlastní webové události, vypálit je v rámci aplikace a pak definovat pravidlo pro odeslání informací o události poskytovateli, jako je váš e-mail. To vám umožní snadno svázat instrumentaci s poskytovateli monitorování stavu. Jako další příklad můžete vypálit událost při každém zpracování objednávky a nastavit pravidlo, které odesílá každou událost do databáze serveru SQL Server. Událost můžete také vypálit, když se uživateli nepodaří přihlásit vícekrát za sebou, a nastavit událost tak, aby používala zprostředkovatele založené na e-mailu.

Konfigurace pro výchozí zprostředkovatele a události je uložena v globálním souboru Web.config. Globální soubor Web.config ukládá všechna webová nastavení uložená v souboru Machine.config v ASP.NET 1x. Globální soubor Web.config je umístěn v následujícím adresáři:

`%windir%\Microsoft.Net\Framework\v2.0.*\config\Web.config`

Část &lt;healthMonitoring&gt; globálního souboru Web.config poskytuje výchozí nastavení konfigurace. Toto nastavení můžete přepsat nebo nakonfigurovat vlastní &lt;nastavení&gt; implementací oddílu healthMonitoring v souboru Web.config pro vaši aplikaci.

Část &lt;healthMonitoring&gt; globálního souboru Web.config obsahuje následující položky:

| **Poskytovatelů** | Obsahuje zprostředkovatele nastavené pro Prohlížeč událostí, Službu WMI a SQL Server. |
| --- | --- |
| **Eventmappings** | Obsahuje mapování pro různé třídy WebBase. Tento seznam můžete rozšířit, pokud vygenerujete vlastní třídu událostí. Generování vlastní třídy událostí poskytuje jemnější rozlišovací schopnost nad zprostředkovateli, které odesíláte informace. Můžete například nakonfigurovat neošetřené výjimky, které mají být odeslány na SQL Server, při odesílání vlastních událostí do e-mailu. |
| **Pravidla** | Propojí eventMappings s poskytovatelem. |
| **Vyrovnávací paměti** | Používá se sql server a poskytovatelé e-mailu k určení, jak často vyprázdnění události zprostředkovatele. |

Níže je uveden příklad kódu z globálního souboru Web.config.

[!code-xml[Main](configuration-and-instrumentation/samples/sample4.xml)]

## <a name="how-to-store-events-to-event-viewer"></a>Jak ukládat události do Prohlížeče událostí

Jak již bylo zmíněno dříve, zprostředkovatel pro protokolování událostí v Prohlížeči událostí je konfigurován pro vás v globálním souboru Web.config. Ve výchozím nastavení jsou protokolovány všechny události založené na **událostech WebBaseErrorEvent** a **WebFailureAuditEvent.** Můžete přidat další pravidla pro protokolování dalších informací do protokolu událostí. Chcete-li například protokolovat všechny události *(tj.* každou událost založenou na **aplikaci WebBaseEvent),** můžete do souboru Web.config přidat následující pravidlo:

[!code-xml[Main](configuration-and-instrumentation/samples/sample5.xml)]

Toto pravidlo by propojilo mapu událostí **Všechny události** s poskytovatelem protokolu událostí. Do globálního souboru Web.config jsou zahrnuty i eventMapping a zprostředkovatel.

## <a name="how-to-store-events-to-sql-server"></a>Jak ukládat události na SQL Server

Tato metoda používá databázi **ASPNETDB,** která je\_generována nástrojem Aspnet regsql.exe. Výchozí zprostředkovatel používá připojovací řetězec LocalSqlServer, který používá\_databázi založenou na souborech ve složce Dat aplikace nebo místní instanci SQLExpress serveru SQL Server. Připojovací řetězec LocalSqlServer i sqlprovider jsou konfigurovány v globálním souboru Web.config.

Připojovací řetězec LocalSqlServer v globálním souboru Web.config vypadá takto:

[!code-xml[Main](configuration-and-instrumentation/samples/sample6.xml)]

Pokud chcete použít jinou instanci serveru SQL Server,\_budete muset použít nástroj Aspnet regsql.exe, který lze nalézt v %windir%\Microsoft.Net\Framework\v2.0. \* složku. Pomocí nástroje Aspnet\_regsql.exe vygenerujte vlastní databázi **ASPNETDB** v instanci serveru SQL Server, přidejte připojovací řetězec do konfiguračního souboru aplikací a potom přidejte zprostředkovatele pomocí nového připojovacího řetězce. Jakmile budete mít vytvořenou databázi **ASPNETDB,** budete muset nastavit pravidlo pro propojení eventMapping u sqlProvider.

Bez ohledu na to, zda používáte výchozího zprostředkovatele SqlProvider nebo nakonfigurujete vlastního zprostředkovatele, budete muset přidat pravidlo spojující zprostředkovatele s mapou událostí. Následující pravidlo propojuje nového zprostředkovatele, kterého jste vytvořili výše, s mapou událostí **Všechny události.** Toto pravidlo zaprotokoluje všechny události založené na **WebBaseEvent** a odešle je mysqlwebeventprovideru, který použije připojovací řetězec MYASPNETDB. Následující kód přidá pravidlo pro propojení zprostředkovatele s mapou událostí:

[!code-xml[Main](configuration-and-instrumentation/samples/sample7.xml)]

Pokud chcete odesílat chyby pouze na SQL Server, můžete přidat následující pravidlo:

[!code-xml[Main](configuration-and-instrumentation/samples/sample8.xml)]

## <a name="how-to-forward-events-to-wmi"></a>Jak předávat události do wmi

Události můžete také předat do systému WMI. Zprostředkovatel služby WMI je ve výchozím nastavení nakonfigurován v globálním souboru Web.config.

Následující příklad kódu přidá pravidlo pro předávání událostí do služeb WMI:

[!code-xml[Main](configuration-and-instrumentation/samples/sample9.xml)]

Budete muset přidat pravidlo pro přidružení eventMapping k poskytovateli a také naslouchací proces služby WMI aplikace naslouchat události. Následující příklad kódu přidá pravidlo pro propojení zprostředkovatele služby WMI s mapou událostí **Všechny události:**

[!code-xml[Main](configuration-and-instrumentation/samples/sample10.xml)]

## <a name="how-to-forward-events-to-email"></a>Jak přeposlat události na e-mail

Události můžete také přeposlat e-mailem. Buďte opatrní, která pravidla událostí mapujete na poskytovatele e-mailu, protože můžete neúmyslně odeslat mnoho informací, které mohou být vhodnější pro SQL Server nebo protokol událostí. Existují dva poskytovatelé e-mailu; SimpleMailWebEventProvider a TemplatedMailWebEventProvider. Každý z nich má stejné atributy konfigurace, s výjimkou atributů "template" a "detailedTemplateErrors", které jsou k dispozici pouze na TemplatedMailWebEventProvider.

> [!NOTE]
> Ani jeden z těchto poskytovatelů e-mailu není nakonfigurován pro vás. Budete je muset přidat do souboru Web.config.

Hlavní rozdíl mezi těmito dvěma poskytovateli e-mailu spočine na to, že SimpleMailWebEventProvider odesílá e-maily v obecné šabloně, kterou nelze změnit. Ukázkový soubor Web.config přidá tohoto poskytovatele e-mailu do seznamu nakonfigurovaných zprostředkovatelů pomocí následujícího pravidla:

[!code-xml[Main](configuration-and-instrumentation/samples/sample11.xml)]

Pro vazbu poskytovatele e-mailu s mapou událostí **Všechny události** je také přidáno následující pravidlo:

[!code-xml[Main](configuration-and-instrumentation/samples/sample12.xml)]

## <a name="aspnet-20-tracing"></a>ASP.NET 2.0 Trasování

Existují tři hlavní vylepšení trasování v ASP.NET 2.0.

1. Funkce integrovaného trasování
2. Programový přístup ke trasovacím zprávám
3. Vylepšené trasování na úrovni aplikace

## <a name="integrated-tracing-functionality"></a>Funkce integrovaného trasování

Nyní můžete směrovat zprávy vyzařované třídou System.Diagnostics.Trace do ASP.NET výstupu trasování a směrovat zprávy vysílané ASP.NET trasování na System.Diagnostics.Trace. Události ASP.NET instrumentace můžete také předat systému System.Diagnostics.Trace. Tato funkce je poskytována nový **writeToDiagnosticsTrace** &lt;atribut&gt; trace element. Pokud je tato logická hodnota true, ASP.NET trasovací zprávy jsou předány system.diagnostics trasování infrastruktury pro všechny naslouchací procesy, které jsou registrovány k zobrazení trasovacích zpráv.

## <a name="programmatic-access-to-trace-messages"></a>Programový přístup ke stopovým zprávám

ASP.NET 2.0 umožňuje programový přístup ke všem trasovacím zprávám prostřednictvím třídy **TraceContextRecord** a kolekce **TraceRecords.** Nejúčinnější způsob přístupu ke zprávám trasování je zaregistrovat delegáta **TraceContextEventHandler** (také nový v ASP.NET 2.0) pro zpracování nové události **TraceFinished.** Potom můžete smyčku prostřednictvím trasovacích zpráv, jak si přejete.

Následující ukázka kódu ilustruje toto:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample13.cs)]

Ve výše uvedeném příkladu jsem smyčka prostřednictvím TraceRecords kolekce a potom zapsat každou zprávu do datového proudu odpovědi.

## <a name="improved-application-level-tracing"></a>Vylepšené trasování na úrovni aplikací

Trasování na úrovni aplikace je vylepšeno zavedením nového&gt; atributu **mostRecent** prvku &lt;trace. Tento atribut určuje, zda je zobrazen nejnovější výstup trasování na úrovni aplikace a starší data trasování za limity, které jsou označeny requestLimit jsou zahozeny. Pokud false, data trasování jsou zobrazeny pro požadavky, dokud requestLimit atribut je dosaženo.

## <a name="aspnet-command-line-tools"></a>nástroje ASP.NET příkazového řádku

Existuje několik nástrojů příkazového řádku, které pomáhají při konfiguraci ASP.NET. ASP.NET vývojáři by měli být\_obeznámeni s nástrojem aspnet regiis.exe. ASP.NET 2.0 poskytuje tři další nástroje příkazového řádku, které pomáhají v konfiguraci.

K dispozici jsou následující nástroje příkazového řádku:

| **Nástroj** | **Použití** |
| --- | --- |
| **aspnet\_regiis.exe** | Umožňuje registraci ASP.NET se su-iis. Existují dvě verze těchto nástrojů, které jsou dodávány s ASP.NET 2.0, jeden pro 32bitové systémy (ve složce Framework) a jeden pro 64bitové systémy (ve složce Framework64).) 64bitová verze nebude nainstalována v 32bitovém os. |
| **aspnet\_regsql.exe** | Nástroj ASP.NET registrace serveru SQL Server slouží k vytvoření databáze serveru Microsoft SQL Server pro použití zprostředkovateli serveru SQL Server v ASP.NET nebo k přidání nebo odebrání možností z existující databáze. Soubor Aspnet\_regsql.exe je umístěn ve složce [drive:]\WINDOWS\Microsoft.NET\Framework\versionNumber na webovém serveru. |
| **aspnet\_regbrowsers.exe** | Nástroj ASP.NET registrace prohlížeče analyzuje a zkompiluje všechny definice prohlížeče v celém systému do sestavení a nainstaluje sestavení do globální mezipaměti sestavení. Nástroj používá definiční soubory prohlížeče (. prohlížeče) z podadresáře prohlížečů .NET Framework. Nástroj naleznete v adresáři %SystemRoot%\Microsoft.NET\Framework\version\. |
| **soubor compiler.exe aspnet\_** | Nástroj ASP.NET kompilace umožňuje zkompilovat ASP.NET webovou aplikaci, a to buď na místě, nebo pro nasazení do cílového umístění, například produkčního serveru. Místní kompilace pomáhá výkon aplikace, protože koncoví uživatelé nenarazí na zpoždění při prvním požadavku na aplikaci, zatímco aplikace je kompilován. |

Vzhledem k\_tomu, že nástroj aspnet regiis.exe není pro ASP.NET 2.0 nový, nebudeme o tom zde diskutovat.

## <a name="aspnet-sql-server-registration-tool---aspnet_regsqlexe"></a>ASP.NET nástroj pro registraci\_serveru SQL Server - aspnet regsql.exe

Pomocí nástroje ASP.NET registrace serveru SQL Server můžete nastavit několik typů možností. Můžete zadat připojení SQL, určit, které ASP.NET aplikační služby používají SQL Server ke správě informací, označit, která databáze nebo tabulka se používá pro závislost mezipaměti SQL, a přidat nebo odebrat podporu pro použití serveru SQL Server k ukládání procedur a stavu relace.

Několik ASP.NET aplikačních služeb spoléhá na poskytovatele při správě ukládání a načítání dat ze zdroje dat. Každý zprostředkovatel je specifický pro zdroj dat. ASP.NET zahrnuje zprostředkovatele serveru SQL Server pro následující funkce ASP.NET:

- Členství (třída [SqlMembershipProvider).](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx)
- Správa rolí (třída [SqlRoleProvider).](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx)
- Profil (třída [SqlProfileProvider).](https://msdn.microsoft.com/library/system.web.profile.sqlprofileprovider.aspx)
- Individuální nastavení webových částí (třída [SqlPersonalizationProvider).](https://msdn.microsoft.com/library/system.web.ui.webcontrols.webparts.sqlpersonalizationprovider.aspx)
- Webové události (třída [SqlWebEventProvider).](https://msdn.microsoft.com/library/system.web.management.sqlwebeventprovider.aspx)

Při instalaci ASP.NET obsahuje soubor Machine.config pro váš server konfigurační prvky, které určují zprostředkovatele serveru SQL Server pro každou ASP.NET funkcí, které jsou závislé na zprostředkovateli. Tito zprostředkovatelé jsou ve výchozím nastavení konfigurováni pro připojení k místní instanci uživatele serveru SQL Server Express 2005. Pokud změníte výchozí připojovací řetězec používaný zprostředkovateli, pak před použitím některé z ASP.NET funkcí nakonfigurovaných v konfiguraci počítače,\_je nutné nainstalovat databázi serveru SQL Server a databázové prvky pro vybranou funkci pomocí souboru Aspnet regsql.exe. Pokud databáze, kterou zadáte pomocí registračního nástroje SQL, ještě neexistuje (aspnetdb bude výchozí databáze, pokud není zadána na příkazovém řádku), musí mít aktuální uživatel práva k vytváření databází na serveru SQL Server a také k vytváření prvků schématu v databázi.

### <a name="sql-cache-dependency"></a>Závislost mezipaměti SQL

Pokročilou funkcí ukládání do mezipaměti výstupu ASP.NET je závislost mezipaměti SQL. Závislost mezipaměti SQL podporuje dva různé provozní režimy: jeden, který používá ASP.NET implementaci dotazování tabulek a druhý režim, který používá funkce oznámení dotazu serveru SQL Server 2005. Registrační nástroj SQL lze použít ke konfiguraci režimu dotazování tabulek.

### <a name="session-state"></a>Stav relace

Ve výchozím nastavení jsou hodnoty stavu relace a informace uloženy v paměti v rámci procesu ASP.NET. Případně můžete data relace uložit do databáze serveru SQL Server, kde je může sdílet více webových serverů. Pokud databáze, kterou zadáte pro stav relace pomocí nástroje pro registraci SQL, ještě neexistuje, musí mít aktuální uživatel práva k vytváření databází na serveru SQL Server a také k vytváření prvků schématu v databázi. Pokud databáze existuje, musí mít aktuální uživatel práva k vytvoření prvků schématu v existující databázi.

Chcete-li nainstalovat databázi stavu relace na\_serveru SQL Server, spusťte nástroj Aspnet regsql.exe a zařaďte příkaz následující informace:

- Název instance serveru SQL Server pomocí možnosti **-S.**
- Přihlašovací pověření pro účet, který má oprávnění k vytvoření databáze v počítači se systémem SQL Server. Pomocí možnosti **-E** můžete použít aktuálně přihlášeného uživatele nebo pomocí možnosti **-U** určit ID uživatele spolu s volbou **-P** k zadání hesla.
- Možnost příkazového řádku **-ssadd** pro přidání databáze stavu relace.

Ve výchozím nastavení nelze použít\_nástroj Aspnet regsql.exe k instalaci databáze stavu relace do počítače se systémem SQL Server 2005 Express Edition.

### <a name="the-aspnet-browser-registration-tool---aspnet_regbrowsersexe"></a>Nástroj pro registraci prohlížeče\_ASP.NET - aspnet regbrowsers.exe

V ASP.NET verze 1.1 obsahoval soubor Machine.config &lt;oddíl&gt;s názvem browserCaps . Tato část obsahovala řadu položek XML, které definovaly konfigurace pro různé prohlížeče na základě regulárního výrazu. Pro ASP.NET verze 2.0 nový . Soubor prohlížeče definuje parametry konkrétního prohlížeče pomocí položek XML. Informace v novém prohlížeči přidáte přidáním nového . Soubor prohlížeče do složky umístěné na adrese %SystemRoot%\Microsoft.NET\Framework\version\CONFIG\Browsers v systému.

Vzhledem k tomu, že aplikace nečte soubor .config pokaždé, když vyžaduje informace o prohlížeči, můžete vytvořit nový soubor . prohlížeč a spustit Aspnet\_regbrowsers.exe přidat požadované změny do sestavení. To umožňuje serveru přístup k nové informace o prohlížeči okamžitě, takže nemusíte vypnout žádné z vašich aplikací vyzvednout informace. Aplikace může přistupovat k možnostem prohlížeče prostřednictvím vlastnosti Browser aktuálního httprequest.

Při spuštění souboru aspnet\_regbrowser.exe jsou k dispozici následující možnosti:

| **Možnost** | **Popis** |
| --- | --- |
| **-?** | Zobrazí text nápovědy Aspnet\_regbbrowsers.exe v příkazovém okně. |
| **-i** | Vytvoří sestavení schopností prohlížeče za běhu a nainstaluje jej do globální mezipaměti sestavení. |
| **-u** | Odinstaluje sestavení schopností prohlížeče za běhu z globální mezipaměti sestavení. |

## <a name="the-aspnet-compilation-tool---aspnet_compilerexe"></a>Nástroj pro kompilaci ASP.NET\_- aspnet compiler.exe

Nástroj ASP.NET kompilace lze použít dvěma obecnými způsoby: pro kompilaci na místě a kompilaci pro nasazení, kde je určen cílový výstupní adresář.

### <a name="compiling-an-application-in-place"></a>[Kompilace aplikace na místě](https://msdn.microsoft.com/library/ms229863.aspx)

Nástroj ASP.NET kompilace může zkompilovat aplikaci na místě, to znamená, že napodobuje chování provádění více požadavků na aplikaci, což způsobuje pravidelnou kompilaci. Uživatelé předem zkompilovaného webu nezaznamená zpoždění způsobené kompilací stránky na první žádost.

Při předkompilaci webu na místě platí následující položky:

- Web si zachová své soubory a adresářovou strukturu.
- Musíte mít kompilátory pro všechny programovací jazyky používané webem na serveru.
- Pokud některý soubor selže kompilace, celý web selže kompilace.

Můžete také překompilovat aplikaci na místě po přidání nových zdrojových souborů do ní. Nástroj zkompiluje pouze nové nebo změněné soubory, pokud nezahrnete možnost **-c.**

> [!NOTE]
> Kompilace aplikace, která obsahuje vnořenou aplikaci, nezkompiluje vnořenou aplikaci. Vnořená aplikace musí být kompilován samostatně.

### <a name="compiling-an-application-for-deployment"></a>[Kompilace aplikace pro nasazení](https://msdn.microsoft.com/library/ms229863.aspx)

Zkompilovat aplikaci pro nasazení (kompilace do cílového umístění) zadáním parametru targetDir. TargetDir může být konečné umístění pro webovou aplikaci nebo kompilované aplikace lze dále nasadit. Pomocí možnosti **-u** zkompiluje aplikaci takovým způsobem, že můžete provádět změny určitých souborů v kompilované aplikaci bez jeho opětovné kompilace. Soubor Aspnet\_compiler.exe rozlišuje mezi statickými a dynamickými typy souborů a při vytváření výsledné aplikace je zpracovává odlišně.

- Statické typy souborů jsou ty, které nemají přidružený kompilátor nebo zprostředkovatele sestavení, například soubory, jejichž název má přípony, například .css, .gif, .htm, .html, .jpg, .js a tak dále. Tyto soubory jsou jednoduše zkopírovány do cílového umístění, s jejich relativní místa ve struktuře adresáře zachována.
- Dynamické typy souborů jsou ty, které mají přidružený kompilátor nebo zprostředkovatelsestavení, včetně souborů s přípony názvů specifických pro ASP.NET, jako je asax, ascx, ashx, .aspx, .browser, .master a tak dále. Nástroj kompilace ASP.NET generuje sestavení z těchto souborů. Pokud je volba **-u** vynechána, nástroj také vytvoří soubory s příponou názvu souboru . KOMPILOVANÉ, které mapují původní zdrojové soubory na jejich sestavení. Chcete-li zajistit zachování struktury adresáře zdroje aplikace, nástroj generuje zástupné soubory v odpovídajících umístěních v cílové aplikaci.

Je nutné použít **-u** možnost označit, že obsah kompilované aplikace lze upravit. V opačném případě jsou následné změny ignorovány nebo způsobit chyby za běhu.

Následující tabulka popisuje, jak nástroj ASP.NET kompilace zpracovává různé typy souborů, když je zahrnuta možnost **-u.**

| **Typ souboru** | **Akce kompilátoru** |
| --- | --- |
| .ascx, .aspx, .master | Tyto soubory jsou rozděleny do značky a zdrojový kód, který zahrnuje jak &lt;kód na pozadí&gt; soubory a jakýkoli kód, který je uzavřen ve skriptu runat = "server" prvky. Zdrojový kód je kompilován do sestavení s názvy, které jsou odvozeny z algoritmu hash a sestavení jsou umístěny v adresáři Bin. Jakýkoli vložkový kód, to ** &lt; ** znamená ** % ** kód uzavřený mezi závorkami a, je součástí značky a není kompilován. Nové soubory se stejným názvem jako zdrojové soubory jsou vytvořeny tak, aby obsahovaly značky a umístěny do odpovídajících výstupních adresářů. |
| .ashx, .asmx | Tyto soubory nejsou kompilovány a jsou přesunuty do výstupních adresářů tak, jak jsou a nejsou kompilovány. Pokud chcete mít kód obslužné rutiny zkompilován, umístěte kód do souborů zdrojového kódu v adresáři Kód aplikace.\_ |
| .cs, .vb, .jsl, .cpp (bez souborů s kódem na pozadí pro výše uvedené typy souborů) | Tyto soubory jsou kompilovány a zahrnuty jako prostředek v sestaveních, které na ně odkazují. Zdrojové soubory nejsou zkopírovány do výstupního adresáře. Pokud soubor kódu není odkazován, není zkompilován. |
| Vlastní typy souborů | Tyto soubory nejsou kompilovány. Tyto soubory jsou zkopírovány do odpovídajících výstupních adresářů. |
| Soubory zdrojového kódu\_v podadresáři Kód aplikace | Tyto soubory jsou zkompilovány do sestavení a umístěny do adresáře Bin. |
| Soubory Resx a .resource\_v podadresáři App GlobalResources | Tyto soubory jsou zkompilovány do sestavení a umístěny do adresáře Bin. V\_hlavním výstupním adresáři není vytvořen žádný podadresář App GlobalResources a do výstupních adresářů se nezkopírují žádné soubory Resx nebo .resources umístěné ve zdrojovém adresáři. |
| Soubory Resx a .resource\_v podadresáři App LocalResources | Tyto soubory nejsou kompilovány a jsou zkopírovány do odpovídajících výstupních adresářů. |
| Soubory .skin v\_podadresáři Témata aplikace | Soubory .skin a statické soubory motivů nejsou zkompilovány a jsou zkopírovány do odpovídajících výstupních adresářů. |
| Statické typy souborů .browser Web.config Sestavení, která jsou již v adresáři Bin k dispozici | Tyto soubory jsou zkopírovány stejně jako do výstupních adresářů. |

Následující tabulka popisuje, jak nástroj ASP.NET kompilace zpracovává různé typy souborů, když je možnost **-u** vynechána.

| **Typ souboru** | **Akce kompilátoru** |
| --- | --- |
| .aspx, .asmx, .ashx, .master | Tyto soubory jsou rozděleny do značky a zdrojový kód, který zahrnuje jak &lt;kód na pozadí&gt; soubory a jakýkoli kód, který je uzavřen ve skriptu runat = "server" prvky. Zdrojový kód je kompilován do sestavení s názvy, které jsou odvozeny z algoritmu hash. Výsledná sestavení jsou umístěna v adresáři Bin. Jakýkoli vložkový kód, to ** &lt; ** znamená ** % ** kód uzavřený mezi závorkami a, je součástí značky a není kompilován. Kompilátor vytvoří nové soubory, které budou obsahovat značky se stejným názvem jako zdrojové soubory. Tyto výsledné soubory jsou umístěny v adresáři Bin. Kompilátor také vytváří soubory se stejným názvem jako zdrojové soubory, ale s příponou . KOMPILOVANÉ, které obsahují informace o mapování. Tá. KOMPILOVANÉ soubory jsou umístěny ve výstupních adresářích odpovídajících původnímu umístění zdrojových souborů. |
| Ascx | Tyto soubory jsou rozděleny do značky a zdrojový kód. Zdrojový kód je zkompilován do sestavení a umístěn do adresáře Bin s názvy, které jsou odvozeny z algoritmu hash. Nejsou generovány žádné soubory značek. |
| .cs, .vb, .jsl, .cpp (bez souborů s kódem na pozadí pro výše uvedené typy souborů) | Zdrojový kód, na který odkazují sestavení vygenerovaná ze souborů ASCX, ASHX nebo ASPX, je zkompilován do sestavení a umístěn do adresáře Bin. Nejsou zkopírovány žádné zdrojové soubory. |
| Vlastní typy souborů | Tyto soubory jsou kompilovány jako dynamické soubory. V závislosti na typu souboru, na kterých jsou založeny, může kompilátor umístit soubory mapování do výstupních adresářů. |
| Soubory v\_podadresáři Kód aplikace | Soubory zdrojového kódu v tomto podadresáři jsou kompilovány do sestavení a umístěny do adresáře Bin. |
| Soubory v\_podadresáři App GlobalResources | Tyto soubory jsou zkompilovány do sestavení a umístěny do adresáře Bin. V\_hlavním výstupním adresáři není vytvořen žádný podadresář App GlobalResources. Pokud konfigurační soubor určuje appliesTo="All", soubory .resx a .resources se zkopírují do výstupních adresářů. Nejsou zkopírovány, pokud jsou odkazovány [BuildProvider](https://msdn.microsoft.com/library/system.web.configuration.buildprovider.aspx). |
| Soubory Resx a .resource\_v podadresáři App LocalResources | Tyto soubory jsou kompilovány do sestavení s jedinečnými názvy a umístěny do adresáře Bin. Do výstupních adresářů nejsou zkopírovány žádné soubory Resx nebo .resource. |
| Soubory .skin v\_podadresáři Témata aplikace | Motivy jsou kompilovány do sestavení a umístěny do adresáře Bin. Soubory se zakázaným inzerováním jsou vytvořeny pro soubory .skin a umístěny do odpovídajícího výstupního adresáře. Statické soubory (například CSS) jsou zkopírovány do výstupních adresářů. |
| Statické typy souborů .browser Web.config Sestavení, která jsou již v adresáři Bin k dispozici | Tyto soubory jsou zkopírovány stejně jako do výstupního adresáře. |

### <a name="fixed-assembly-names"></a>[Pevné názvy sestavení](https://msdn.microsoft.com/library/ms229863.aspx##)

Některé scénáře, například nasazení webové aplikace pomocí Instalační služby systému Windows MSI, vyžadují použití konzistentních názvů souborů a obsahu a konzistentních adresářových struktur k identifikaci sestavení nebo nastavení konfigurace aktualizací. V těchto případech můžete použít **-fixednames** možnost určit, že nástroj ASP.NET kompilace by měl zkompilovat sestavení pro každý zdrojový soubor namísto použití kde jsou kompilovány více stránek do sestavení. To může vést k velkému počtu sestavení, takže pokud se obáváte škálovatelnosti, měli byste tuto možnost používat opatrně.

### <a name="strong-name-compilation"></a>[Kompilace silného názvu](https://msdn.microsoft.com/library/ms229863.aspx##)

Možnosti **-aptca**, **-delaysign**, **-keycontainer** a **-keyfile** jsou k\_dispozici, takže můžete použít soubor Aspnet compiler.exe k vytvoření silně pojmenovaných sestavení bez použití [nástroje Silný název (Sn.exe)](https://msdn.microsoft.com/library/k5b5tt23.aspx) samostatně. Tyto možnosti odpovídají atributu **AllowPartiallyTrustedCallersAttribute**, **AssemblyDelaySignAttribute**, **AssemblyKeyNameAttribute**a **AssemblyKeyFileAttribute**.

Diskuse o těchto atributů je mimo rozsah tohoto kurzu.

## <a name="labs"></a>Testovací prostředí

Každá z následujících laboratoří vychází z předchozích testovacích prostředí. Budete je muset udělat v pořádku.

## <a name="lab-1-using-the-configuration-api"></a>Lab 1: Použití konfiguračního rozhraní API

1. Vytvořte nový web s názvem *mod9lab*.
2. Přidejte na web nový webový konfigurační soubor.
3. Do souboru web.config přidejte následující:

[!code-xml[Main](configuration-and-instrumentation/samples/sample14.xml)]

Tím zajistíte oprávnění k ukládání změn do souboru web.config.

1. Přidejte nový ovládací prvek Label do souboru Default.aspx a změňte ID na **lblDebugStatus**.
2. Přidejte nový ovládací prvek Button do souboru Default.aspx.
3. Změňte ID ovládacího prvku Button na **btnToggleDebug** a text **přepnout stav ladění**.
4. Otevřete zobrazení kódu pro soubor default.aspx na pozadí kódu a přidejte **příkaz using** pro **soubor System.Web.Configuration** následujícím způsobem:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample15.cs)]

1. Přidejte do třídy dvě soukromé\_proměnné a metodu Page Init, jak je znázorněno níže:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample16.cs)]

1. Přidejte do načtení stránky\_následující kód:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample17.cs)]

1. Uložit a procházet default.aspx. Všimněte si, že ovládací prvek Label zobrazuje aktuální stav ladění.
2. Poklepejte na ovládací prvek Button v návrháři a přidejte následující kód do události Click pro ovládací prvek Button:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample18.cs)]

1. Uložte a procházejte výchozí soubor ASPX a klepněte na tlačítko.
2. Po každém kliknutí na tlačítko otevřete soubor web.config &lt;&gt; a dodržujte atribut **ladění** v části kompilace.

## <a name="lab-2-logging-application-restarts"></a>Lab 2: Protokolování aplikace restartuje

V tomto testovacím prostředí vytvoříte kód, který vám umožní přepnout protokolování vypnutí aplikací, spuštění a rekompilace v Prohlížeči událostí.

1. Přidejte DropDownList na default.aspx a změňte ID na ddlLogAppEvents.
2. Nastavte vlastnost **AutoPostBack** pro dropdownlist na **hodnotu true**.
3. Přidejte tři položky do kolekce Položky pro DropDownList. Vytvořte **text** pro první položku *Vybrat hodnotu* a hodnotu -1. Text **a** **hodnotu** druhé položky načiní **hodnotou true** a **text** a **hodnota** třetí položky **False**.
4. Přidejte nový popisek do default.aspx. Změňte ID na **lblLogAppEvents**.
5. Otevřete zobrazení s kódem na pozadí pro default.aspx a přidejte novou deklaraci pro proměnnou typu HealthMonitoringSection, jak je znázorněno níže:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample19.cs)]

1. Přidejte do existujícího kódu\_v aplikaci Page Init následující kód:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample20.cs)]

1. Poklepejte na DropDownList a přidejte následující kód do události SelectedIndexChanged:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample21.cs)]

1. Procházet default.aspx.
2. Nastavte rozevírací hodnotu na **hodnotu False**.
3. Zrušte zaškrtnutí protokolu aplikací v Prohlížeči událostí.
4. Klepnutím na tlačítko změníte atribut Ladění aplikace.
5. Aktualizujte protokol aplikace v Prohlížeči událostí. 

    1. Byly zaznamenány nějaké události?
    2. Proč nebo proč ne?
6. Nastavte rozevírací hodnotu na **Hodnotu True.**
7. Klepnutím na tlačítko přepnete atribut Ladění aplikace.
8. Aktualizujte přihlášení aplikace do Prohlížeče událostí. 

    1. Byly zaznamenány nějaké události?
    2. Jaký byl důvod pro vypnutí aplikace?
9. Experimentujte se zapnutím a vypnutím protokolování a podívejte se na změny provedené v souboru web.config.

## <a name="more-information"></a>Více informací:

ASP.NET model poskytovatele 2.0 umožňuje vytvářet vlastní poskytovatele nejen pro aplikační instrumentaci, ale i pro mnoho dalších použití, jako je členství, profily atd. Podrobné informace o psaní vlastního zprostředkovatele pro protokolování událostí aplikace do textového souboru naleznete na [tomto odkazu](https://msdn.microsoft.com/library/default.asp?url=/library/dnaspp/html/ASPNETProvMod_Prt6.asp).
