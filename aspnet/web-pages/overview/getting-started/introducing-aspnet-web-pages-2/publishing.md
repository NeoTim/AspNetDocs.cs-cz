---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
title: Představení webových stránek ASP.NET – publikování webu pomocí WebMatrixu | Microsoft Docs
author: Rick-Anderson
description: Tento kurz představuje konečnou instalaci v sadě kurzů, která zavádí webové stránky ASP.NET a WebMatrix společnosti Microsoft. Popisuje, jak publikovat web t...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 7e85c70e-1a88-4408-8b3d-29611c7713ed
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
msc.type: authoredcontent
ms.openlocfilehash: a09339a833ea0b4a2d3c3a9323cce777577ea048
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240585"
---
# <a name="introducing-aspnet-web-pages---publishing-a-site-by-using-webmatrix"></a>Představení webových stránek ASP.NET – publikování webu pomocí WebMatrixu

, autor: [Tom FitzMacken](https://github.com/tfitzmac)

> Tento kurz představuje konečnou instalaci v sadě kurzů, která zavádí webové stránky ASP.NET a WebMatrix společnosti Microsoft. Popisuje, jak publikovat web na internetu, aby s ním mohli pracovat i jiní uživatelé. Předpokládá, že jste dokončili sérii [vytvořením konzistentního vzhledu webů webových stránek ASP.NET](https://go.microsoft.com/fwlink/?LinkId=251585).
> 
> Naučíte se, jak web publikovat pomocí:
> 
> - Microsoft Azure
> - Společnost hostující hostování webů

## <a name="about-publishing-your-site"></a>Informace o publikování webu

Nyní jste dokončili veškerou práci na místním počítači, včetně testování vašich stránek. Chcete-li spustit vaše stránky<em>. cshtml</em> , použili jste webový server, který je součástí WebMatrix, konkrétně IIS Express. Ale samozřejmě nikdo uvidí web, který jste vytvořili, s výjimkou vás. Pokud chcete ostatním uživatelům umožnit spolupráci s webem, musíte ho publikovat na internetu.

Pokud už nemáte přístup k veřejnému webovému serveru, publikování znamená, že musíte mít účet s *cloudovou platformou* nebo *poskytovatelem hostingu*. Cloudová platforma, například Microsoft Azure, poskytuje infrastrukturu na vyžádání pro vaše aplikace. Poskytovatel hostingu je společnost, která vlastní veřejně přístupné webové servery a poskytuje místo pro svůj web. Plány hostování jsou spouštěny z několika dolarů za měsíc (nebo dokonce zdarma) pro malé weby na mnoho stovek dolarů měsíčně pro weby s velkým objemem komerčních webů.

> [!NOTE]
> Můžete mít přístup k veřejnému webovému serveru prostřednictvím poskytovatele internetových služeb (ISP), který používáte k získání internetových služeb doma. Poskytovatel hostingu ale musí podporovat webové stránky ASP.NET. Řada poskytovatelů internetových služeb ne, ale je to vždycky kontrolujeme.

V tomto kurzu vám poskytneme přehled o tom, jak publikovat. Není praktické poskytnout přesné podrobnosti pro vše, protože proces se liší od každého poskytovatele hostingu. Ale získáte dobrou představu, jak tento proces funguje.

Tento kurz obsahuje čtyři části:

1. [Nastavení výchozí stránky](#defaultpage)
2. Publikování (vyberte jednu z následujících možností)  
 a. [Publikování webu na Microsoft Azure](#azure)  
 b. [Publikování webu na společnosti hostující na webu](#host)
3. [Aktualizace živého webu: Opětovné publikování](#update)

<a id="defaultpage"></a>
## <a name="setting-up-the-default-page"></a>Nastavení výchozí stránky

Když uživatel přejde na základní adresu webového serveru, zobrazí se uživateli výchozí stránka pro váš web. Například když je *Default.htm* nastavena jako výchozí stránka na webu `www.contoso.com` , pak navigace na `www.contoso.com` je stejná jako navigace na `www.contoso.com/Default.htm` .

V současné době váš web používá jako výchozí stránku **výchozí. cshtml** . Tato stránka je pro výchozí stránku podrobná, ale v tomto kurzu jste do této stránky nepřidali žádný obsah, takže by se zobrazila prázdná stránka. Otevřete default. cshtml a nahraďte obsah následujícím kódem.

[!code-cshtml[Main](publishing/samples/sample1.cshtml)]

Teď je váš web připravený k publikování. Nejdřív se dozvíte, jak nasadit lokalitu do Azure a jak ji nasadit do společnosti pro hostování webů. Jedna možnost funguje pro váš web a stačí provést pouze jednu z možností nasazení.

<a id="azure"></a>
## <a name="publishing-your-site-to-microsoft-azure"></a>Publikování webu na Microsoft Azure

V tomto kurzu nejprve ukážete, jak nasadit web do Microsoft Azure. Když se přihlásíte pomocí účet Microsoft, můžete v Azure vytvořit až 10 bezplatných webů. Tyto bezplatné weby poskytují pohodlný způsob testování vašich webů. Tento ukázkový web můžete kdykoli odstranit později, abyste se vyhnuli používání všech svých bezplatných webů. Můžete si během několika minut vytvořit bezplatný zkušební účet. Podrobnosti najdete v článku [Bezplatná zkušební verze Azure](https://azure.microsoft.com/free/dotnet/).

Na pásu karet WebMatrix klikněte na tlačítko **publikovat** .

![Tlačítko publikovat na pásu karet WebMatrix](publishing/_static/image1.png)

Zobrazí se dialogové okno **publikování webu** . Pokud jste se k vašemu účet Microsoft přihlásili, bude dialogové okno obsahovat odkaz **Začínáme s Azure** . Klikněte na tento odkaz.

![Publikování webu](publishing/_static/image2.png)

Pokud jste se přihlásili k účet Microsoft, budete mít k dispozici možnost přihlásit se. Aby bylo možné publikovat web v Azure, musíte se přihlásit k účet Microsoft.

![Přihlášení](publishing/_static/image3.png)

Po přihlášení k vašemu účet Microsoft dialogové okno obsahuje odkazy na vytvoření nového webu v Azure nebo připojení k některé ze stávajících webů v Azure.

![Vytvořit nový web](publishing/_static/image4.png)

Vyberte **vytvořit novou lokalitu**.

Pokud jste najmenovali svůj projekt jako **WebPagesMovies**, výchozí název vašeho webu bude **webpagesmovies.azurewebsites.NET**. Tento výchozí název není pravděpodobně k dispozici, je-li označen červeným vykřičníkem.

![Název výchozího webu](publishing/_static/image5.png)

Změňte název lokality na něco, co je k dispozici, a vyberte umístění, které je blízko vaší poloze.

![změněný název lokality](publishing/_static/image6.png)

Klikněte na **OK**.

WebMatrix provede test, který určí, jestli je server kompatibilní s vaší lokalitou.

![test kompatibility](publishing/_static/image7.png)

Vyberte **Pokračovat**.

Zobrazí se výsledky testu kompatibility.

![výsledek kompatibility](publishing/_static/image8.png)

Vyberte **Pokračovat**.

WebMatrix zobrazuje soubory a databáze, které budou publikovány na webu. Vzhledem k tomu, že se jedná o první publikování webu, jsou uvedeny všechny soubory. Můžete zrušit kontrolu souboru, který není připravený k publikování. V následujících publikacích se zobrazí pouze soubory, které se změnily. Viz [aktualizace živého webu: Opětovné publikování](#update).

![publikování náhledu](publishing/_static/image9.png)

Vyberte **Pokračovat**.

Po nasazení lokality do Azure se zobrazí zpráva, která indikuje, že nasazení bylo dokončeno.

![publikování dokončeno](publishing/_static/image10.png)

Váš web a databáze byly publikovány do Azure a jsou nyní k dispozici veřejnosti. Klikněte na odkaz ve zprávě oznamující, že publikování se dokončilo, a teď se zobrazí nasazená lokalita. Vy nebo kdokoli s přístupem k Internetu můžete přidávat nebo upravovat záznamy v databázi.

![](publishing/_static/image11.png)

<a id="host"></a>
## <a name="publishing-your-site-to-a-web-hosting-company"></a>Publikování webu na společnosti hostující na webu

Pokud se rozhodnete, že nebudete publikovat do Azure, můžete místo toho publikovat web do společnosti hostující na webu.

Klikněte na odkaz **Najít hostování webu** .

![Tlačítko najít webové hostování v dialogovém okně Nastavení publikování](publishing/_static/image12.png)

Přejdete na stránku na webu společnosti Microsoft, kde jsou uvedeni poskytovatelé hostingu, kteří podporují ASP.NET.

![Na webu společnosti Microsoft, kde jsou uvedeni poskytovatelé hostingu](publishing/_static/image13.png)

Zjevně může být obtížné přesně zjistit, jaké funkce hostování můžete v dlouhodobém období potřebovat. Zvažte několik věcí, které je potřeba vzít v úvahu:

- Pro účely webu WebPagesMovies nemusíte mít k dispozici samostatný doplněk pro SQL Server, což často má za cenu extra. V lokalitě používáte edici SQL Server Compact, která je samostatně obsažená. Pro některé budoucí práce na webu ale může být potřeba SQL Server přístup. Pokud se domníváte, že jste si myslíte, že můžete SQL Server funkci přidat později.
- Ověřte, zda poskytovatel hostingu podporuje protokol publikování Nasazení webu. Můžete publikovat pomocí protokolu FTP, ale je pohodlnější použít Nasazení webu.

Některé weby nabízí bezplatnou zkušební dobu. Bezplatná zkušební verze je dobrým způsobem, jak se pokusit o publikování a hostování při pořád experimentování s webovými stránkami WebMatrix a ASP.NET.

Vyberte takový, který chcete. Pro tento kurz jsme vybrali DiscountASP.NET, protože během vytváření tohoto kurzu byla tato společnost povýšená, která umožňuje lidem hostovat web zdarma po dobu několika měsíců.

> [!NOTE]
> Naše volba poskytovatele hostingu pro účely tohoto kurzu by se neměla interpretovat jako potvrzení této společnosti. Museli jsme ale zvolit pro ilustraci a DiscountASP.NET je jedna z mnoha společností, které podporují webové stránky ASP.NET, a Nasazení webu protokol pro publikování.

Společnost se po registraci k poskytovateli hostingu obvykle pošle e-mailem, který obsahuje uživatelské jméno a heslo, adresu URL webového serveru atd. Pokud hostující společnost podporuje Nasazení webu protokol, může vám odeslat soubor, který obsahuje nastavení publikování, nebo si ho můžete stáhnout. Soubor nastavení publikování zjednodušuje proces.

Po přihlášení a připraven k publikování klikněte na pásu karet WebMatrix na tlačítko **publikovat** . Zobrazí se dialogové okno **publikování nastavení** .

Pokud poskytovatel hostingu poslal soubor nastavení publikování, klikněte na odkaz **importovat nastavení publikování** a importujte soubor. Pokud nemáte soubor nastavení publikování, vyplňte pole pomocí hodnot, které vám hostingová společnost poslala e-mailem. Toto dialogové okno **Nastavení publikování** může vypadat, jako když jste hotovi:

![Nastavení publikování se vyplnila v dialogovém okně publikovat nastavení.](publishing/_static/image14.png)

Klikněte na **ověřit připojení**. Pokud je vše v pořádku, zobrazí se dialogové okno se zprávou **úspěšně připojeno**, což znamená, že může komunikovat se serverem poskytovatele hostingu.

![Zpráva o úspěchu, pokud je nastavení publikování správné](publishing/_static/image15.png)

Pokud dojde k problému, WebMatrix vám nejlépe řekne, co je problém:

![Chybová zpráva, pokud došlo k potížím s nastavením publikování](publishing/_static/image16.png)

Uložte nastavení kliknutím na **Uložit** . WebMatrix nabízí test, aby se zajistilo, že bude moci správně komunikovat s hostitelským webem:

![Nabídka zpráv pro provedení testu procesu publikování](publishing/_static/image17.png)

Klikněte na tlačítko **Ano**. WebMatrix odesílá některé ukázkové soubory poskytovateli hostingu. Po dokončení testu kompatibility vypíše WebMatrix výsledky:

![Výsledky testu publikování](publishing/_static/image18.png)

Pokud jste připraveni přejít, pokračujte a klikněte na **pokračovat** a spusťte proces publikování pro reálný. WebMatrix vyčíslí, které soubory jsou ve vaší lokalitě a které jsou už na hostitelském serveru (hned teď, žádné) a poskytuje náhled procesu publikování:

![Náhled toho, co se soubory, které proces publikování nahraje](publishing/_static/image19.png)

Seznam souborů, které mají být publikovány, obsahuje webové stránky, které jste vytvořili jako *filmy. cshtml*. Seznam obsahuje také soubory pro pomocníky, které jste nainstalovali, soubory, které mají být spuštěny SQL Server Compact Edition pro vaši databázi a tak dále. V důsledku toho může být počáteční proces publikování podstatný.

Klikněte na **Pokračovat**. WebMatrix zkopíruje soubory na server poskytovatele hostingu. Po dokončení se výsledky nahlásí na stavovém řádku:

![Zpráva stavového řádku po úspěšném dokončení procesu publikování](publishing/_static/image20.png)

Pokud chcete zobrazit živý web, klikněte na odkaz ve stavovém řádku. Přidejte do adresy URL *filmy* a zobrazí se soubor *filmů. cshtml* , který jste vytvořili:

![Živý web zobrazující stránku filmů](publishing/_static/image21.png)

<a id="update"></a>
## <a name="updating-the-live-site-republishing"></a>Aktualizace živého webu: Opětovné publikování

Po publikování webu (do Azure nebo do společnosti hostující na webu) se ve &mdash; vašem počítači a ve verzi poskytovatele služby nacházejí dvě kopie IT verze. Pravděpodobně budete chtít pokračovat v vývoji lokality (Pokud nic jiného není v rámci dalšího kurzu sady). V takovém případě je nutné web znovu publikovat, aby bylo možné zkopírovat změny z počítače do poskytovatele služeb. Proces publikování ve WebMatrixu umožňuje určit, které soubory se na vašem webu změnily, a publikovat jenom tyto soubory.

Pokud chcete zjistit, jak funguje opětovné publikování, otevřete web *filmy. cshtml* , udělejte nějakou malou změnu a pak soubor uložte. Například změňte název na `Movies - Updated` .

Klikněte na tlačítko **publikovat** na pásu karet. WebMatrix určuje, co se změnilo, a zobrazí náhled souborů, které bude publikovat.

![Dialogové okno Publikovat zobrazující změněné soubory připravené pro opětovné publikování](publishing/_static/image22.png)

> [!IMPORTANT] 
> 
> Ve výchozím nastavení publikuje WebMatrix vaši databázi (soubor *. sdf* ) pouze při prvním publikování webu. Jakmile je váš web publikovaný a lidé budou spolupracovat na webu, databáze na živém webu má obvykle skutečná data lokality. Musíte být velmi opatrní, nemusíte přepsat živou databázi souborem *. sdf* , který je ve vašem počítači, což obvykle obsahuje pouze testovací data. To je důvod, proč se zobrazí upozornění, že při **publikování dojde k přepsání všech vzdálených databází**a proč je ve výchozím nastavení zaškrtnuté políčko pro *WebPagesMovies. sdf* .

Klikněte na **Pokračovat**. WebMatrix publikuje změněné soubory a zobrazí zprávu o úspěchu, třeba při prvním publikování.

Přejděte na živý web (můžete kliknout na odkaz ve zprávě o úspěchu, pokud se pořád zobrazuje) a ověřit, jestli se vaše změna publikovala.

> [!TIP] 
> 
> **Vzdálená úprava souborů**
> 
> Jako alternativu ke změně lokality a následnému opětovnému publikování můžete upravovat vzdálené soubory přímo v WebMatrixu. V tomto scénáři otevřete soubor, který je na poskytovateli služeb, a WebMatrix stáhne kopii IT, kterou si můžete upravit. Pokaždé, když soubor uložíte, WebMatrix odešle změny do webu.
> 
> Vzdálené úpravy jsou snadný způsob, jak provádět změny v živém webu. Změny, které provedete tímto způsobem, však nejsou synchronizovány se soubory v místní lokalitě. Chcete-li synchronizovat místní soubory se vzdálenou lokalitou, můžete stáhnout vzdálené soubory. Tento proces funguje podobně jako publikování, s výjimkou reverzních.
> 
> Další informace o zařízeních WebMatrix pro vzdálenou úpravu a vzdálené stažení tady nepopisujeme. Jsou poměrně užitečné, pokud více lidí musí pracovat na stejné lokalitě v různých počítačích. Další informace najdete v tématu [publikování a úprava vzdáleného webu pomocí WebMatrix 2 beta](https://go.microsoft.com/fwlink/?LinkId=251591).

## <a name="additional-resources"></a>Další zdroje

- [ASP.NET Fórum webových stránek WebMatrix ASP.NET](https://forums.asp.net/1224.aspx/1?WebMatrix+and+ASP+NET+Web+Pages), což je skvělé místo pro publikování otázek a získání odpovědí.

> [!div class="step-by-step"]
> [Předchozí](layouts.md)
