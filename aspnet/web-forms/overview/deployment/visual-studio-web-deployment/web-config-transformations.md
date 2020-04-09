---
uid: web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
title: 'ASP.NET nasazení webu pomocí sady Visual Studio: Transformace souborů Web.config | Dokumenty společnosti Microsoft'
author: tdykstra
description: Tato série kurzů ukazuje, jak nasadit (publikovat) ASP.NET webovou aplikaci do webových aplikací Služby App Service Azure nebo poskytovateli hostingu třetí strany, usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 5a2a927b-14cb-40bc-867a-f0680f9febd7
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
msc.type: authoredcontent
ms.openlocfilehash: a9d39547c94a63003442ba6fe1257693dde24b05
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676123"
---
# <a name="aspnet-web-deployment-using-visual-studio-webconfig-file-transformations"></a>ASP.NET nasazení webu pomocí sady Visual Studio: Transformace souborů Web.config

podle [Tom Dykstra](https://github.com/tdykstra)

[Stáhnout počáteční projekt](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> Tato série kurzů ukazuje, jak nasadit (publikovat) ASP.NET webové aplikace do Webových aplikací služby Azure App Service nebo poskytovateli hostingu třetí strany pomocí Visual Studia 2012 nebo Visual Studia 2010. Informace o sérii naleznete [v prvním kurzu v sérii](introduction.md).

## <a name="overview"></a>Přehled

Tento kurz ukazuje, jak automatizovat proces změny souboru *Web.config* při jeho nasazení do různých cílových prostředí. Většina aplikací má v souboru *Web.config* nastavení, která se při nasazení aplikace musí lišit. Automatizace procesu provádění těchto změn zabrání nutnosti provádět je ručně při každém nasazení, což by bylo únavné a náchylné k chybám.

Připomenutí: Pokud se vám zobrazí chybová zpráva nebo něco nefunguje, když procházíte kurzem, nezapomeňte se podívat na [stránku pro řešení potíží](troubleshooting.md).

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a>Transformace web.config versus parametry nasazení webu

Proces změny nastavení souboru *Web.config* lze automatizovat dvěma [způsoby: transformace web.config](https://msdn.microsoft.com/library/dd465326.aspx) a [parametry nasazení webu](https://msdn.microsoft.com/library/ff398068.aspx). Transformační soubor *Web.config* obsahuje značky XML, které určují, jak změnit soubor *Web.config* při jeho nasazení. Můžete zadat různé změny pro konkrétní konfigurace sestavení a pro konkrétní profily publikování. Výchozí konfigurace sestavení jsou Ladění a vydání a můžete vytvořit vlastní konfigurace sestavení. Profil publikování obvykle odpovídá cílovému prostředí. (Další informace o publikování profilů najdete v kurzu [Nasazení do služby IIS jako testovacího prostředí.)](deploying-to-iis.md)

Parametry nasazení webu lze použít k určení mnoha různých druhů nastavení, které musí být nakonfigurovány během nasazení, včetně nastavení, která se nacházejí v souborech *Web.config.* Při použití k určení změn souborů *Web.config* jsou parametry nasazení webu složitější, ale jsou užitečné, pokud neznáte hodnotu, která má být nastavena, dokud nenasadíte. Například v podnikovém prostředí můžete vytvořit *balíček nasazení* a předat jej osobě v oddělení IT k instalaci v produkčním prostředí a tato osoba musí být schopna zadat připojovací řetězce nebo hesla, která neznáte.

Pro scénář, který tato série kurzů pokrývá, víte předem vše, co je třeba udělat pro soubor *Web.config,* takže není nutné používat parametry nasazení webu. Nakonfigurujete některé transformace, které se liší v závislosti na použité konfiguraci sestavení a některé, které se liší v závislosti na použitém profilu publikování.

<a id="watransforms"></a>

## <a name="specifying-webconfig-settings-in-azure"></a>Určení nastavení web.config v Azure

Pokud nastavení souboru *Web.config,* které chcete `<connectionStrings>` změnit, jsou v `<appSettings>` prvku nebo a pokud nasazujete do webových aplikací ve službě Azure App Service, máte další možnost automatizace změn během nasazení. Nastavení, která se mají projevit v Azure, můžete zadat na kartě **Konfigurace** na stránce portálu pro správu webové aplikace (přejděte dolů k **části nastavení aplikace** a **připojovacích řetězců).** Když nasadíte projekt, Azure automaticky použije změny. Další informace naleznete v [tématu Weby Windows Azure: Jak fungují aplikační řetězce a připojovací řetězce](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx).

## <a name="default-transformation-files"></a>Výchozí transformační soubory

V **Průzkumníku řešení**rozbalte *web.config,* abyste viděli transformační soubory *Web.Debug.config* a *Web.Release.config,* které jsou ve výchozím nastavení vytvořeny pro dvě výchozí konfigurace sestavení.

![Web.config_transform_files](web-config-transformations/_static/image1.png)

Transformační soubory pro vlastní konfigurace sestavení můžete vytvořit tak, že klepnete pravým tlačítkem myši na soubor Web.config a z kontextové nabídky zvolíte **Přidat transformace konfigurace.** Pro účely tohoto kurzu to nemusíte dělat a možnost nabídky je zakázána, protože jste nevytvořili žádné vlastní konfigurace sestavení.

Později vytvoříte další tři transformační soubory, po jednom pro profily publikování testu, pracovní a produkční. Typickým příkladem nastavení, které byste zpracovat v souboru transformace profilu publikování, protože závisí na cílovém prostředí je koncový bod WCF, který se liší pro test versus výroba. Po vytvoření profilů publikování, které jsou s ním, vytvoříte soubory transformace profilu publikování v pozdějších kurzech.

## <a name="disable-debug-mode"></a>Zakázání režimu ladění

Příkladem nastavení, které závisí na konfiguraci sestavení, `debug` nikoli na cílovém prostředí, je atribut. Pro sestavení verze obvykle chcete ladění zakázáno bez ohledu na to, do kterého prostředí nasazujete. Proto ve výchozím nastavení šablony projektu sady Visual Studio vytvořit *Web.Release.config transformovat* soubory s kódem, `debug` `compilation` který odebere atribut z prvku. Zde je výchozí *Web.Release.config*: kromě některé ukázkové transformační kód, který `compilation` je zakomentován, obsahuje kód v elementu, který odebere `debug` atribut:

[!code-xml[Main](web-config-transformations/samples/sample1.xml?highlight=18)]

Atribut `xdt:Transform="RemoveAttributes(debug)"` určuje, že chcete `debug` atribut odebrat `system.web/compilation` z prvku v nasazeném souboru *Web.config.* To se provede při každém nasazení sestavení verze.

## <a name="limit-error-log-access-to-administrators"></a>Omezit přístup k protokolu chyb správcům

Pokud dojde k chybě při spuštění aplikace, aplikace zobrazí obecnou chybovou stránku namísto systémově generované chybové stránky a používá [balíček Elmah NuGet](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) pro protokolování chyb a vytváření sestav. Prvek `customErrors` v souboru *Web.config* aplikace určuje chybovou stránku:

[!code-xml[Main](web-config-transformations/samples/sample2.xml)]

Chcete-li zobrazit chybovou stránku, dočasně změňte `mode` atribut `customErrors` prvku z "RemoteOnly" na "On" a spusťte aplikaci z aplikace Visual Studio. Způsobit chybu vyžádáním neplatné adresy URL, například *Studentsxxx.aspx*. Místo chybové stránky "Prostředek nebyl nalezen" vygenerovaná ze strany IIS se zobrazí stránka *GenericErrorPage.aspx.*

![Chybová stránka](web-config-transformations/_static/image2.png)

Chcete-li zobrazit protokol chyb, nahraďte vše v adrese URL za číslem portu *elmah.axd* `http://localhost:51130/elmah.axd`(například) a stiskněte Enter:

![Stránka ELMAH](web-config-transformations/_static/image3.png)

Nezapomeňte nastavit `customErrors` prvek zpět do režimu "RemoteOnly", když budete hotovi.

Ve vývojovém počítači je vhodné povolit volný přístup ke stránce protokolu chyb, ale v produkčním prostředí by to bylo bezpečnostní riziko. Pro produkční lokalitu chcete přidat autorizační pravidlo, které omezuje přístup k protokolu chyb správcům, a ujistěte se, že omezení funguje, chcete-li v testu a přípravě také. Proto je to další změna, kterou chcete implementovat při každém nasazení sestavení release, a proto patří do souboru *Web.Release.config.*

Otevřete *web.Release.config* a `location` přidejte nový `configuration` prvek bezprostředně před uzavírací značku, jak je znázorněno zde.

[!code-xml[Main](web-config-transformations/samples/sample3.xml?highlight=27-34)]

Hodnota `Transform` atributu "Vložit" `location` způsobí, že tento prvek má `location` být přidán jako na stejné úrovni k existujícím prvkům v souboru *Web.config.* (Již existuje `location` jeden prvek, který určuje autorizační pravidla pro stránku **Aktualizovat kredity.)**

Nyní můžete zobrazit náhled transformace a ujistěte se, že jste ji kódovali správně.

V **Průzkumníku řešení**klepněte pravým tlačítkem myši na *web.release.config* a klepněte na příkaz **Náhled transformace**.

![Nabídka Transformace náhledu](web-config-transformations/_static/image4.png)

Otevře se stránka, která zobrazuje vývojový soubor *Web.config* vlevo a jak bude nasazený soubor *Web.config* vypadat vpravo se zvýrazněnými změnami.

![Náhled ladicí transformace](web-config-transformations/_static/image5.png)

![Náhled transformace umístění](web-config-transformations/_static/image6.png)

(V náhledu si můžete všimnout některých dalších změn, pro které jste nenapsali transformace: obvykle zahrnují odstranění prázdného místa, které nemá vliv na funkčnost.)

Když testujete lokalitu po nasazení, budete také testovat ověřit, zda je pravidlo autorizace účinné.

> [!NOTE] 
> 
> **Poznámka k zabezpečení** Nikdy nezobrazovat podrobnosti o chybě veřejnosti v produkční aplikaci ani tyto informace neukládat ve veřejném umístění. Útočníci mohou pomocí informací o chybách zjistit chyby zabezpečení na webu. Pokud elmah používáte ve vlastní aplikaci, nakonfigurujte ELMAH tak, aby minimalizoval bezpečnostní rizika. Elmah příklad v tomto kurzu by neměly být považovány za doporučenou konfiguraci. Jedná se o příklad, který byl vybrán, aby ilustroval, jak zpracovat složku, ve které musí být aplikace schopna vytvářet soubory. Další informace naleznete [v tématu zabezpečení koncového bodu ELMAH](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages).

## <a name="a-setting-that-youll-handle-in-publish-profile-transformation-files"></a>Nastavení, které budete zpracovávat v souborech transformace profilu publikování

Běžným scénářem je mít nastavení souboru *Web.config,* které se musí lišit v každém prostředí, do kterého nasadíte. Například aplikace, která volá službu WCF může potřebovat jiný koncový bod v testovacím a provozním prostředí. Aplikace Contoso University obsahuje také nastavení tohoto druhu. Toto nastavení řídí viditelný indikátor na stránkách webu, který vám řekne, ve kterém prostředí se právě nacházejíte, například vývoj, testování nebo výrobu. Hodnota nastavení určuje, zda aplikace připojí "(Dev)" nebo "(Test)" k hlavnímu nadpisu na stránce předlohy *Site.Master:*

![Ukazatel prostředí](web-config-transformations/_static/image7.png)

Indikátor prostředí je vynechán, když je aplikace spuštěna v pracovní nebo produkční.

Webové stránky Univerzity Contoso čtou `appSettings` hodnotu nastavenou v souboru *Web.config,* aby bylo možné určit, v jakém prostředí je aplikace spuštěna:

[!code-xml[Main](web-config-transformations/samples/sample4.xml)]

Hodnota by měla být "Test" v testovacím prostředí a "Prod" pro pracovní a produkční.

Následující kód v transformačním souboru implementuje tuto transformaci:

[!code-xml[Main](web-config-transformations/samples/sample5.xml)]

Hodnota `xdt:Transform` atributu "SetAttributes" označuje, že účelem této transformace je změna hodnot atributů existujícího prvku v souboru *Web.config.* Hodnota `xdt:Locator` atributu "Match(key)" označuje, že prvek, `key` který má `key` být změněn, je ten, jehož atribut odpovídá zde zadanému atributu. Jediným dalším atributem `add` prvku `value`je a to je to, co se změní v nasazeném souboru *Web.config.* Zde zobrazený kód `value` způsobí, `Environment` `appSettings` že atribut prvku bude nastaven na "Test" v souboru *Web.config,* který je nasazen.

Tato transformace patří do souborů transformace profilu publikování, které jste ještě nevytvořili. Soubory transformace, které tuto změnu implementují, vytvoříte a aktualizujete při vytváření profilů publikování pro testovací, pracovní a produkční prostředí. To uděláte v [nasazení do služby IIS](deploying-to-iis.md) a [nasazení do produkčních](deploying-to-production.md) kurzů.

> [!NOTE]
> Vzhledem k tomu, že toto nastavení je v `<appSettings>` prvku, máte jinou alternativu pro určení transformace při nasazování do webových aplikací ve službě Azure App Service viz určení nastavení [Web.config v Azure](#watransforms) dříve v tomto tématu.

## <a name="setting-connection-strings"></a>Nastavení připojovacích řetězců

Přestože výchozí transformační soubor obsahuje příklad, který ukazuje, jak aktualizovat připojovací řetězec, ve většině případů není nutné nastavit transformace připojovacího řetězce, protože v profilu publikování můžete zadat připojovací řetězce. To uděláte v [nasazení do služby IIS](deploying-to-iis.md) a [nasazení do produkčních](deploying-to-production.md) kurzů.

## <a name="summary"></a>Souhrn

Nyní jste udělali co nejvíce s transformacemi *Web.config* před vytvořením profilů publikování a viděli jste náhled toho, co bude v nasazeném souboru Web.config.

![Náhled transformace umístění](web-config-transformations/_static/image8.png)

V následujícím kurzu se postaráte o úlohy nastavení nasazení, které vyžadují nastavení vlastností projektu.

## <a name="more-information"></a>Další informace

Další informace o tématech, na něž se vztahuje tento kurz, naleznete [v tématu Použití transformací Web.config ke změně nastavení v cílovém souboru Web.config nebo souboru app.config během nasazení](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms) v mapě obsahu nasazení webu pro visual studio a ASP.NET.

> [!div class="step-by-step"]
> [Předchozí](preparing-databases.md)
> [další](project-properties.md)
