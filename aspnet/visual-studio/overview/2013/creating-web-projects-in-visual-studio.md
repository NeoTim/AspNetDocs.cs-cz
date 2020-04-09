---
uid: visual-studio/overview/2013/creating-web-projects-in-visual-studio
title: Vytváření ASP.NET webových projektů v sadě Visual Studio 2013 | Dokumenty společnosti Microsoft
author: tdykstra
description: Toto téma vysvětluje možnosti pro vytváření ASP.NET webových projektů v sadě Visual Studio 2013 s aktualizací 3 Zde jsou některé nové funkce pro vývoj webu c...
ms.author: riande
ms.date: 12/01/2014
ms.assetid: 61941e64-0c0d-4996-9270-cb8ccfd0cabc
msc.legacyurl: /visual-studio/overview/2013/creating-web-projects-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: fbb4cd7afa2506879d47bce980bf0164aad40c2c
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676046"
---
# <a name="creating-aspnet-web-projects-in-visual-studio-2013"></a>Vytváření webových projektů ASP.NET v sadě Visual Studio 2013

podle [Tom Dykstra](https://github.com/tdykstra)

> Toto téma vysvětluje možnosti vytváření ASP.NET webových projektů v sadě Visual Studio 2013 s aktualizací 3
> 
> Tady jsou některé nové funkce pro vývoj webových aplikací ve srovnání s dřívějšími verzemi sady Visual Studio:
> 
> - Jednoduché uživatelské rozhraní pro vytváření projektů, které nabízejí [podporu pro více ASP.NET rámci](#add) (webové formuláře, MVC a webové rozhraní API).
> - [ASP.NET Identity](#indauth), nový systém členství v ASP.NET, který funguje stejně ve všech ASP.NET rámci a pracuje s web hosting software jiné než IIS.
> - Použití [Bootstrap](#bootstrap) poskytnout citlivý design a možnosti témat.
> - Nové funkce pro webové formuláře, které byly nabízeny pouze pro mvc, jako je [například automatické vytváření testovacích projektů](#testproj) a [intranetová šablona webu](#winauth).
> 
> Informace o tom, jak vytvářet webové projekty pro Azure Cloud Services nebo Azure Mobile Services, najdete [v tématu Začínáme s Cloudovými službami Azure a ASP.NET](https://azure.microsoft.com/documentation/articles/cloud-services-dotnet-get-started/) a vytvoření aplikace [Leaderboard s Azure Mobile Services .NET Backend](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/).

<a id="prerequisites"></a>
## <a name="prerequisites"></a>Požadavky

Tento článek se vztahuje na [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) s [nainstalovanou aktualizací 3.](https://go.microsoft.com/fwlink/?linkid=397827&amp;clcid=0x409)

<a id="wap"></a>
## <a name="web-application-projects-versus-web-site-projects"></a>Projekty webových aplikací versus projekty webových stránek

ASP.NET vám dává na výběr mezi dvěma druhy webových projektů: *projekty webových aplikací* a *projekty webových stránek*. Doporučujeme projekty webových aplikací pro nový vývoj a tento článek se vztahuje pouze na projekty webových aplikací. Další informace naleznete v [tématu Projekty webových aplikací versus projekty webových stránek v sadě Visual Studio](https://msdn.microsoft.com/library/dd547590(v=vs.120).aspx) na webu MSDN.

<a id="overview"></a>
## <a name="overview-of-web-application-project-creation"></a>Přehled vytváření projektu webové aplikace

Následující kroky ukazují, jak vytvořit webový projekt:

1. Na stránce **Start** nebo v nabídce **Soubor** klikněte na **Nový projekt.**
2. V dialogovém okně **Nový projekt** klikněte v levém podokně na **Web** a v prostředním podokně **ASP.NET webovou aplikaci.**

    ![Dialogové okno Nový projekt](creating-web-projects-in-visual-studio/_static/image1.png)

    **Cloud** můžete zvolit v levém podokně a vytvořit [azure cloudovou službu](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy), [mobilní službu Azure](https://msdn.microsoft.com/library/windows/apps/dn629482.aspx)nebo Azure [WebJob](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-webjobs). Toto téma se nevztahuje na tyto šablony.
3. V pravém podokně klikněte na zaškrtávací políčko **Přidat přehledy aplikací do projectu,** pokud chcete sledovat stav a využití vaší aplikace. Další informace naleznete [v tématu Sledování výkonu ve webových aplikacích](https://azure.microsoft.com/documentation/articles/app-insights-web-monitor-performance/).
4. Zadejte **název**projektu , **umístění**a další možnosti a klepněte na tlačítko **OK**.

    Zobrazí se dialogové okno **Nový ASP.NET projektu.**

    ![Dialogové okno Nový projekt](creating-web-projects-in-visual-studio/_static/image2.png)
5. Klikněte na šablonu.

    ![Výběr šablony](creating-web-projects-in-visual-studio/_static/image3.png)
6. Pokud chcete přidat podporu pro další architektury, které nejsou zahrnuty v šabloně, zaškrtněte příslušné políčko. (V zobrazeném příkladu můžete přidat MVC nebo webové rozhraní API do projektu webových formulářů.)

    ![Přidání architektur](creating-web-projects-in-visual-studio/_static/image4.png)
7. <a id="testproj"></a>Pokud chcete přidat projekt testování částí, klepněte na tlačítko **Přidat testy částí**.

    ![Přidání testů jednotek](creating-web-projects-in-visual-studio/_static/image5.png)
8. Pokud chcete jinou metodu ověřování, než jakou šablona poskytuje ve výchozím nastavení, klepněte na **tlačítko Změnit ověřování**.

    ![Konfigurovat ověřovací tlačítko](creating-web-projects-in-visual-studio/_static/image6.png)

    ![Dialogové okno Konfigurace ověřování](creating-web-projects-in-visual-studio/_static/image7.png)

<a id="azurenewproj"></a>
### <a name="create-a-web-app-or-virtual-machine-in-azure"></a>Vytvoření webové aplikace nebo virtuálního počítače v Azure

Visual Studio obsahuje funkce, které usnadňují práci se službami Azure pro hostování webových aplikací. Například můžete provést všechny následující akce přímo z ide Visual Studio:

- Vytvářejte a spravujte webové aplikace nebo virtuální počítače, které zpřístupní vaši aplikaci přes Internet.
- Zobrazit protokoly vytvořené aplikací při spuštění v cloudu.
- Spouštět v režimu ladění vzdáleně, zatímco aplikace běží v cloudu.
- Zobrazení a správa dalších služeb Azure, jako jsou databáze SQL.

Můžete [si vytvořit účet Azure,](https://www.windowsazure.com/pricing/free-trial/) který obsahuje základní služby, jako jsou webové aplikace zdarma, a pokud jste předplatitelem MSDN, můžete [aktivovat výhody,](https://azure.microsoft.com/pricing/member-offers/visual-studio-subscriptions/) které vám poskytují měsíční kredity na další služby Azure. 

Ve výchozím nastavení umožňuje dialogové okno **Nový ASP.NET projekt** vytvořit webovou aplikaci nebo virtuální počítač pro nový webový projekt. Pokud nechcete vytvořit novou webovou aplikaci nebo virtuální počítač, zrušte zaškrtnutí **políčka Host in the cloud.**

![Vytvoření vzdálených prostředků](creating-web-projects-in-visual-studio/_static/image8.png)

Zaškrtávací políčko titulek může být **Host v cloudu** nebo **Vytvořit vzdálené prostředky**a v obou případech efekt je stejný. Pokud ponecháte zaškrtnuté políčko, Visual Studio ve výchozím nastavení vytvoří webovou aplikaci ve službě Azure App Service. Rozevírací seznam můžete použít ke změně na **virtuální počítač,** pokud dáváte přednost. Pokud ještě nejste přihlášení k Azure, budete vyzváni k zadání přihlašovacích údajů Azure. Po přihlášení dialogové okno umožňuje konfigurovat prostředky, které Visual Studio vytvoří pro váš projekt. Následující obrázek znázorňuje dialog pro webovou aplikaci; pokud se rozhodnete vytvořit virtuální počítač, zobrazí se různé možnosti.

![Konfigurace nastavení aplikací Azure](creating-web-projects-in-visual-studio/_static/image9.png)

Další informace o tom, jak tento proces používat k vytváření prostředků Azure, najdete v tématu [Začínáme s Azure a ASP.NET](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet) a vytvoření [virtuálního počítače pro web s Visual Studio](https://azure.microsoft.com/documentation/articles/virtual-machines-dotnet-create-visual-studio-powershell/).

Zbývající část tohoto článku obsahuje další informace o dostupných šablon a jejich možnostech. Článek také zavádí Bootstrap, rozložení a tématiku rámec používaný v šablonách.

<a id="vs2013"></a>
## <a name="visual-studio-2013-web-project-templates"></a>Šablony webového projektu Sady Visual Studio 2013

Visual Studio používá šablony k vytváření webových projektů. Šablona projektu můžete vytvářet soubory a složky v novém projektu, nainstalovat balíčky NuGet a poskytnout ukázkový kód pro základní pracovní aplikace. Šablony implementují nejnovější webové standardy a jsou určeny k předvedení osvědčených postupů pro používání ASP.NET technologií a také vám poskytnou skokový start při vytváření vlastní aplikace.

Visual Studio 2013 poskytuje následující možnosti pro šablony webových projektů pro projekty, které cílí na .NET 4.5 nebo novější verze rozhraní .NET:

- [Prázdná šablona](#empty)
- [Šablona webových formulářů](#wf)
- [Šablona MVC](#mvc)
- [Šablona webového rozhraní API](#webapi)
- [Šablona aplikace s jednou stránkou](#spa)
- [Šablona mobilní služby Azure](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)
- [Šablony Visual Studia 2012](#vs2012)

Můžete také nainstalovat rozšíření Sady Visual Studio, které poskytuje [šablonu Facebooku](#facebook).

Informace o tom, jak vytvořit projekty, které cílí na .NET 4, naleznete v [tématu Visual Studio 2012 Šablony](#vs2012) dále v tomto tématu.

Informace o vytváření ASP.NET aplikací pro mobilní klienty naleznete [v tématu Mobilní podpora v ASP.NET](../../../mobile/overview.md).

<a id="empty"></a>
### <a name="empty-template"></a>Prázdná šablona

Šablona Empty poskytuje minimální složky a soubory pro ASP.NET webovou aplikaci, například soubor projektu (*csproj* nebo .* vbproj*) a soubor *Web.config.* Podporu webových formulářů, MVC nebo webového rozhraní API můžete přidat pomocí zaškrtávacích políček v části **Přidat složky a základní odkazy pro:** popisek.

Pro šablonu Prázdná nejsou k dispozici žádné možnosti ověřování. Funkce ověřování je implementována v ukázkových aplikacích a šablona Empty nevytvoří ukázkovou aplikaci.

<a id="wf"></a>
### <a name="web-forms-template"></a>Šablona webových formulářů

Rozhraní Web Forms Framework poskytuje následující funkce, které umožňují rychle vytvářet webové servery bohaté na uživatelské rozhraní a funkce přístupu k datům:

- Návrhář WYSIWYG v sadě Visual Studio.
- Serverové ovládací prvky, které vykreslují HTML a které můžete přizpůsobit nastavením vlastností a stylů.
- Bohatý sortiment ovládacích prvků pro přístup k datům a zobrazení dat.
- Model událostí, který zveřejňuje události, které můžete programovat, jako byste programklientské aplikace, jako je například WPF.
- Automatické uchování stavu (dat) mezi požadavky HTTP.

Obecně platí, že vytvoření aplikace webových formulářů vyžaduje méně úsilí programování než vytvoření stejné aplikace pomocí ASP.NET rámci MVC. Webové formuláře však nejsou určeny pouze pro rychlý vývoj aplikací. Existuje mnoho složitých komerčních aplikací a rámců postavených na webových formulářích.

Vzhledem k tomu, že stránka webových formulářů a ovládací prvky na stránce automaticky generují velkou část značek odeslaných do prohlížeče, nemáte takovou, jakou jemně odstupňovanou kontrolu nad kódem HTML, který ASP.NET mvc nabízí. Deklarativní model pro konfiguraci stránek a ovládacích prvků minimalizuje množství kódu, který je třeba napsat, ale skryje některé chování HTML a HTTP. Například není vždy možné přesně určit, jaké značky mohou být generovány ovládacím prvkem.

Rámec webových formulářů není vhodný jako ASP.NET MVC na vývojové postupy založené na vzorcích, jako je [vývoj řízený testem](http://en.wikipedia.org/wiki/Test-driven_development), [oddělení obav](http://en.wikipedia.org/wiki/Separation_of_concerns), [inverze kontroly](http://en.wikipedia.org/wiki/Inversion_of_control)a [vkládání závislostí](http://en.wikipedia.org/wiki/Dependency_injection). Pokud chcete napsat kód zakódovaný tímto způsobem, můžete; je to prostě není tak automatické, jak je v ASP.NET rámci MVC. [Projekt ASP.NET Web Forms MVP](http://webformsmvp.com/) ukazuje přístup, který usnadňuje oddělení obav a testovatelnosti při zachování rychlého vývoje, který byly vytvořeny pro poskytování webových formulářů. Služba Microsoft SharePoint je postavena na mvp webových formulářů.

Šablona Webové formuláře vytvoří ukázkovou aplikaci webových formulářů, která pomocí [bootstrapu](#bootstrap) poskytuje responzivní návrh a funkce tematů. Následující obrázek znázorňuje domovskou stránku.

![Domovská stránka aplikace šablony webových formulářů](creating-web-projects-in-visual-studio/_static/image10.png)

Další informace o webových formulářích naleznete [v tématu ASP.NET Web Forms](https://asp.net/web-forms). Informace o tom, co pro vás šablona Webových formulářů dělá, naleznete v [tématu Vytváření základní aplikace webových formulářů pomocí sady Visual Studio 2013](https://blogs.msdn.com/b/webdev/archive/2013/12/19/building-a-basic-web-forms-application-using-visual-studio-2013.aspx).

<a id="mvc"></a>
### <a name="mvc-template"></a>Šablona MVC

ASP.NET MVC byla navržena tak, aby usnadnila vývojové postupy založené na vzorcích, jako je vývoj založený na [testech](http://en.wikipedia.org/wiki/Test-driven_development), [oddělení obav](http://en.wikipedia.org/wiki/Separation_of_concerns), [inverze kontroly](http://en.wikipedia.org/wiki/Inversion_of_control)a [vstřikování závislosti](http://en.wikipedia.org/wiki/Dependency_injection). Rámec podporuje oddělení vrstvy obchodní logiky webové aplikace od její prezentační vrstvy. Rozdělením aplikace do modelů (M), zobrazení (V) a řadiče (C), ASP.NET MVC může usnadnit správu složitosti ve větších aplikacích.

S ASP.NET MVC pracujete přímo s HTML a HTTP než ve webových formulářích. Webové formuláře mohou například automaticky zachovat stav mezi požadavky HTTP, ale musíte jej kódovat explicitně v mvc. Výhodou modelu MVC je, že umožňuje převzít úplnou kontrolu nad tím, co vaše aplikace dělá a jak se chová ve webovém prostředí. Nevýhodou je, že musíte napsat další kód.

MVC byl navržen tak, aby byl rozšiřitelný a poskytoval vývojářům napájení možnost přizpůsobit rámec pro potřeby svých aplikací. Kromě toho je zdrojový kód ASP.NET MVC k dispozici pod licencí OSI.

Šablona MVC vytvoří ukázkovou aplikaci MVC 5, která používá [Bootstrap](#bootstrap) k zajištění responzivního návrhu a funkcí témat. Následující obrázek znázorňuje domovskou stránku.

![Ukázková aplikace MVC](creating-web-projects-in-visual-studio/_static/image11.png)

Další informace o MVC naleznete [v tématu ASP.NET MVC](https://asp.net/mvc). Informace o tom, jak vybrat šablonu MVC 4, najdete v [tématu Visual Studio 2012 šablony](#vs2012) dále v tomto článku.

<a id="webapi"></a>
### <a name="web-api-template"></a>Šablona webového rozhraní API

Šablona webového rozhraní API vytvoří ukázkovou webovou službu založenou na webovém rozhraní API, včetně stránek nápovědy rozhraní API založených na MVC.

ASP.NET web API je rámec, který usnadňuje vytváření služeb HTTP, které osloví širokou škálu klientů, včetně prohlížečů a mobilních zařízení. ASP.NET Web API je ideální platformou pro vytváření služeb RESTful v rozhraní .NET Framework.

Šablona webového rozhraní API vytvoří ukázkovou webovou službu. Na následujících obrázcích jsou ukázkové stránky nápovědy.

![Stránka nápovědy webového rozhraní API](creating-web-projects-in-visual-studio/_static/image12.png)

![Stránka nápovědy webového rozhraní API pro rozhraní GET API](creating-web-projects-in-visual-studio/_static/image13.png)

Další informace o webovém rozhraní API naleznete [v tématu ASP.NET Web API](https://asp.net/web-api).

<a id="spa"></a>
### <a name="single-page-application-template"></a>Šablona aplikace s jednou stránkou

Šablona Spa (Single Page Application) vytvoří ukázkovou aplikaci, která používá javascript, HTML 5 a [KnockoutJS](http://knockoutjs.com/) v klientovi a ASP.NET webové rozhraní API na serveru.

Jedinou možností ověřování pro šablonu SPA jsou [jednotlivé uživatelské účty](#indauth).

Následující obrázek znázorňuje počáteční stav ukázkové aplikace, kterou vytvoří šablona SPA.

![Ukázková aplikace SPA](creating-web-projects-in-visual-studio/_static/image14.png)

Informace o vytvoření aplikace pomocí šablony SPA naleznete v tématu [Web API - External Authentication Services](../../../web-api/overview/security/external-authentication-services.md).

Další informace o ASP.NET jednostránkových aplikacích a dalších šablonách SPA, které používají jiné architektury JavaScriptu než KnockoutJS, naleznete v následujících zdrojích:

- [ASP.NET jednostránková aplikace](../../../single-page-application/index.md).
- [Principy funkcí zabezpečení v šabloně SPA pro VS2013 RC](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx)
- [Jednostránkové aplikace: Vytvářejte moderní, responzivní webové aplikace s ASP.NET](https://msdn.microsoft.com/magazine/dn463786.aspx)

<a id="facebook"></a>
### <a name="facebook-template"></a>Šablona Facebooku

Můžete nainstalovat [rozšíření Sady Visual Studio, které poskytuje šablonu Facebooku](https://go.microsoft.com/fwlink/?LinkID=509965&amp;clcid=0x409). Tato šablona vytvoří ukázkovou aplikaci, která je navržena tak, aby běžela na webu Facebooku. Je založen na ASP.NET MVC a používá webové rozhraní API pro funkce aktualizace v reálném čase.

Pro šablonu Facebook nejsou k dispozici žádné možnosti ověřování, protože aplikace Facebook běží na webu Facebook a spoléhají se na ověřování na Facebooku.

Další informace o ASP.NET aplikacích Facebook najdete [v tématu Aktualizace rozhraní MVC Facebook API](https://blogs.msdn.com/b/webdev/archive/2014/06/10/updating-the-mvc-facebook-api.aspx).

<a id="vs2012"></a>
### <a name="visual-studio-2012-templates"></a>Šablony Visual Studia 2012

Dialogové okno vytvoření webového projektu sady Visual Studio 2013 neposkytuje přístup k některým šablonám, které byly k dispozici v sadě Visual Studio 2012. Pokud chcete použít některou z těchto šablon, můžete kliknout na uzel Visual Studio 2012 v levém podokně dialogového okna Nový projekt sady Visual Studio.

![Šablony Visual Studia 2012](creating-web-projects-in-visual-studio/_static/image15.png)

Uzel **Visual Studio 2012** umožňuje zvolit následující webové šablony, ke kterým nemáte přístup ve výchozím seznamu šablon pro Visual Studio 2013:

- ASP.NET Webová aplikace MVC 4
- ASP.NET webová aplikace dynamických datových entit
- ASP.NET řízení serveru AJAX
- ASP.NET rozšiřovač řízení serveru AJAX
- ASP.NET serverový ovládací prvek

<a id="bootstrap"></a>
## <a name="bootstrap-in-the-visual-studio-2013-web-project-templates"></a>Bootstrap v šablonách webového projektu Visual Studia 2013

Šablony projektu Visual Studio 2013 používají [Bootstrap](http://getbootstrap.com/), rámec rozložení a motivů vytvořený twitterem. Bootstrap používá CSS3 k zajištění responzivního designu, což znamená, že rozložení se mohou dynamicky přizpůsobovat různým velikostem oken prohlížeče. Například v širokém okně prohlížeče vypadá domovská stránka vytvořená šablonou Webových formulářů na následujícím obrázku:

![Domovská stránka aplikace šablony webových formulářů](creating-web-projects-in-visual-studio/_static/image16.png)

Ztěžte okno a horizontálně uspořádané sloupce se přesunou do svislého uspořádání:

![Bootstrap vertikální uspořádání sloupců](creating-web-projects-in-visual-studio/_static/image17.png)

Zúžete okno o něco více a horizontální horní nabídka se změní na ikonu, kterou můžete kliknutím rozbalit do vertikálně orientované nabídky:

![Ikona nabídky Bootstrap](creating-web-projects-in-visual-studio/_static/image18.png)

![Bootstrap vertikální menu](creating-web-projects-in-visual-studio/_static/image19.png)

Můžete také použít funkci motivů Bootstrap, abyste snadno provedli změnu vzhledu a chování aplikace. Můžete například provést následující kroky ke změně motivu.

1. V prohlížeči přejděte na [http://Bootswatch.com](http://Bootswatch.com), zvolte motiv a klikněte na **Stáhnout**. (To to stáhne *bootstrap.min.css* ve výchozím nastavení; pokud chcete prozkoumat kód CSS, získejte *bootstrap.css* místo minifikované verze.)
2. Zkopírujte obsah staženého souboru CSS.
3. V sadě Visual Studio vytvořte nový soubor **šablony stylů** s názvem *bootstrap-theme.css* ve složce *Obsah* a vložte do něj stažený kód CSS.
4. *Otevřete\_aplikaci Start/Bundle.config* a změňte *bootstrap.css* na *bootstrap-theme.css*.

Spusťte projekt znovu a aplikace má nový vzhled. Následující obrázek znázorňuje účinek motivu Amelia:

![Motiv Bootstrap Amelia](creating-web-projects-in-visual-studio/_static/image20.png)

K dispozici je mnoho motivů Bootstrap, a to jak bezplatné, tak prémiové verze. Bootstrap také nabízí širokou škálu komponent ui, jako jsou [rozevírací nabídky](http://twitter.github.io/bootstrap/components.html#dropdowns), [skupiny tlačítek](http://twitter.github.io/bootstrap/components.html#buttonGroups)a [ikony](http://twitter.github.io/bootstrap/base-css.html#images). Další informace o Bootstrapu najdete [na webu Bootstrap](http://twitter.github.io/bootstrap/).

Pokud používáte návrháře webových formulářů v sadě Visual Studio, všimněte si, že návrhář nepodporuje CSS3, takže není přesně zobrazit všechny efekty Bootstrap motivy nebo změny responzivní rozložení. Stránky webových formulářů se však při zobrazení pomocí prohlížeče zobrazí správně.

<a id="add"></a>
## <a name="adding-support-for-additional-frameworks"></a>Přidání podpory pro další rámce

Když vyberete šablonu, automaticky se zaškrtne políčko pro rozhraní používaná šablonou. Pokud například vyberete šablonu **webových formulářů,** zaškrtne se políčko **Webové formuláře** a nelze ji vymazat.

![Výběr šablony](creating-web-projects-in-visual-studio/_static/image21.png)

![Přidání architektur](creating-web-projects-in-visual-studio/_static/image22.png)

Můžete zaškrtnout políčko pro rozhraní, které není zahrnuto v šabloně, abyste přidali podporu pro tuto architekturu při vytvoření projektu. Chcete-li například povolit použití stránek Web Forms *.aspx* po zaškrtnutí šablony MVC, zaškrtněte políčko **Webové formuláře.** Chcete-li povolit mvc při použití šablony webových formulářů, klepněte na zaškrtávací políčko **MVC.** Přidání rozhraní umožňuje návrhu i podporu za běhu. Pokud například přidáte podporu MVC do projektu webových formulářů, budete moci vytvořit uživatelské zařízení a zobrazení.

Pokud v projektu zkombinujete webové formuláře a mvc a [povolíte popisné adresy URL](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx) ve webových formulářích, mohou nastat neočekávané problémy se směrováním, kdy jedna adresa URL obsahuje více možných cílů. Přednost budou mít trasy, které jsou definovány jako první. Pokud máte například `Home` řadič a stránku *Home.aspx,* `http://contoso.com/home` adresa URL přejde na *web Home.aspx,* pokud `EnableFriendlyUrls` před voláním `MapRoute` metody zavoláte v *RouteConfig.cs*, nebo stejná adresa URL přejde do výchozího zobrazení `Home` ovladače, pokud zavoláte `MapRoute` dříve `EnableFriendlyUrls`.

Přidání rozhraní nepřidá žádné ukázkové funkce aplikace. Pokud například přidáte podporu webových formulářů, když vyberete šablonu MVC, nebude vytvořen žádný soubor domovské stránky *Default.aspx.* Jsou přidány pouze složky, soubory a odkazy potřebné pro podporu rozhraní. Z tohoto důvodu přidání rozhraní nezmění možnosti ověřování, které jsou implementovány podle kódu v ukázkových aplikacích vytvořených šablonami. Pokud například vyberete šablonu Vyprázdnit a přidáte webové formuláře nebo podporu MVC, bude tlačítko **Konfigurovat ověřování** stále zakázáno.

Následující části stručně popisují účinek každého zaškrtávacího políčka.

### <a name="add-web-forms-support"></a>Přidat podporu webových formulářů

Vytvoří prázdné složky Data a *Modely* *aplikací\_* a soubor *Global.asax.* Ty jsou již vytvořeny všemi šablonami kromě šablony Empty, takže zaškrtnutí políčka Webové formuláře není u jiných šablon v žádném rozdílu.

Šablona Webových formulářů ve výchozím nastavení povoluje popisné adresy URL, ale když přidáte podporu webových formulářů do jiných šablon zaškrtnutím políčka Webové formuláře, nejsou adresy URL automaticky povoleny.

### <a name="add-mvc-support"></a>Přidat podporu MVC

Nainstaluje balíčky MVC, Razor a WebPages NuGet, vytvoří prázdné *složky Data\_aplikací*, *Řadiče*, *Modely*a *Zobrazení,* vytvoří složku *Start aplikace\_* se *souborem RouteConfig.cs* a vytvoří soubor *Global.asax.*

### <a name="add-web-api-support"></a>Přidat podporu webového rozhraní API

Nainstaluje balíčky WebApi a Newtonsoft.Json NuGet, vytvoří prázdné *složky\_Data aplikací*, *Řadiče*a *Modely,* vytvoří složku Start *aplikace\_* se *souborem WebApiConfig.cs* a vytvoří soubor *Global.asax.*

<a id="auth"></a>
## <a name="authentication-methods"></a>Metody ověřování

Visual Studio 2013 nabízí několik možností ověřování pro šablony webových formulářů, MVC a webového rozhraní API:

- [Bez ověřování](#noauth)
- [Individuální uživatelské účty](#indauth) (ASP.NET Identity, dříve známé jako ASP.NET členství)
- [Účty organizace](#orgauth) (služba Windows Server Active Directory nebo Azure Active Directory)
- [Ověřování systému Windows](#winauth) (intranet)

![Dialogové okno Konfigurace ověřování](creating-web-projects-in-visual-studio/_static/image23.png)

<a id="noauth"></a>

### <a name="no-authentication"></a>Bez ověřování

Pokud vyberete **možnost Žádné ověřování**, ukázková aplikace nebude obsahovat žádné webové stránky pro přihlášení, žádné uživatelské okno označující, kdo je přihlášen, žádné třídy entit pro databázi členství a žádný připojovací řetězec pro databázi členství.

<a id="indauth"></a>
### <a name="individual-user-accounts"></a>Jednotlivé uživatelské účty

Pokud vyberete **jednotlivé uživatelské účty**, ukázková aplikace bude nakonfigurována tak, aby pro ověřování uživatelů používala ASP.NET identity (dříve označované jako ASP.NET členství). ASP.NET Identita umožňuje uživateli zaregistrovat si účet vytvořením uživatelského jména a hesla na webu nebo přihlášením k poskytovatelům sociálních sítí, jako je Facebook, Google, Účet Microsoft nebo Twitter. Výchozí úložiště dat pro profily uživatelů v ASP.NET identity je databáze SQL Server LocalDB, kterou můžete nasadit na SQL Server nebo Azure SQL Database pro produkční lokalitu.

V sadě Visual Studio 2013 jsou tyto funkce stejné jako v sadě Visual Studio 2012, ale základní kód pro systém členství ASP.NET byl přepsán. Mezi výhody nového základu kódu patří následující:

- Nový systém členství je založen na [OWIN](http://owin.org/) spíše než na modulu ASP.NET Forms Authentication. To znamená, že můžete použít stejný mechanismus ověřování, ať už používáte webové formuláře nebo MVC ve službě IIS, nebo jste vlastní hostování webového rozhraní API nebo SignalR.
- Nová databáze členství je spravována kódem entity framework u první a všechny tabulky jsou reprezentovány třídami entit, které můžete upravit. To znamená, že můžete snadno přizpůsobit schéma databáze a webové uživatelské uživatelské uživatelské informace související s profilem tak, aby vyhovovaly vašim vlastním potřebám, a můžete snadno nasadit aktualizace pomocí migrace Code First.

Nový systém členství je implementován automaticky v nových šablonách a může být implementován ručně v libovolném projektu, který cílí na rozhraní .NET 4.5 nebo novější.

ASP.NET Identity je dobrá volba, pokud vytváříte internetové stránky, které jsou určeny především pro externí zákazníky. Pokud vaše organizace používá službu Active Directory nebo Office 365 a chcete vytvořit projekt, který umožňuje jednotné přihlašování pro zaměstnance a obchodní partnery, může být možnost **Účty organizace** lepší volbou.

Další informace o možnosti Individuální uživatelské účty naleznete v následujících zdrojích:

- [www.asp.net/identity](../../../identity/index.md). Dokumentace o ASP.NET identity na ASP.NET webu.
- [Vytvořte ASP.NET aplikaci MVC 5 s Facebookem a Google OAuth2 a přihlášením OpenID](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md). Ukazuje také, jak přizpůsobit data profilu uživatele.
- [Webové rozhraní API – externí ověřovací služby](../../../web-api/overview/security/external-authentication-services.md)
- [Přidání externích přihlášení do aplikace ASP.NET v sadě Visual Studio 2013](https://blogs.msdn.com/b/webdev/archive/2013/06/27/adding-external-logins-to-your-asp-net-application-in-visual-studio-2013.aspx)

<a id="orgauth"></a>
### <a name="organizational-accounts"></a>Organizační účty

Pokud vyberete **organizační účty**, ukázková aplikace bude nakonfigurována tak, aby používala Windows Identity Foundation (WIF) pro ověřování na základě uživatelských účtů ve službě Azure Active Directory (Azure AD, která zahrnuje Office 365) nebo Windows Server Active Directory. Další informace naleznete v [tématu Možnosti ověřování účtu organizace](#orgauthoptions) dále v tomto tématu.

<a id="winauth"></a>
### <a name="windows-authentication"></a>Ověřování systému Windows

Pokud vyberete **ověřování systému Windows**, ukázková aplikace bude nakonfigurována tak, aby k ověřování používala modul služby IIS ověřování systému Windows. Aplikace zobrazí id domény a uživatele účtu Active directory nebo místního počítače, který je přihlášen k systému Windows, ale nebude obsahovat registraci uživatele nebo uživatelské rozhraní přihlášení. Tato možnost je určena pro intranetové weby.

Případně můžete vytvořit intranetový web, který používá ověřování služby AD, výběrem [možnosti Místní v části Účty organizace](#orgauthonprem). Místní možnost používá Windows Identity Foundation (WIF) místo modulu ověřování systému Windows. Některé další kroky jsou nutné k nastavení možnosti Místní, ale WIF umožňuje funkce, které nejsou k dispozici s modulem ověřování systému Windows. Pomocí rozhraní WIF můžete například konfigurovat přístup k aplikacím ve službě Active Directory a data adresáře dotazů.

<a id="orgauthoptions"></a>
## <a name="organizational-account-authentication-options"></a>Možnosti ověřování účtů organizace

Dialogové okno **Konfigurovat ověřování** nabízí několik možností pro azure active directory (Azure AD, která zahrnuje Office 365) nebo ověřování účtů Služby Active Directory (AD) systému Windows Server:

- [Cloud – jedna organizace](#orgauthsingle) (Azure AD nebo AD pomocí integrace adresářů s Azure AD)
- [Cloud – multi organizace](#orgauthmulti) (Azure AD nebo AD pomocí integrace adresářů s Azure AD)
- [Místní](#orgauthonprem) (AD)

Pokud chcete vyzkoušet některou z možností Azure AD, ale ještě nemáte účet, [klikněte sem a zaregistrujte si účet Azure AD](https://go.microsoft.com/fwlink/?LinkId=309942).

> [!NOTE]
> Pokud zvolíte jednu z možností Azure AD, váš projekt vyžaduje databázi a budete muset přihlásit k účtu globálního správce pro vašeho klienta Azure AD. Zadejte název a heslo pro účet organizace admin@contoso.onmicrosoft.com(například), který má oprávnění správce pro vašeho klienta Azure AD.
> 
> **Nezadávejte přihlašovací údaje k účtu Microsoft contoso@hotmail.com(například) do přihlašovacího dialogového okna.**

<a id="orgauthsingle"></a>
### <a name="cloud---single-organization-authentication"></a>Cloud – ověřování jedné organizace

![Ověřování jedné organizace](creating-web-projects-in-visual-studio/_static/image24.png)

Tuto možnost zvolte, pokud chcete povolit ověřování pro uživatelské účty, které jsou definovány v jednom [tenantovi](https://technet.microsoft.com/library/jj573650.aspx)Azure AD . Například web je contoso.com a bude k dispozici zaměstnancům společnosti Contoso, kteří jsou v contoso.onmicrosoft.com tenantovi. Nebudete moct nakonfigurovat Azure AD tak, aby uživatelům z jiných klientů přístup k aplikaci.

#### <a name="domain"></a>Domain (Doména)

Zadejte doménu Azure AD, ve které chcete aplikaci nastavit, například: `contoso.onmicrosoft.com`. Pokud máte [vlastní doménu](http://www.cloudidentity.com/blog/2013/04/14/adding-a-custom-domain-to-your-windows-azure-ad/) `contoso.com` , `contoso.onmicrosoft.com`například místo , můžete ji zadat zde.

#### <a name="access-level"></a>Úroveň přístupu

Pokud aplikace potřebuje dotazovat nebo aktualizovat informace o adresáři pomocí rozhraní Graph API, zvolte **Jedno přihlášení, Číst data adresáře** nebo **Jedno přihlášení, čtení a zápis dat adresáře**. V opačném případě zvolte **Jednotné přihlašování**. Další informace najdete [v tématu Úrovně přístupu k aplikacím](https://msdn.microsoft.com/library/windowsazure/b08d91fa-6a64-4deb-92f4-f5857add9ed8#BKMK_AccessLevels) a [použití rozhraní API pro graf pro dotazování Azure AD](https://msdn.microsoft.com/library/windowsazure/dn151791.aspx).

#### <a name="application-id-uri"></a>Identifikátor URI ID aplikace

Ve výchozím nastavení vytvoří šablona identifikátor URI aplikace připojením názvu projektu k doméně Azure AD. Pokud je `Example` například název projektu a `contoso.onmicrosoft.com`doména je , `https://contoso.onmicrosoft.com/Example`změní se identifikátor URI aplikace . Pokud chcete ručně zadat identifikátor URI id aplikace, rozbalte oddíl **Další možnosti** a do textového pole zadejte identifikátor URI id aplikace. Identifikátor URI id aplikace `https://`musí začínat .

Ve výchozím nastavení pokud aplikace, která je již zřízena ve službě Azure AD má stejné Identifikátor URI aplikace jako ten, který Visual Studio používá pro projekt, projekt bude připojen k existující aplikaci namísto zřizování nové. Pokud chcete, aby se v takovém případě zřizovala nová aplikace, zrušte zaškrtnutí políčka **Přepsat položku aplikace, pokud již existuje jedna se stejným ID.**

Pokud políčko **Přepsat** není zaškrtnuto a Visual Studio najde existující aplikaci se stejným identifikátorem URI ID aplikace, vytvoří nový identifikátor URI připojením čísla k identifikátoru URI, který bude používat. Předpokládejme například, že `Example`název projektu je , ponecháte textové pole prázdné, zrušte zaškrtnutí políčka **Přepsat** a tenant Azure AD už má aplikaci s identifikátorem URI `https://contoso.onmicrosoft.com/Example`. V takovém případě bude nová aplikace zřízena s identifikátorem URI aplikace jako `https://contoso.onmicrosoft.com/Example_20130619330903`.

#### <a name="provisioning-the-application-in-azure-ad"></a>Zřizování aplikace ve službě Azure AD

Aby bylo možné zřídit aplikaci ve službě Azure AD nebo připojit projekt k existující aplikaci, Visual Studio potřebuje pověření globálního správce pro doménu. Po klepnutí na tlačítko **OK** v dialogovém okně **Konfigurovat ověřování** se zobrazí výzva k zadání uživatelského jména a hesla globálního správce pro zadanou doménu. Později po kliknutí na **vytvořit projekt** v dialogovém okně Nový **ASP.NET projektu** Visual Studio zřídí aplikace ve službě Azure AD. Všimněte si, že jako součást tohoto procesu Visual Studio vloží tajné hodnoty klienta do souboru Web.config, jejichž platnost vyprší jeden rok po vytvoření.

Informace o tom, jak vytvářet aplikace, které používají cloudové ověřování **jedné organizace,** najdete v následujících zdrojích informací:

- [Ověřování Azure](../2012/windows-azure-authentication.md)
- [Přidání přihlášení do webové aplikace pomocí služby Azure AD](https://msdn.microsoft.com/library/windowsazure/dn151790.aspx)
- [Vývoj aplikací ASP.NET s použitím Azure Active Directory](../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)
- [Zabezpečené ASP.NET webové rozhraní API pomocí komponent Azure AD a Microsoft OWIN](https://msdn.microsoft.com/magazine/dn463788.aspx)

Kurzy ještě nebyly aktualizovány pro Visual Studio 2013; některé z toho, co kurzy nasměrují na ruční, jsou automatizované ve Visual Studiu 2013.

<a id="orgauthmulti"></a>
### <a name="cloud---multi-organization-authentication"></a>Cloud – ověřování více organizací

![Ověřování více organizací](creating-web-projects-in-visual-studio/_static/image25.png)

Tuto možnost zvolte, pokud chcete povolit ověřování pro uživatelské účty, které jsou definovány ve více [klientech](https://technet.microsoft.com/library/jj573650.aspx)Azure AD . Například lokalita je contoso.com a bude zpřístupněna zaměstnancům společnosti Contoso, kteří jsou v contoso.onmicrosoft.com nájemci, a zaměstnancům společnosti Fabrikam, kteří jsou v fabrikam.onmicrosoft.com tenantovi.

Nastavení, která zadáte, a krok zřizování aplikace jsou podobné [ověřování jedné organizace](#orgauthsingle).

Informace o tom, jak vytvářet aplikace, které používají **cloudové ověřování více organizací,** naleznete v následujících zdrojích informací:

- [Snadná integrace webových aplikací &amp; s Azure Active Directory, ASP.NET Visual Studio](https://blogs.msdn.com/b/active_directory_team_blog/archive/2013/06/26/improved-windows-azure-active-directory-integration-with-asp-net-amp-visual-studio.aspx) na blogu týmu Služby Active Directory.
- [Vývoj víceklientských webových aplikací pomocí](https://msdn.microsoft.com/library/windowsazure/dn151789.aspx) výukového programu Azure AD. Kurz ještě nebyl aktualizován pro Visual Studio 2013; některé z toho, co kurz vás nasměruje k ručnímu je automatizovaná v sadě Visual Studio 2013.
- [Musíte se zaregistrovat s vlastní více organizací ASP.NET app před přihlášením](http://www.cloudidentity.com/blog/2013/10/26/you-have-to-sign-up-with-your-own-multiple-organizations-asp-net-app-before-you-can-sign-in/). Blog od Vittorio Bertocci, který vysvětluje, jak vyřešit běžný problém, se kterým se lidé setkávají při vytváření projektu, který používá ověřování více organizací.

<a id="orgauthonprem"></a>
### <a name="on-premises-organizational-authentication"></a>Místní organizační ověřování

![Místní organizační ověřování](creating-web-projects-in-visual-studio/_static/image26.png)

Tuto možnost zvolte, pokud chcete povolit ověřování pro uživatelské účty, které jsou definovány ve službě Windows Server Active Directory (AD) a nechcete používat Azure AD. Tuto možnost můžete použít k vytvoření intranetové sítě nebo internetového serveru. Pro internetový server použijte službu ADFS (ADFS) pomocí služby ADFS. Další informace naleznete [v tématu Použití možnosti místního organizačního ověřování (ADFS) s ASP.NET ve Visual Studiu 2013](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/).

Pro intranetový web můžete jako alternativu zvolit [ověřování systému Windows](#winauth) místo této možnosti. Pro možnost Ověřování systému Windows není třeba zadejte adresu URL dokumentu metadat. Ověřování systému Windows však neumožňuje řídit přístup k aplikacím ve službě Active Directory nebo dotazovat data adresáře.

#### <a name="on-premises-authority"></a>Místní úřad

Zadejte adresu URL, která odkazuje na dokument metadat. Dokument metadat obsahuje souřadnice autority. Aplikace bude používat tyto souřadnice řídit tok webového přihlášení.

#### <a name="application-id-uri"></a>Identifikátor URI ID aplikace

Zadejte jedinečný identifikátor URI, který může služba AD použít k identifikaci této aplikace, nebo ponechte prázdné, aby ji visual studio vytvořilo.

<a id="nextsteps"></a>
## <a name="next-steps"></a>Další kroky

Tento dokument poskytl některé základní nápovědy pro vytvoření nového ASP.NET webového projektu v sadě Visual Studio 2013. Další informace o použití sady Visual Studio [https://www.asp.net/visual-studio/](../../index.md)pro vývoj webu naleznete v tématu .
