---
uid: web-pages/overview/getting-started/aspnet-web-pages-razor-faq
title: Nejčastější dotazy k ASP.NET webových stránek (Břitva) | Dokumenty společnosti Microsoft
author: Rick-Anderson
description: Tento článek uvádí některé nejčastější dotazy týkající se ASP.NET webových stránek (Razor) a WebMatrix. Verze softwaru použité v kurzu ASP.NET webových stránek (R...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: b137bd04-25e1-47cb-9d96-ef2e179ecf1f
msc.legacyurl: /web-pages/overview/getting-started/aspnet-web-pages-razor-faq
msc.type: authoredcontent
ms.openlocfilehash: a312d1327bc88e721bf7fc7459e420e3f582c88d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543701"
---
# <a name="aspnet-web-pages-razor-faq"></a>Webové stránky ASP.NET (Razor) – časté otázky

, autor: [Tom FitzMacken](https://github.com/tfitzmac)

> > [!NOTE] 
> > WebMatrix se již nedoporučuje jako integrované vývojové prostředí pro ASP.NET webových stránek. Použijte [visual studio](xref:web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio) nebo kód sady Visual [Studio](https://code.visualstudio.com/).
>
> Tento článek uvádí některé nejčastější dotazy týkající se ASP.NET webových stránek (Razor) a WebMatrix.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v kurzu
> 
> 
> - webové stránky ASP.NET (Břitva) 3
> - Visual Studio 2013
> - WebMatrix 3
>   
> 
> Tento kurz funguje také s ASP.NET webových stránek 2, WebMatrix 2 a Visual Studio 2012.

- [Jaký je rozdíl mezi ASP.NET webovými stránkami, ASP.NET webovými formuláři a ASP.NET MVC?](#Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC)
- [Potřebuji k práci s webovými stránkami webmatrix?](#Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages)
- [Lze na stránce webových stránek používat ovládací prvky ASP.NET webových formulářů?](#Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page)
- [Je možné nasadit web ASP.NET webu bez použití aplikace WebMatrix?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)
- [Musím k podpoře přihlášení používat pomocníka WebSecurity?](#Do_I_have_to_use_the_WebSecurity_helper_to_support_logins)
- [Podporuje ASP.NET webových stránek html5?](#Does_ASP.NET_Web_Pages_support_HTML5)
- [Mohu s webovými stránkami používat JavaScript a jQuery?](#Can_I_use_JavaScript_and_jQuery_with_Web_Pages)
- [Další zdroje informací](#AdditionalResources)

Dotazy týkající se chyb a dalších problémů naleznete v [příručce ASP.NET Web Pages (Razor) Troubleshooting Guide](https://go.microsoft.com/fwlink/?LinkId=253001).

<a id="Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC"></a>
## <a name="whats-the-difference-between-aspnet-web-pages-aspnet-web-forms-and-aspnet-mvc"></a>Jaký je rozdíl mezi ASP.NET webovými stránkami, ASP.NET webovými formuláři a ASP.NET MVC?

Všechny tři jsou ASP.NET technologie pro vytváření dynamických webových aplikací:

- ASP.NET webových stránek se zaměřuje na přidávání dynamického kódu (na straně serveru) a přístupu k databázi na stránky HTML a obsahuje jednoduchou a zjednodušenou syntaxi.
- ASP.NET webových formulářů je založen na objektovém modelu stránky a tradičních ovládacích prvcích typu okna (tlačítka, seznamy atd.). Webové formuláře používají model založený na událostech, který je známý těm, kteří pracovali s vývojem na bázi klienta (windows forms).
- ASP.NET MVC implementuje model kontroleru zobrazení modelu pro ASP.NET. Důraz je kladen na "oddělení obav" (zpracování, data a vrstvy ui).

Všechny tři rámce jsou plně podporovány a nadále rozvíjet ASP.NET tým. Obecně platí, že volba, který rámec použít, závisí na vašem pozadí a zkušenostech s ASP.NET.

ASP.NET webových stránek, zejména byl navržen tak, aby bylo snadné pro lidi, kteří již znají HTML přidat zpracování serveru na svých stránkách. Je to dobrá volba pro studenty, fandy, lidi obecně, kteří jsou v programování noví. To může být také dobrou volbou pro vývojáře, kteří mají zkušenosti s non-ASP.NET webových technologií.

<a id="Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages"></a>
## <a name="do-i-need-webmatrix-in-order-to-work-with-web-pages"></a>Potřebuji k práci s webovými stránkami webmatrix?

Ne. WebMatrix se již nedoporučuje jako integrované vývojové prostředí pro ASP.NET webových stránek. Použijte [visual studio](program-asp-net-web-pages-in-visual-studio.md) nebo kód sady Visual [Studio](https://code.visualstudio.com/).

Pokud nechcete používat visual studio nebo kód sady Visual Studio, můžete produkty komponent nainstalovat jednotlivě pomocí [Instalační služby webové platformy společnosti Microsoft](https://www.microsoft.com/web/downloads/platform.aspx). Potřebujete následující produkty:

- Microsoft .NET Framework 4.5
- ASP.NET MVC 5 (který také instaluje rámec ASP.NET webových stránek)
- Služba IIS Express (webový server)
- Microsoft SQL Server Compact 4.0 (databáze)

Textového editoru můžete použít k úpravám stránek *.cshtml* (nebo *.vbhtml).*

Správa sql server kompaktnídatabáze *(.sdf* soubory) bez nástroje je o něco těžší. Visual Studio obsahuje nástroje pro správu databází *SDF.* Můžete také spustit příkazy SQL v kódu k provedení mnoha úloh správy serveru SQL Server.

Chcete-li testovat stránky *.cshtml* bez použití integrovaného vývojového prostředí (IDE), můžete je nasadit na živý server. (Viz [Lze nasadit web ASP.NET webu bez použití webmatrixu?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix))

### <a name="running-iis-express-without-using-an-ide"></a>Spuštění služby IIS Express bez použití ide

Pokud do počítače nainstalujete službu IIS Express jako webový server, můžete ji použít k testování stránek. IIS Express můžete spustit z příkazového řádku a přidružit jej k určitému číslu portu. Tento port pak zadáte, když v prohlížeči požádáte o soubory *.cshtml.*

V systému Windows otevřete příkazový řádek s oprávněními správce a změňte na *C:\Program Files\IIS Express.* (Pro 64bitové systémy použijte složku *C:\Program Files (x86)\IIS Express.)* Potom zadejte následující příkaz pomocí skutečné cesty k webu:

`iisexpress.exe /port:35896 /path:C:\BasicWebSite`

Můžete použít libovolné číslo portu, které ještě není rezervováno jiným procesem. (Čísla portů nad 1024 jsou obvykle zdarma.) Pro `path` tuto hodnotu použijte cestu ke složce webu, kde jsou soubory *.cshtml.*

Po spuštění tohoto příkazu nastavit Službu IIS Express tak, aby zobrazovala vaše stránky, můžete otevřít prohlížeč a přejít na soubor *CSHTML.* Použijte adresu URL takto:

`http://localhost:35896/default.cshtml`

Nápovědu k možnostem příkazového `iisexpress.exe /?` řádku iis express zadejte na příkazovém řádku.

<a id="Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page"></a>
## <a name="can-i-use-aspnet-web-forms-controls-on-a-web-pages-page"></a>Lze na stránce webových stránek používat ovládací prvky ASP.NET webových formulářů?

Ne. Ovládací prvky webových formulářů, jako je ovládací prvek [CheckBox,](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox) [ověřovací ovládací prvky](https://msdn.microsoft.com/library/bwd43d0x)a ovládací prvek [GridView,](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview) fungují pouze na stránkách webových formulářů (*soubory ASPX).* Tyto ovládací prvky vyžadují rámec stránky webových formulářů.

<a id="Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix"></a>
## <a name="can-i-deploy-an-aspnet-web-pages-site-without-using-webmatrix"></a>Je možné nasadit web ASP.NET webu bez použití aplikace WebMatrix?

Ano. Soubory webových stránek můžete ručně kopírovat na server (obvykle pomocí protokolu FTP). Pokud provádíte ruční kopírování, budete muset také zkopírovat soubory, které podporují SQL Server Compact (databáze). Podrobnosti naleznete v položce blogu [Nasazení aplikací webových stránek bez nástroje](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317).

<a id="Do_I_have_to_use_the_WebSecurity_helper_to_support_logins"></a>
## <a name="do-i-have-to-use-the-websecurity-helper-to-support-logins"></a>Musím k podpoře přihlášení používat pomocníka WebSecurity?

Ne. Zprostředkovatel, `SimpleMembership` který je součástí ASP.NET webových stránek, je jednou z možností. K dispozici jsou také poskytovatelé zabezpečení, kteří jsou součástí ASP.NET (se kterými můžete pracovat ve webových formulářích). Ověřování pomocí formulářů můžete například používat ve ASP.NET webových stránek stejně jako ve webových formulářích. Jeden příklad použití ověřování pomocí formulářů naleznete v článku podpory společnosti Microsoft [Jak implementovat ověřování na základě formulářů v aplikaci ASP.NET pomocí jazyka C#.NET](https://support.microsoft.com/kb/301240). Chcete-li stáhnout jednoduchý příklad, viz [ASP.NET verze "Přihlašovací &amp; heslo](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm).

Informace o použití ověřování systému Windows naleznete v příspěvku blogu [Pomocí ověřování systému Windows v ASP.NET webových stránkách](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298).

<a id="Does_ASP.NET_Web_Pages_support_HTML5"></a>
## <a name="does-aspnet-web-pages-support-html5"></a>Podporuje ASP.NET webových stránek html5?

Ano. Stránky, které vytvoříte pomocí ASP.NET webových stránek (*.cshtml* nebo *.vbhtml* stránky) jsou v podstatě HTML stránky, které také obsahují kód, který běží na serveru, před stránka je vykreslen. Dokud prohlížeč uživatele podporuje HTML5, můžete použít elementy HTML5 na stránce *.cshtml* nebo *.vbhtml.*

<a id="Can_I_use_JavaScript_and_jQuery_with_Web_Pages"></a>
## <a name="can-i-use-javascript-and-jquery-with-web-pages"></a>Mohu s webovými stránkami používat JavaScript a jQuery?

Jistě. Stránky, které vytvoříte pomocí ASP.NET webových stránek (*.cshtml* nebo *.vbhtml* stránky) jsou jen HTML stránky s kódem serveru v nich. Proto vše, co můžete udělat v normální html stránky pomocí JavaScript nebo jQuery můžete také udělat v *.cshtml* nebo *.vbhtml* stránky.

Šablona **Počáteční web** v aplikaci WebMatrix obsahuje několik knihoven jQuery. Pokud vytvoříte web pomocí této šablony, složka *Skripty* obsahuje knihovnu jádra jQuery *(jquery-1.6.2.js)* a knihovny pro ověření jQuery (*jquery.validate.js*atd.).

Zde jsou některé blogové příspěvky, které ilustrují způsoby použití jQuery s ASP.NET webových stránek:

- [Přidání jQuery Dobroty na ASP.NET webových stránek pomocí WebMatrix](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/) Rachel Appel
- [5 min: WebMatrix + jQuery UI + json + jQuery šablony](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/) Jonas Eriksson
- [WebMatrix a jQuery formuláře](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms) Mike Brind

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>Další zdroje

[Webové stránky ASP.NET (Razor) – průvodce řešením potíží](https://go.microsoft.com/fwlink/?LinkId=253001)

[Fórum WebMatrix a ASP.NET webových stránek](https://forums.asp.net/1224.aspx/1?WebMatrix) na webu ASP.NET
