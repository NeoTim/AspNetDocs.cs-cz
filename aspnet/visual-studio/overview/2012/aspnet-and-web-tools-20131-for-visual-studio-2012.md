---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: Poznámky k verzi pro ASP.NET a webové nástroje 2013.1 pro Visual Studio 2012 | Dokumenty společnosti Microsoft
author: rick-anderson
description: Tento dokument popisuje vydání ASP.NET a webových nástrojů 2013.1 pro Visual Studio 2012.
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: d4aced4e77a150d52358c2d2513ff79e6594a9de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543571"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>Poznámky k verzi pro ASP.NET a webové nástroje 2013.1 pro Visual Studio 2012

podle [společnosti Microsoft](https://github.com/microsoft)

> Tento dokument popisuje vydání ASP.NET a webových nástrojů 2013.1 pro Visual Studio 2012.

## <a name="contents"></a>Obsah

- [Poznámky k instalaci](#install)
- [Požadavky na software](#requirements)
- Nové funkce v ASP.NET a webových nástrojích 2013.1 pro Visual Studio 2012

    - [Bootstrap](#bootstrap)
    - [Šablony](#templates)

        - [ASP.NET šablonu MVC 5](#mvc5template)
        - [šablona ASP.NET Web API 2](#apitemplate)
        - [Šablony položek](#itemtemplate)
    - [Entity Framework 6](#ef6)
    - [ASP.NET lešení](#scaffold)
    - [Editor břitvy](#razor)
    - [NuGet 2.7](#nuget)
- Známé problémy a nejnovější změny

    - [ASP.NET lešení](#issuescaffolding)

        - [MVC a webové api lešení - HTTP 404, nebyla nalezena chyba](#404issue)
        - [Visual Studio Express 2012 pro web přestane fungovat po přidání položky sádlo](#expressissue)
    - [ASP.NET Břitva 3](#issuerazor)

        - [Zobrazení souboru cshtml pomocí funkce Procházet pomocí nebo F5 způsobí chybu serveru](#browseissue)
        - [Url Přepsat a tilde (~)](#rewriteissue)
    - [Šablony](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a>Poznámky k instalaci

[Instalace](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET a webových nástrojů 2013.1 pro Visual Studio 2012.

<a id="requirements"></a>
## <a name="software-requirements"></a>Požadavky na software

Musíte mít visual studio 2012 nebo Visual Studio Express 2012 pro web.

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>Nové funkce v ASP.NET a webových nástrojích 2013.1 pro Visual Studio 2012

<a id="bootstrap"></a>
### <a name="bootstrap"></a>Bootstrap

Při přichycení mvc 5 řadiče a zobrazení, značky pro zobrazení používá [Bootstrap](http://getbootstrap.com/).

<a id="templates"></a>
### <a name="templates"></a>Šablony

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a>ASP.NET šablonu MVC 5

Přidali jsme novou šablonu MVC 5. Odkazuje na nejnovější balíčky MVC 5 NuGet a můžete použít přisycování uživatelského přilnavého zařízení k přidání řadičů a zobrazení.

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a>šablona ASP.NET Web API 2

Přidali jsme novou šablonu Webové ho rozhraní API 2. Odkazuje na nejnovější webové api 2 NuGet balíčky a můžete použít veslací lišty přidat řadiče a zobrazení.

<a id="itemtemplate"></a>
#### <a name="item-templates"></a>Šablony položek

Přidali jsme nové šablony položek pro zobrazení MVC 5, webové stránky (Razor 3) a řadiče Web API 2. Instalují související balíčky NuGet do projektu při přidávání nových položek.

<a id="ef6"></a>
### <a name="entity-framework-6"></a>Entity Framework 6

Když přistarém ovladači MVC nebo webového rozhraní API pomocí entity Framework, používáme Framework 6. Další informace o rozhraní Entity Framework naleznete v [historii verzí entity frameworku](https://msdn.com/data/jj574253).

Můžete také stáhnout a nainstalovat entity Framework 6 Nástroje pro Visual Studio 2012. Viz [Get Entity Framework](https://msdn.com/data/ee712906#tooling).

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET lešení

ASP.NET generování uživatelského rozhraní je rozhraní pro generování kódu pro ASP.NET webových aplikací. Usnadňuje přidání často používaný kód do projektu, který spolupracuje s datovým modelem.

V předchozích verzích sady Visual Studio bylo lešení omezeno na ASP.NET projekty MVC. Pomocí této aktualizace můžete nyní používat zasanácí číslo pro všechny ASP.NET projektu, včetně webových formulářů. Tato aktualizace nepodporuje generování stránek pro projekt webových formulářů, ale můžete stále používat generování uživatelského formuláře s webovými formuláři přidáním závislostí MVC do projektu. Podpora generování stránek pro webové formuláře bude přidána v budoucí aktualizaci.

Při použití uživatelského přilechrápění zajišťujeme, že jsou v projektu nainstalovány všechny požadované závislosti. Pokud například začnete s projektem ASP.NET webových formulářů a potom pomocí uživatelského rozhraní přidáte řadič webového rozhraní API, budou do projektu automaticky přidány požadované balíčky nuget a odkazy.

Chcete-li přidat uživatelské rozhraní MVC do projektu webových formulářů, přidejte **novou položku scaffolded a** v dialogovém okně vyberte **závislosti MVC 5.** Existují dvě možnosti pro lešení MVC; Minimální a plná. Pokud vyberete Minimální, do projektu se přidají pouze balíčky NuGet a odkazy pro ASP.NET MVC. Pokud vyberete možnost Úplné, budou přidány minimální závislosti a také požadované soubory obsahu pro projekt MVC.

Podpora asynchronních řadičů lešení používá nové asynchronní funkce z entity Framework 6.

Další informace a kurzy naleznete [v tématu ASP.NET Přehled lešení](../2013/aspnet-scaffolding-overview.md). Tyto kurzy ukazují veselení s Visual Studio 2013, ale jsou také použitelné pro ASP.NET a webových nástrojů 2013.1 pro Visual Studio 2012.

<a id="razor"></a>
### <a name="razor-editor"></a>Editor břitvy

S touto aktualizací visual studio 2012 nyní podporuje nástroje a úpravy Razor 3.

<a id="nuget"></a>
### <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7 obsahuje bohatou sadu nových funkcí, které jsou podrobně popsány na [NuGet 2.7 Poznámky k verzi](http://docs.nuget.org/docs/release-notes/nuget-2.7).

Tato verze NuGet odstraňuje potřebu pro uživatele explicitně povolit NuGet obnovit chybějící balíčky. Při instalaci NuGet 2.7 uživatelé implicitně souhlas k automatickému obnovení chybějící balíčky. Uživatelé mohou explicitně odhlásit obnovení balíčku prostřednictvím nastavení NuGet v sadě Visual Studio. Tato změna zjednodušuje fungování obnovení balíčků.

## <a name="known-issues-and-breaking-changes"></a>Známé problémy a nejnovější změny

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET lešení

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC a webové api lešení - HTTP 404, nebyla nalezena chyba

Pokud při přidávání šástavla dojde k chybě, je možné, že projekt zůstane v nekonzistentním stavu. Některé provedené změny se šaše budou vráceny zpět, ale jiné změny, jako jsou například nainstalované balíčky NuGet, nebudou vráceny zpět. Pokud jsou změny konfigurace směrování vráceny zpět, uživatelé obdrží chybu HTTP 404 při navigaci na položky sklopné kódy.

Chcete-li opravit tuto chybu pro MVC, přidejte novou položku scaffolded a vyberte mvc 5 závislosti (minimální nebo úplné). Tento proces přidá všechny požadované změny do projektu.

Oprava této chyby pro webové rozhraní API:

1. Přidejte do projektu následující třídu WebApiConfig.

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. Konfigurace webapiconfig.register v\_metodě Start aplikace v Global.asax takto:

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a>Visual Studio Express 2012 pro web přestane fungovat po přidání položky sádlo

Pokud Visual Studio Express 2012 pro web přestane fungovat po přidání scaffolded položky s entity Framework (například web API 2 Controller s akcemi, pomocí entity Framework), je možné, že Visual Studio Express nepodařilo načíst nativní bitové kopie sestavení závislé na System.Web.Extensions.

Chcete-li tento problém vyřešit, nakonfigurujte aplikaci Visual Studio Express tak, aby fungovala s bitovou kopií msil souboru System.Web.Extensions:

1. Otevřete příkazový řádek v režimu správce.
2. Přejděte na %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE nebo %ProgramFiles(x86)%\Microsoft Visual Studio 11.0\Common7\IDE (pro 64bitový systém Windows).
3. Otevřete v textovém editoru soubor VWDExpress.exe.config.
4. Pod &lt;prvek konfiguračního&gt; &gt;/&lt;runtime přidejte následující řádek:  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. Restartujte visual studio express 2012 pro web.

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a>ASP.NET Břitva 3

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a>Zobrazení souboru cshtml pomocí funkce Procházet pomocí nebo F5 způsobí chybu serveru

Když vytvoříte projekt MVC 5 v sadě Visual Studio 2012 (nebo otevřete v sadě Visual Studio 2012 projekt MVC 5, který byl vytvořen v sadě Visual Studio 2013) a pokusíte se zobrazit soubor cshtml pomocí funkce Procházet pomocí nebo F5, zobrazí se chyba, která uvádí – **Chyba serveru v aplikaci ./.** Server se pokusí přejít na`http://localhost:XXXX/Views/../XXXX.cshtml`

Chcete-li tento problém vyřešit, změňte nastavení **Akce zahájení** v projektu na **Konkrétní stránku**. Není nutné zadat hodnotu pro stránku.

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

Po provedení této změny se výběrem f5 přejde`http://localhost:XXXX`do kořenového adresáře aplikace ( ). Toto chování není stejné jako chování pro projekty MVC 5 v sadě Visual Studio 2013, kde nastavení **Aktuální stránka** spustí otevřenou stránku.

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a>Url Přepsat a tilde (~)

Po upgradu na ASP.NET Razor 3 nebo ASP.NET MVC 5, tilda (~) zápis již nemusí fungovat správně, pokud používáte přepíše URL. Přepsání adresy URL ovlivňuje zápis tildy(~) &lt;v&gt; &lt;elementech&gt; &lt;HTML,&gt;jako je A/ , SCRIPT/ , LINK/ , a v důsledku toho se vlnovka již nemapuje do kořenového adresáře.

Pokud například přepíšete požadavky na **asp.net/content** na **asp.net**, atribut href &lt;v a&gt; href="~/content/"/ **/** se překládá na **/content/content/** místo . Chcete-li potlačit tuto změnu, můžete nastavit kontext **WasUrlRewritten služby IIS\_** na false v každé webové stránce nebo v **aplikaci\_BeginRequest** v Global.asax.

<a id="templateissue"></a>
### <a name="templates"></a>Šablony

Při vytváření ASP.NET projektů MVC pomocí sady Visual Studio 2012 ve Windows 8.1 nebo Windows Server 2012 R2 zobrazí Visual Studio chybovou zprávu s textem Konfigurace webové [url] pro ASP.NET 4.5 se nezdařilo."

![chyba konfigurace](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

Tato chyba se zobrazí, protože Visual Studio 2012 nepovoluje funkci ASP.NET 4.5, když je nainstalována v těchto verzích systému Windows. Chcete-li povolit ASP.NET 4.5, proveďte kroky popsané v [části Zapnutí nebo vypnutí funkcí systému Windows](https://windows.microsoft.com/windows-8/turn-windows-features-on-off).

![zapnutí nebo vypnutí funkcí systému Windows](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

Případně můžete povolit ASP.NET 4.5 prostřednictvím příkazového řádku.

1. Otevřete příkazový řádek v režimu správce.
2. Spusťte následující příkaz, abyste povolili ASP.NET 4.5.  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
