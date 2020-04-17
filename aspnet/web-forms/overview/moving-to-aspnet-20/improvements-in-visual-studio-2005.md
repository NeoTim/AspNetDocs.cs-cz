---
uid: web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
title: Vylepšení sady Visual Studio 2005 | Dokumenty společnosti Microsoft
author: rick-anderson
description: Visual Studio 2005 poskytuje vývojářům webových aplikací dlouhý seznam vylepšení a vylepšení webových projektů.
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 72d90cd0-b3d9-454c-b2eb-ed0d9812f32c
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
msc.type: authoredcontent
ms.openlocfilehash: e98771614bf4e0095f8ff596e7cdb26c8c9de1ad
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542973"
---
# <a name="improvements-in-visual-studio-2005"></a>Vylepšení v sadě Visual Studio 2005

podle [společnosti Microsoft](https://github.com/microsoft)

> Visual Studio 2005 poskytuje vývojářům webových aplikací dlouhý seznam vylepšení a vylepšení webových projektů.

Visual Studio 2005 poskytuje vývojářům webových aplikací dlouhý seznam vylepšení a vylepšení webových projektů. Stejně výkonné jako Visual Studio .NET 2002 a 2003 jsou, bylo mnoho stížností ve způsobu, jakým byly zpracovány webové projekty. Visual Studio 2005 přidává značný počet nových funkcí k řešení těchto stížností. Pro ty, kteří dávají přednost způsobu, jakým Visual Studio .NET 2003 zpracovány kompilace webových aplikací, naleznete v [tématu projekty webových aplikací](https://go.microsoft.com/fwlink/?LinkId=57870).

V tomto modulu dobře pokrýt vylepšení při vytváření, správě a vývoji webových projektů. V pozdějšímodul, dobře pokrýt vylepšení v vytváření webových projektů a jejich nasazení.

## <a name="frontpage-server-extensions"></a>Rozšíření serveru FrontPage

Aplikace Visual Studio .NET 2002 a 2003 vyžadovaly rozšíření FrontPage Server Extensions v poli za účelem vytvoření nebo sestavení webových projektů. Vývojáři měli na výběr mezi dvěma různými režimy přístupu (Rozšíření pro serverová rozšíření nebo Režim přístupu k souborům), oba používali rozšíření FrontPage Server Extensions k provádění úkolů, jako je nastavení kořenového adresáře aplikace ve službách IIS atd.

Visual Studio 2005 odstraňuje závislost na rozšíření frontpage server pro místní projekty. Visual Studio 2005 nyní přistupuje k metabáze služby IIS přímo namísto použití rozšíření FrontPage Server Extensions. Visual Studio 2005 také přidává podporu pro ftp, který umožňuje vzdálený přístup k projektu bez nutnosti rozšíření FrontPage Server Extensions.

Pro vývojáře, kteří chtějí používat rozšíření FrontPage Server Extensions ve svých projektech, je tato možnost stále k dispozici. Na základě silné zpětné vazby od komunity vývojářů ASP.NET však to není požadavek.

> [!NOTE]
> Rozšíření FrontPage Server Extensions jsou stále vyžadována pro vzdálené vytváření, otevírání projektů atd.

## <a name="aspnet-development-server"></a>Vývojový server ASP.NET

Visual Studio 2005 je dodáváno s novým webovým serverem s názvem ASP.NET Development Server. (Tento webový server byl dříve známý jako Cassini.)

Existuje několik výhod ASP.NET Development Server.

- Nyní je možné, aby nesprávci vyvíjeli a ladili webový server.
- ASP.NET Development Server dynamicky mapuje virtuální adresáře do libovolného umístění v systému souborů, což umožňuje flexibilní umístění projektu.
- Uživatelé systému Windows XP Professional, kteří již používají službu IIS, budou nyní moci vytvářet nové webové aplikace, které nebudou mít vliv na strukturu souborů nebo složek výchozího webu ve službě IIS.

Pro využití funkce ASP.NET Vývojového serveru není vyžadována žádná zvláštní konfigurace. Pokud je webový projekt hostovaný v systému souborů laděný nebo procházený, aplikace Visual Studio 2005 automaticky spustí instanci ASP.NET vývojového serveru na náhodném portu, který bude požadavek obsluhovat.

Další informace budou popsány na ASP.NET Development Server dále v tomto modulu.

## <a name="improved-file-management"></a>Vylepšená správa souborů

V sadě Visual Studio 2002 a 2003 ukládal soubor projektu (.vbproj pro VB.NET a .csproj pro C#) informace o všech souborech ve webové aplikaci. Zobrazení Průzkumníka řešení je založeno na informacích o souboru v souboru projektu. Z tohoto důvodu Průzkumník řešení by často zobrazit nepřesné informace v případech, kdy byly použity externí editory. Visual Studio 2002 a 2003 by často přepsat změny souborů nebo není zobrazit nejnovější verzi souborů.

Visual Studio 2005 je odebrána soubor u projektu. Místo toho přečte informace o souboru a složce přímo z disku, což vede k přesnému zobrazení souborů v projektu. Vzhledem k tomu, že složka Reference v sadě Visual Studio 2002 a 2003 nepředstavuje skutečnou složku ve webové aplikaci, aplikace Visual Studio 2005 také odebere složku Reference složky z Průzkumníka řešení. Chcete-li získat přístup k odkazům pro váš projekt v sadě Visual Studio 2005, měli byste použít stránky Vlastnosti pro projekt.

## <a name="creating-web-projects"></a>Vytváření webových projektů

Weboví vývojáři mají k dispozici mnoho nových možností pro vytvoření projektu v sadě Visual Studio 2005. Webové servery lze nyní vytvořit kdekoli v systému souborů a lze je ladit nebo procházet pomocí nového ASP.NET Vývojového serveru. Vývojáři mohou také vytvářet nové weby pomocí ftp.

Klepnutím sem zobrazíte video návod k vytváření webových projektů v sadě Visual Studio 2005.

![](improvements-in-visual-studio-2005/_static/image1.png)

[Otevřít video na celou obrazovku](improvements-in-visual-studio-2005/_static/creating_projects1.wmv)

### <a name="file-system-projects"></a>Projekty systému souborů

Jak jste viděli v návodu k videu, můžete vytvořit webové servery v systému souborů buď v místním počítači, nebo ve vzdáleném umístění prostřednictvím sdílené složky. Weby vytvořené v systému souborů jsou procházeny a laděny pomocí ASP.NET Development Server.

> [!NOTE]
> ASP.NET Development Server může způsobit určité nejasnosti pro zákazníky. Pokud je webový projekt vytvořen v systému souborů ve struktuře adresářů IISs (tj. c:/inetpub/wwwroot), bude web stále procházen prostřednictvím ASP.NET Development Server při spuštění z aplikace Visual Studio 2005. Proto není použitelná žádná konfigurace služby IIS (tj. metody ověřování).

Výchozí webový projekt také odebere velké části režie pouze výchozí stránku.aspx, default.cs soubor a složku App/_Data. Web.config a speciální složky (tj. aplikace/_code) jsou přidány podle potřeby. Webový projekt obsahuje pouze soubory a složky, které potřebujete.

### <a name="http-projects"></a>Projekty HTTP

Projekty PROTOKOLU HTTP mohou být projekty vytvořené na místním webu služby IIS nebo na vzdáleném webu. Výchozí umístění projektu `http://localhost`je . Pokud klepnete na tlačítko Procházet, existují dvě možnosti protokolu HTTP: místní služba IIS a vzdálená lokalita. Hlavní rozdíl v těchto dvou možnostech je metoda, při které jsou informace o webu zobrazeny v dialogovém okně Zvolit umístění a jak jsou soubory zkopírovány na webový server.

Možnost Místní služby IIS přečte informace o webu z metabáze v místním počítači a soubory se zkopírují pomocí systému souborů. Možnost Vzdálený web používá rozšíření FrontPage Server Extensions a informace o webu a soubory jsou zkopírovány pomocí volání vzdáleného volání vzdáleného volání http a serverového serveru.

> [!NOTE]
> Vs###/_tmp.htm soubor a get/_aspx/_ver.aspx se již nepoužívají k určení informace o verzi.

Výchozí možnost http je místní iis. Tato možnost přečte metabáze služby IIS a určí, které weby jsou k dispozici a kde má být obsah vytvářen. Můžete vybrat jinou složku nebo virtuální adresář výběrem ve stromovém zobrazení. Můžete také vytvořit nový virtuální adresář, označit složky jako aplikace a také odstranit existující virtuální adresáře z tohoto dialogového okna.

![Dialogové okno Zvolit umístění](improvements-in-visual-studio-2005/_static/image1.gif)

**Obrázek 1**: Dialogové okno Vybrat umístění

Na rozdíl od dřívějších verzí sady Visual Studio pokud zaškrtnete **políčko Použít vrstvu ssazených soketů** a certifikát SSL neodpovídá adrese URL, kterou procházíte, zobrazí se dialogové okno Výstrahy zabezpečení s dotazem, zda chcete pokračovat. Při použití sady Visual Studio .NET 2003, pokud certifikát nebyl odpovídající, vytvoření projektu by se nezdaří.

![Výstraha zabezpečení týkající se certifikátu SSL](improvements-in-visual-studio-2005/_static/image2.gif)

**Obrázek 2**: Výstraha zabezpečení týkající se certifikátu SSL

### <a name="note-on-host-headers"></a>Poznámka k záhlaví hostitelů

Pokud vytváříte webovou aplikaci na webu vázaném na určitou adresu IP, budete muset zajistit konfiguraci hlavičky hostitele. V opačném případě visual studio `http://localhost`vytvoří web v aplikaci , ale IP adresa se nevyřeší správně při procházení nebo ladění webu z ide.

Pokud vyberete možnost Vzdálený web, dialogové okno se změní, abyste mohli zadat cílovou adresu URL nového webu. Tato adresa URL musí být na serveru s povolenými rozšířeními FrontPage Server Extensions. Chcete-li pracovat s místním webovým serverem pomocí rozšíření FrontPage Server Extensions, můžete použít možnost Vzdálený web a zadat místní adresu URL.

![Vytvoření webu na vzdáleném serveru](improvements-in-visual-studio-2005/_static/image1.jpg)

**Obrázek 3**: Vytvoření webu na vzdáleném serveru

Při vytváření aplikace na vzdáleném webu prostřednictvím ssl, pokud se certifikát SSL neshoduje, potvrzovací dialog se mírně liší od dialogového okna zobrazeného při použití možnosti Místní služba IIS.

![Výstraha zabezpečení vzdáleného webu](improvements-in-visual-studio-2005/_static/image3.gif)

**Obrázek 4**: Výstraha zabezpečení vzdáleného webu

<a id="_Toc116100243"></a>

#### <a name="ftp"></a>FTP

Visual Studio 2005 zavádí možnost vytvářet weby prostřednictvím ftp. Použijete-li tuto možnost, ide vytvoří soubory místně v uživatelské dočasné složce a potom používá FTP přesunout soubory do umístění FTP.

> [!NOTE]
> Umístění dočasné&lt;složky je c:/Documents&gt;and Settings/ User /Local&lt;Settings/Temp/VWDWebCache/ Server&gt;/_&lt;název aplikace&gt;

Při použití možnosti FTP se zobrazí dialogové okno Zvolit umístění. Do tohoto dialogu zadáte požadované informace o připojení FTP, jak je znázorněno níže.

![Dialogové okno Zvolit umístění pro FTP](improvements-in-visual-studio-2005/_static/image2.jpg)

**Obrázek 5**: Dialogové okno Zvolit umístění pro FTP

## <a name="lab-setup-ftp-site-and-create-a-project"></a>Lab: Nastavení serveru FTP a vytvoření projektu

Následující kroky nakonfigurují server FTP tak, aby uživatel měl umístění, do kterého může prostřednictvím protokolu FTP odesílat pouze oni.

### <a name="install-the-ftp-service"></a>Instalace služby FTP

1. Sem Přidat odebrat programy, vyberte Přidat nebo odebrat součásti systému Windows.
2. Vyberte Možnost Internetová informační služba (aplikační server v systému Windows 2003) a klepněte na tlačítko **Podrobnosti**.
3. Zaškrtněte **službu FTP (File Transfer Protocol)** a klepněte na tlačítko **OK**.
4. Chcete-li nainstalovat službu FTP, klepněte na tlačítko **Další.**

### <a name="create-a-new-folder-for-content"></a>Vytvoření nové složky pro obsah

1. V Průzkumníkovi Windows vytvořte novou složku s názvem **Uživatel1** uvnitř aplikace c:/inetpub/wwwroot.

#### <a name="configure-folders-and-permissions-on-folders"></a>Konfigurace složek a oprávnění u složek.

1. Otevřete modul snap-in Internetové informační služby z nástroje pro správu. Nyní budete mít složku Servery FTP pod uzlou název počítače.
2. Rozbalte **servery FTP**.
3. Klepněte pravým tlačítkem myši na **výchozí server FTP**, vyberte **nový**a potom na **položku Virtuální adresář**a potom klepněte na příkaz **Další**.
4. Zadejte **User1** pro název virtuálního adresáře a klepněte na tlačítko **Další**.
5. Zadejte **c:/inetpub/wwwroot/User1** pro cestu a klepněte na tlačítko **Další**.
6. Chcete-li průvodce dokončit, klepněte na tlačítko **Další** a potom na **tlačítko Dokončit.**
7. Klepněte pravým tlačítkem myši na virtuální adresář **Uživatel1** v části Výchozí server FTP a vyberte **příkaz Vlastnosti**.
8. Zaškrtněte políčko **Zaškrtnout** zápis a klepnutím na **tlačítko OK** zavřete dialogové okno.
9. Klepněte pravým tlačítkem myši na **výchozí server FTP** a vyberte **příkaz Vlastnosti**.
10. Na kartě **Účty zabezpečení** zaškrtněte políčko **Povolit anonymní připojení**.
11. V dialogovém okně klepněte na **tlačítko Ano** s dotazem, zda chcete pokračovat.
12. Klepnutím na **tlačítko OK** zavřete dialogové okno.
13. Rozbalte **výchozí web pod** uzlou **webovou sítí.**
14. Klikněte pravým tlačítkem myši na adresář **User1** a vyberte **Vlastnosti.**
15. V části **Nastavení aplikace** klikněte na **Vytvořit** a označte složku jako aplikaci.
16. Klepnutím na **tlačítko OK** zavřete dialogové okno.
17. Zavřete modul snap-in Internetové informační služby.

### <a name="create-web-project"></a>Vytvořit webový projekt

1. Otevřete Visual Studio 2005.
2. V nabídce **Soubor** vyberte **Nový web**.
3. V rozevíracím souboru **Umístění** vyberte **ftp**.
4. Klikněte na **Browse** (Procházet).
5. Do textového pole **Server** zadejte **localhost.**
6. Do textového pole Adresář zadejte **Uživatel1.**
7. Klikněte na **Otevřít**. Umístění FTP bude zadáno do dialogového okna Nový web.
8. Klikněte na tlačítko **OK**.
9. Zrušte zaškrtnutí **políčka Anonymní přihlášení** v dialogovém okně Přihlášení ftp, zadejte pověření a klepněte na tlačítko **OK**.
10. Jaká je adresa URL projektu? (Adresa URL projektu se zobrazí v Průzkumníku řešení.)
11. V nabídce **Sestavení** vyberte **Vytvořit web** nebo **Vytvořit řešení**.
12. Klikněte pravým tlačítkem myši na default.aspx v Průzkumníku řešení a vyberte **Zobrazit v prohlížeči**.
13. V dialogovém okně Adresa `http://localhost/user1` URL webu zadejte adresu URL a klepněte na tlačítko **OK**.

> [!NOTE]
> Pokud se zobrazí chyba označující neschopnost načíst typ /_Default, ujistěte se, že používáte ASP.NET 2.0 na webu a nikoli starší verzi. Můžete to udělat z karty ASP.NET v Internetové informační službě.

## <a name="opening-web-projects"></a>Otevření webových projektů

Otevření webových projektů je podobné vytváření projektů. V následujících částech volat oblasti dávat pozor při práci v rámci ide. Zahrnuje také práci s webovými projekty pomocí HTTP a FTP.

Chcete-li otevřít webový projekt, vyberte v nabídce Soubor položku Otevřít webový server. Budete vyzváni se stejným dialogem Zvolit umístění, který byl dříve zahrnut, a máte k dispozici stejné čtyři možnosti: systém souborů, místní službu IIS, FTP a vzdálený web.

<a id="_Toc116100245"></a>

## <a name="file-system"></a>Systém souborů

Jak je uvedeno dříve v tomto modulu, Visual Studio již používá soubor projektu. Pokud se tedy rozhodnete otevřít web ze systému souborů, máte ve skutečnosti možnost vybrat libovolnou složku, i když vybraná složka nebyla původně vytvořena jako webový projekt v sadě Visual Studio. Můžete například otevřít složku Dokumenty jako web a aplikace Visual Studio ji šťastně otevře a zobrazí soubory, jak je znázorněno níže.

![Dokumenty otevřené jako web](improvements-in-visual-studio-2005/_static/image3.jpg)

**Obrázek 6** *: Dokumenty* otevřené jako web

Vzhledem k tomu, že visual studio pouze vytvoří další soubory a složky v případě potřeby, žádné další soubory nebo složky jsou přidány do umístění, které otevřete. Vedlejším účinkem této architektury je, že zabraňuje vnoření webových serverů v systému souborů. Zvažte například následující strukturu adresáře.

Webový projekt na C:/MyWebSite

Další webový projekt na C:/MyWebSite/Nested

Při otevření webu na adrese c:/MyWebSite se vnořená složka zobrazí jako podsložka této aplikace.

<a id="_Toc116100246"></a>

## <a name="http"></a>HTTP

Při otevírání webových serverů pomocí protokolu HTTP se nastavení čte buď z metabáze služby IIS (Local IIS), nebo pomocí rozšíření FrontPage Server Extensions (Vzdálený web).) Pokud existují vnořené webové aplikace, zobrazí se také s ikonou, která je identifikuje jako aplikaci. Pokud jste obeznámeni s prací s webovými aplikacemi v aplikaci FrontPage, chování v sadě Visual Studio 2005 je podobné.

I když Visual Studio zobrazí ikonu pro aplikace, které jsou vnořené pod aplikací, která je aktuálně otevřena v rámci ide, neumožní rozbalit je zobrazit jejich obsah. Můžete je však dvakrát otevřít. Pokud tak učiníte, zobrazí se dialogové okno s výzvou k otevření webové aplikace (a nahrazení aktuálně otevřeného řešení) nebo k přidání webové aplikace do aktuálního řešení.

![Poklepáním na ikonu vnořené aplikace se zobrazí tento dialog](improvements-in-visual-studio-2005/_static/image4.jpg)

**Obrázek 7**: Poklepánína vnořenou ikonou aplikace vás zobrazí v tomto dialogovém okně

<a id="_Toc116100247"></a>

## <a name="ftp-site"></a>Serveru ftp

Když otevřete web přes FTP, všechny soubory se zkopírují místně do dočasné složky. Úplná cesta pro umístění místního úložiště je zobrazena v podokně Vlastnosti projektu a je vytvořena v následujícím formátu.

C:/Dokumenty a&lt;nastavení/ Uživatel&gt;/Místní nastavení/Temp/VWDWebCache/&lt;Název aplikace /_&gt;&lt;&gt;

Při použití FTP visual studio bude muset zadat základní adresu URL pro váš projekt, takže můžete procházet, jak je znázorněno níže. Pokud nezadáte základní adresu URL, aplikace Visual Studio vás o tuto adresu požádá při prvním pokusu o procházení stránky na webu.

![Určení základní adresy URL pro servery FTP](improvements-in-visual-studio-2005/_static/image5.jpg)

**Obrázek 8**: Určení základní adresy URL pro servery FTP

## <a name="improvements-in-compilation"></a>Vylepšení kompilace

Práce s webovými aplikacemi v sadě Visual Studio 2005 je znatelně rychlejší než předchozí verze. To je způsobeno v nemalé části změny v architektuře kompilace.

V sadě Visual Studio 2002 a 2003 byly webové aplikace zkompilovány do jednoho primárního sestavení, které se ve složce /bin. V sadě Visual Studio 2005 byla přidána složka aplikace nebo _Code. Třídy a další kód bez uznatého kódu jsou přidány do složky App/_Code. Když Visual Studio vytvoří projekt, všechny soubory ve složce App/_Code jsou zkompilovány do jednoho souboru App/_Code.dll. Výsledkem této změny je, že následná sestavení jsou mnohem rychlejší než v předchozích verzích.

> [!NOTE]
> Nástroj příkazového řádku MSBuild lze také použít k vytvoření ASP.NET webových aplikací. Tento nástroj bude zahrnut do modulu 9.

Dalším vylepšením kompilace je nová možnost Sestavit stránku v nabídce Sestavení. Tato funkce umožňuje vývojáři znovu sestavit pouze aktuální stránku (spolu s, samozřejmě, a závislosti), takže změny mohou být kompilovány rychleji. Vzhledem k tomu, že C# nenabízí kompilaci na pozadí pro účely aktualizace technologie IntelliSense atd., budou z této funkce nesmírně těžit, protože umožní rychlou aktualizaci technologie IntelliSense pouhým opětovným sestavením jedné stránky.

Vlastnosti sestavení pro projekt umožňují konfigurovat typ sestavení, ke kterému dochází před spuštěním úvodní stránky. Vývojáři mohou zvolit pouze sestavení aktuální stránky tak, aby Visual Studio můžete spustit ladění aplikací rychleji po změně kódu.

![Akce zahájení stránky sestavení](improvements-in-visual-studio-2005/_static/image6.jpg)

**Obrázek 9**: Akce zahájení stránky sestavení

Další skvělé vylepšení sady Visual Studio a ASP.NET architektura je v oblasti úprav a pokračovat. V sadě Visual Studio 2005 mohou vývojáři spustit ladění projektu a provést změny kódu v projektu bez odpojení ladicího programu. Ve skutečnosti můžete doslova začít ladit projekt, přidat novou třídu, přidat kód do této třídy, přidat kód na stránku, která vytvoří novou instanci této třídy a provede metodu třídy, to vše bez odpojení ladicího programu. Spuštění nového kódu je doslova stejně snadné jako aktualizace prohlížeče!

Kliknutím sem zobrazíte video návod k funkci úprav a pokračování funkce v sadě Visual Studio 2005.

![](improvements-in-visual-studio-2005/_static/image2.png)

[Otevřít video na celou obrazovku](improvements-in-visual-studio-2005/_static/editcontinue1.wmv)

Robustní funkce úprav a pokračování v ASP.NET 2.0 a Visual Studio 2005 je z důvodu změny architektury pro ASP.NET aplikace. V ASP.NET 1.x byly aplikace vytvořené v sadě Visual Studio 2002/2003 zkompilovány do primárního sestavení, které bylo uloženo ve složce /bin. Všechny třídy, stránky atd. Potom za běhu by ASP.NET zkompilovalvšechny ovládací prvky, značky a ASP.NET kód na stránkách a zkopíroval tyto knihovny DLL do dočasné složky ASP.NET.

V sadě Visual Studio 2005 pomocí ASP.NET 2.0 byly výše dva modely kompilace osnovy (jeden pro Visual Studio a jeden pro ASP.NET za běhu) byly sloučeny do jednoho společného modelu kompilace. To znamená, že všechny problémy kompilace jsou nyní zachyceny během fáze vývoje namísto za běhu. Umožňuje také podporu návrháře a technologie IntelliSense pro funkce, jako jsou uživatelské ovládací prvky a stránky předlohy.

Kliknutím sem zobrazíte video návod podpory návrháře pro uživatelské ovládací prvky.

![](improvements-in-visual-studio-2005/_static/image3.png)

[Otevřít video na celou obrazovku](improvements-in-visual-studio-2005/_static/usercontrols1.wmv)

> [!NOTE]
> Při odebrání uživatelského ovládacího prvku @Register ze stránky zůstane direktiva ve značkách a měla by být odebrána ručně, aby se zabránilo chybám analyzátoru, pokud je uživatelský ovládací prvek odstraněn z webu.

Dalším vylepšením modelu kompilace sady Visual Studio je funkce Publikovat web. Vzhledem k tomu, že funkce publikovat předkompilace webu, vývojáři mohou využívat přidané výkon není nutné zkompilovat nic na vyžádání. Také předkompiluje veškerý zdrojový kód ve složce App/_Code do dll tak, aby žádný zdrojový kód musí být nasazen.

![Dialogové okno Publikovat web](improvements-in-visual-studio-2005/_static/image7.jpg)

**Obrázek 10**: Dialog Publikovat web

> [!NOTE]
> Nástroj aspnet/_compile.exe lze také použít k předkompilaci webové aplikace ASP.NET. Tento nástroj bude zahrnut do modulu 9.

Při publikování webu jsou předkompilované soubory uloženy ve složce Dočasné ASP.NET soubory, jak je znázorněno níže. Soubory s *příponou .compiled* jsou soubory XML, které definují závislosti pro konkrétní knihovny DLL. Všechny webové formuláře nebo uživatelské ovládací prvky jsou zkompilovány do náhodných knihoven DLL začínajících *na App/_Web/_*.

Pokud ponecháte zaškrtnuté políčko *Povolit, aby byl tento předkompilovaný web aktualizovatelný,* nebudou značky uvnitř webových formulářů a uživatelských ovládacích prvků předem zkompilovány do dll, což vám umožní provádět změny po nasazení. Pokud dáváte přednost uzamčení značky tak, aby změny nasazeného obsahu nejsou povoleny, zaškrtněte toto políčko.

Zaškrtávací políčko *Použít pevná pojmenování a jednostránková sestavení* umožňuje zakázat dávkovou kompilaci tak, aby byla každá stránka zkompilována do sestavení s pevným názvem. Ponechání tohoto políčka nezaškrtnuté umožňuje využít výhod dávkové kompilace.

Zaškrtávací políčko *Povolit silné pojmenování na předkompilovaných sestaveních* umožňuje silné pojmenování předkompilovaných sestavení.

> [!NOTE]
> V ASP.NET 1.x musela být sestavení se silným názvem nainstalována do globální mezipaměti sestavení (GAC). V ASP.NET 2.0 není nutné instalovat sestavení se silným názvem do gac.

![Předkompilované soubory aplikací ASP.NET](improvements-in-visual-studio-2005/_static/image8.jpg)

**Obrázek 11**: Předkompilované soubory aplikací ASP.NET

> [!NOTE]
> Ve výše uvedené aplikaci nebyl žádný soubor web.config. Pokud by existovala, byla by po procesu publikování webu volána *precompiledApp.config.*

## <a name="improvements-in-deployment"></a>Vylepšení nasazení

Stejně jako v souborech Visual Studio 2002 a 2003 nabízí visual studio 2005 funkci copy projectu. Tato funkce však byla posílena v sadě Visual Studio 2005 a nyní se nazývá Kopírovat web.

Dialogové okno Kopírovat web je rozděleno na levý a pravý rámeček. Levý rámec se nazývá zdrojový web a pravý rámec se nazývá Vzdálený web. Jedna věc, která může zmást některé vývojáře je, že místo zobrazené v pravém rámu není nutně vzdálený web. Může se jedná o web v místním systému souborů nebo v místní instanci služby IIS. Kromě toho web zobrazený v levém rámci nemusí být nutně zdrojovým webem, protože dialogové okno umožňuje publikovat ze vzdáleného webu *na* zdrojový web.

Pokud kopírujete projekt na vzdálený web, musí být na tomto webu nainstalována rozšíření FrontPage Server Extensions. Pokud tomu tak není, budete se muset připojit pomocí FTP. Na druhou stranu, pokud kopírujete projekt do místní instance služby IIS, rozšíření FrontPage Server Extensions nejsou vyžadována.

> [!NOTE]
> Pokud se pokusíte vytvořit nový web v místní instanci služby IIS a jsou nainstalována rozšíření FrontPage 2002 Server Extensions, zobrazí se chybová zpráva, že vytváření webů není na serveru SharePoint podporováno. V takovém případě máte možnost nainstalovat rozšíření FrontPage 2000 Server Extensions nebo odebrat rozšíření FrontPage Server Extensions.

Kliknutím sem zobrazíte video návod k funkci Kopírovat web.

![](improvements-in-visual-studio-2005/_static/image4.png)

[Otevřít video na celou obrazovku](improvements-in-visual-studio-2005/_static/copysite1.wmv)

## <a name="improvements-in-debugging"></a>Vylepšení ladění

Existují čtyři klíčová vylepšení ladění v sadě Visual Studio 2005.

- Ladění místně jako non-správce je možné po vybalení z krabice.
- Atribut Ladění pro element Kompilace je nyní ve výchozím nastavení false.
- Nastavení a konfigurace vzdáleného ladění je jednodušší než dříve.
- Nyní můžete ladit web otevřený prostřednictvím umístění FTP.

## <a name="debugging-as-a-non-administrator"></a>Ladění jako nesprávce

Přidání ASP.NET Development Server umožňuje non-správci snadno ladit ASP.NET aplikace hned po vybalení. Pokud je ASP.NET aplikace spuštěná v místním systému souborů laděna, spustí sada Visual Studio ASP.NET development server v kontextu přihlášeného uživatele. Tento uživatel pak můžete ladit tuto aplikaci bez jakékoli další konfigurace.

## <a name="debug-is-false-by-default"></a>Ladění je ve výchozím nastavení nepravdivé

V ASP.NET 1.x byl atribut *ladění* v elementu *kompilace* souboru web.config ve výchozím nastavení nastaven na *hodnotu true.* Vždy bylo doporučeno, aby vývojáři nastavit tento atribut *false* před nasazením aplikace do produkčního prostředí, ale protože většina vývojářů plně pochopit důsledky opuštění ladicí atribut nastaven na hodnotu true, oni prostě opustil i tak-je.

Nejzávažnější problém s ladění atribut nastaven na hodnotu true je, že zakáže asp.NETs dávkový model kompilace. Proto každá stránka je zkompilován do samostatné dll. Pokud se webová aplikace skládá z tisíců stránek (není neslýchané žádným způsobem), to znamená, že několik tisíc malých Knihoven DLL budou vytvořeny prostřednictvím této aplikace. Zatímco tyto knihovny DLL jsou malé velikosti, nejsou načteny do žádné ho dispono v paměti. Proto způsobit fragmentaci v systémové paměti a může přispět k OutOfMemoryException výskyty.

V ASP.NET 2.0 je ve výchozím nastavení nastaven atribut ladění na hodnotu false. Jak jste již viděli, když vývojář debugs ASP.NET aplikace v sadě Visual Studio 2005, jsou vyzváni k přidání souboru web.config s ladění povoleno. Tím vznikne stejné nevýhody, které byly přítomny v ASP.NET 1.x, ale nyní vývojář je jasně upozorněn, že atribut by měl být obnoven na false před přesunutím aplikace do produkčního prostředí.

## <a name="remote-debugging-setup-and-configuration"></a>Nastavení a konfigurace vzdáleného ladění

V sadě Visual Studio 2002/2003 se vzdálené ladění spoléhalo na správce ladění počítače (mdm.exe) a proces vs7jit.exe. Z tohoto důvodu, řešení problémů vzdálené ladění byl často černá skříňka pro zákazníky, a to často nebylo o moc lepší pro PSS.

Visual Studio 2005 odstraňuje závislost na procesech mdm.exe a vs7jit.exe. Místo toho nyní používá službu Vzdálené sledování ladění (msvsmon.exe.)

Požadavek na ladění v sadě Visual Studio 2005 vzdáleně je poměrně jednoduchý. Před laděním je třeba spustit nástroj msvsmon.exe na vzdáleném serveru. Vzdálený monitor ladění můžete nainstalovat z disku CD-ROM sady Visual Studio nebo můžete jednoduše spustit soubor msvsmon.exe ze sdílené složky bez nutnosti instalace na webový server.

Při spuštění msvsmon.exe, je pravděpodobné, že si bude stěžovat na porty blokovány pro vzdálené ladění. Naštěstí můžete snadno odblokovat porty přímo v rámci dialogového okna varování, jak je znázorněno níže.

![Oznámení, že brána Windows Firewall blokuje vzdálené ladění](improvements-in-visual-studio-2005/_static/image9.jpg)

**Obrázek 12**: Oznámení, že brána Windows Firewall blokuje vzdálené ladění

Jakmile odblokujete porty potřebné pro ladění, zobrazí se monitor vzdáleného ladění, jak je znázorněno níže. Z tohoto rozhraní můžete sledovat připojení a snadno změnit oprávnění k ladění.

![Monitor vzdáleného ladění](improvements-in-visual-studio-2005/_static/image10.jpg)

**Obrázek 13**: Monitor vzdáleného ladění

Je také možné vzdáleně ladit webovou aplikaci otevřenou přes FTP. Kroky jsou stejné jako ty, které byly dříve zahrnuty. Budete však muset zadat základní adresu URL pro procházení projektu FTP, jak je uvedeno výše v tomto modulu.

## <a name="lab-2"></a>Laboratoř 2

## <a name="remote-debugging-with-visual-studio-2005"></a>Vzdálené ladění pomocí sady Visual Studio 2005

Toto testovací prostředí vás provede vzdáleným laděním pomocí sady Visual Studio 2005.

Klikněte zde pro video návod k této laboratoři.

![](improvements-in-visual-studio-2005/_static/image5.png)

[Otevřít video na celou obrazovku](improvements-in-visual-studio-2005/_static/remdebug1.wmv)

Toto testovací prostředí vyžaduje, abyste měli dva počítače, jeden se systémem Visual Studio 2005 a druhý se spuštěnou iis 5 nebo vyšší.

1. Otevřete aplikaci Visual Studio 2005 a vytvořte nový web na vzdáleném serveru.

> [!NOTE]
> Web můžete vytvořit ve vzdálené instanci služby IIS nebo prostřednictvím serveru FTP.

1. Ze vzdáleného webového serveru vyhledejte program msvsmon.exe ve vývojovém počítači pomocí cesty UNC a spusťte jej.  
 Výchozí umístění pro nástroj msvsmon.exe je //server/c$/Program Files/Microsoft Visual Studio 8/Common7/IDE/Remote Debugger/x86.
2. Pokud se zobrazí výzva k odblokování portů pro vzdálené ladění, uvažte.
3. Z vývojového počítače otevřete kód na pozadí pro Default.aspx a nastavte zarážku v Page/_Load metoda.
4. Spusťte ladění z vývojového počítače.

Zarážka by měla být přístupná podle očekávání.

## <a name="aspnet-development-server"></a>Vývojový server ASP.NET

Jak jsme již probrali, visual studio 2005 dodává s webovým serverem s názvem ASP.NET Development Server. (ASP.NET Development Server se někdy označuje jako Cassini.) Tento webový server je pohodlným prostředkem pro procházení a ladění webových aplikací spuštěných v systému souborů.

ASP.NET Development Server je webový server s omezeným přístupem. Neumožňuje vzdálená připojení, neumožňuje žádné požadavky od jiného uživatele než uživatele, který spustil webový server. Také nemá možnost obsluhovat stránky ASP. Jsou obsluhovány pouze ASP.NET prostředky a prostředky HTML (včetně obrázků, souborů CSS atd.).

Vývojový ASP.NET lze spustit prostřednictvím příkazového řádku spuštěním souboru WebDev.WebServer.exe umístěného na adrese c:/Windows/Microsoft.NET/Framework/v2.0./*/*/*/*/*. V následujícím dialogovém okně jsou zobrazeny parametry, které jsou k dispozici.

![](improvements-in-visual-studio-2005/_static/image11.jpg)

**Obrázek 14**

> [!NOTE]
> ASP.NET Development Server není podporován, pokud je explicitně spuštěn prostřednictvím příkazového řádku.
