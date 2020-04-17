---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-cs
title: Ověřování uživatelů pomocí ověřování pomocí formulářů (C#) | Dokumenty společnosti Microsoft
author: rick-anderson
description: Přečtěte si, jak používat atribut [Authorize] k ochraně určitých stránek heslem v aplikaci MVC. Naučíte se, jak používat webové stránky správy příliš ...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 239fd3ca-5630-4b8d-bc4b-2f906b1d3504
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: f14f996c0b3a438647b5d181675457735e473354
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540971"
---
# <a name="authenticating-users-with-forms-authentication-c"></a>Ověřování uživatelů pomocí formulářů (C#)

podle [společnosti Microsoft](https://github.com/microsoft)

> Přečtěte si, jak používat atribut [Authorize] k ochraně určitých stránek heslem v aplikaci MVC. Dozvíte se, jak pomocí Nástroje pro správu webu vytvářet a spravovat uživatele a role. Dozvíte se také, jak nakonfigurovat, kde jsou uloženy informace o uživatelském účtu a roli.

Cílem tohoto kurzu je vysvětlit, jak můžete pomocí ověřování pomocí formulářů chránit zobrazení v aplikacích ASP.NET MVC. Dozvíte se, jak pomocí Nástroje pro správu webu vytvářet uživatele a role. Dozvíte se také, jak zabránit neoprávněným uživatelům v vyvolání akcí řadiče. Nakonec se dozvíte, jak nakonfigurovat, kde jsou uložena uživatelská jména a hesla.

#### <a name="using-the-web-site-administration-tool"></a>Použití Nástroje pro správu webu

Než budeme dělat něco jiného, měli bychom začít tím, že vytvoří některé uživatele a role. Nejjednodušší způsob, jak vytvořit nové uživatele a role, je využít výhod nástroje pro správu webu sady Visual Studio 2008. Tento nástroj můžete spustit výběrem možnosti nabídky **Projekt, ASP.NET Konfigurace**. Případně můžete spustit Nástroj pro správu webu kliknutím na (poněkud děsivou) ikonu kladiva, která zasáhne svět, který se zobrazí v horní části okna Průzkumníka řešení (viz obrázek 1).

**Obrázek 1 – Spuštění nástroje pro správu webu**

![clip_image002](authenticating-users-with-forms-authentication-cs/_static/image1.jpg)

V nástroji pro správu webu vytvoříte nové uživatele a role výběrem karty Zabezpečení. Klepnutím na odkaz **Vytvořit uživatele** vytvoříte nového uživatele s názvem Stephen (viz obrázek 2). Zadejte uživateli Stephen libovolné heslo, které chcete (například *tajné).*

**Obrázek 2 – Vytvoření nového uživatele**

![clip_image004](authenticating-users-with-forms-authentication-cs/_static/image2.jpg)

Nové role vytvoříte tak, že nejprve povolíte role a definujete jednu nebo více rolí. Povolte role kliknutím na odkaz **Povolit role.** Dále vytvořte roli s názvem *Správci* kliknutím na odkaz **Vytvořit nebo spravovat role** (viz obrázek 3).

**Obrázek 3 – Vytvoření nové role**

![clip_image006](authenticating-users-with-forms-authentication-cs/_static/image3.jpg)

Nakonec vytvořte nového uživatele s názvem Sally a přidružte Sally k roli Administrators klepnutím na odkaz Vytvořit uživatele a výběrem správců při vytváření Sally (viz obrázek 4).

**Obrázek 4 – Přidání uživatele do role**

![clip_image008](authenticating-users-with-forms-authentication-cs/_static/image4.jpg)

Když je vše řečeno a vykonáno, měli byste mít dva nové uživatele jménem Stephen a Sally. Měli byste mít také novou roli s názvem Správci. Sally je členem role Administrators a Stephen není.

#### <a name="requiring-authorization"></a>Vyžadování autorizace

Můžete vyžadovat, aby byl uživatel ověřen dříve, než uživatel vyvolá akci kontroleru přidáním atributu [Authorize] k akci. Atribut [Authorize] můžete použít na jednotlivé akce řadiče nebo můžete použít tento atribut pro celou třídu kontroleru.

Například řadič v Listing 1 zpřístupňuje akci s názvem CompanySecrets(). Vzhledem k tomu, že tato akce je dekorována atributem [Authorize], nelze tuto akci vyvolat, pokud není ověřen uživatel.

**Výpis 1 – Řadiče\HomeController.cs**

[!code-csharp[Main](authenticating-users-with-forms-authentication-cs/samples/sample1.cs)]

Pokud vyvoláte akci CompanySecrets() zadáním adresy URL /Home/CompanySecrets do adresního řádku prohlížeče a nejste ověřeným uživatelem, budete automaticky přesměrováni do zobrazení Přihlášení (viz obrázek 5).

**Obrázek 5 – Zobrazení přihlášení**

![clip_image010](authenticating-users-with-forms-authentication-cs/_static/image5.jpg)

Pomocí zobrazení Přihlášení můžete zadat své uživatelské jméno a heslo. Pokud nejste registrovaným uživatelem, můžete kliknutím na odkaz **registru** přejít do zobrazení Registr (viz obrázek 6). Pomocí zobrazení Registr můžete vytvořit nový uživatelský účet.

**Obrázek 6 – Zobrazení registru**

![clip_image012](authenticating-users-with-forms-authentication-cs/_static/image6.jpg)

Po úspěšném přihlášení se zobrazí zobrazení CompanySecrets (viz obrázek 7). Ve výchozím nastavení budete nadále přihlášeni, dokud nezavřete okno prohlížeče.

**Obrázek 7 – Zobrazení CompanySecrets**

![clip_image014](authenticating-users-with-forms-authentication-cs/_static/image7.jpg)

#### <a name="authorizing-by-user-name-or-user-role"></a>Autorizace podle uživatelského jména nebo uživatelské role

Atribut [Authorize] můžete použít k omezení přístupu k akci kontroleru na určitou sadu uživatelů nebo určitou sadu uživatelských rolí. Například upravený domácí řadič v seznamu 2 obsahuje dvě nové akce s názvem StephenSecrets() a AdministratorSecrets().

**Výpis 2 – Řadiče\HomeController.cs**

[!code-csharp[Main](authenticating-users-with-forms-authentication-cs/samples/sample2.cs)]

Pouze uživatel s uživatelským jménem Stephen může vyvolat StephenSecrets() akce. Všichni ostatní uživatelé budou přesměrováni do zobrazení Přihlášení. Vlastnost Users přijímá seznam názvů uživatelských účtů oddělených čárkami.

Akci AdministratorSecrets() mohou vyvolat pouze uživatelé v roli Administrators. Například protože Sally je členem skupiny Administrators, může vyvolat akci AdministratorSecrets(). Všichni ostatní uživatelé budou přesměrováni do zobrazení Přihlášení. Vlastnost Role přijímá seznam názvů rolí oddělený chod čárek.

#### <a name="configuring-authentication"></a>Konfigurace ověřování

V tomto okamžiku se možná divíte, kde jsou uloženy informace o uživatelském účtu a roli. Ve výchozím nastavení jsou informace uloženy v databázi (RANU) SQL Express s názvem ASPNETDB.mdf umístěné ve složce Data aplikací\_aplikace MVC. Tato databáze je generována ASP.NET rámci automaticky při spuštění členství.

Chcete-li zobrazit databázi ASPNETDB.mdf v okně Průzkumník řešení, musíte nejprve vybrat možnost nabídky Projekt, Zobrazit všechny soubory.

Použití výchozí databáze SQL Express je v pořádku při vývoji aplikace. S největší pravděpodobností však nebudete chtít použít výchozí databázi ASPNETDB.mdf pro produkční aplikaci. V takovém případě můžete změnit, kde jsou uloženy informace o uživatelském účtu, provedením následujících dvou kroků:

1. Přidání databázových objektů aplikačních služeb do produkční databáze – Změňte připojovací řetězec aplikace tak, aby přectol na produkční databázi.

Prvním krokem je přidání všech potřebných databázových objektů (tabulek a uložených procedur) do produkční databáze. Nejjednodušší způsob, jak přidat tyto objekty do nové databáze, je využít ASP.NET Průvodce instalací serveru SQL Server (viz obrázek 8). Tento nástroj můžete spustit otevřením příkazového řádku sady Visual Studio 2008 ze skupiny programů sady Microsoft Visual Studio 2008 a spuštěním následujícího příkazu z příkazového řádku:

aspnet\_regsql

**Obrázek 8 – Průvodce instalací serveru ASP.NET SQL Server**

![clip_image016](authenticating-users-with-forms-authentication-cs/_static/image8.jpg)

Průvodce instalací serveru ASP.NET SQL Server umožňuje vybrat databázi serveru SQL Server v síti a nainstalovat všechny databázové objekty vyžadované ASP.NET aplikačními službami. Databázový server nemusí být umístěn v místním počítači.

> [!NOTE] 
> 
> Pokud nechcete používat Průvodce instalací ASP.NET serveru SQL Server, můžete najít skripty SQL pro přidání databázových objektů aplikačních služeb v následující složce:
> 
> > C:\Windows\Microsoft.NET\Framework\v2.0.50727

Po vytvoření potřebných databázových objektů je třeba upravit připojení databáze používané aplikací MVC. Upravte připojovací řetězec ApplicationServices ve webové konfiguraci (web.config) souboru tak, aby odkazuje na produkční databázi. Například upravené připojení v Výpis 3 odkazuje na databázi s názvem MyProductionDB (původní applicationservices připojovací řetězec byl zakomentován).

**Výpis 3 - Web.config**

[!code-xml[Main](authenticating-users-with-forms-authentication-cs/samples/sample3.xml)]

#### <a name="configuring-database-permissions"></a>Konfigurace oprávnění databáze

Pokud používáte integrované zabezpečení pro připojení k databázi, pak budete muset přidat správný uživatelský účet systému Windows jako přihlášení do databáze. Správný účet závisí na tom, zda jako webový server používáte ASP.NET Development Server nebo Internetovou informační službu. Správný uživatelský účet také závisí na operačním systému.

Pokud používáte ASP.NET Development Server (výchozí webový server používaný aplikací Visual Studio), aplikace se spustí v kontextu uživatelského účtu systému Windows. V takovém případě je třeba přidat uživatelský účet systému Windows jako přihlášení databázového serveru.

Pokud používáte Internetovou informační službu, je třeba přidat buď účet ASPNET, nebo účet NT AUTHORITY/NETWORK SERVICE jako přihlášení k databázovému serveru. Pokud používáte systém Windows XP, přidejte účet ASPNET jako přihlášení do databáze. Pokud používáte novější operační systém, například Windows Vista nebo Windows Server 2008, přidejte jako přihlášení do databáze účet NT AUTHORITY/NETWORK SERVICE.

Nový uživatelský účet můžete do databáze přidat pomocí aplikace Microsoft SQL Server Management Studio (viz obrázek 9).

**Obrázek 9 – Vytvoření nového přihlášení k serveru Microsoft SQL Server**

![clip_image018](authenticating-users-with-forms-authentication-cs/_static/image9.jpg)

Po vytvoření požadované přihlášení, je třeba mapovat přihlášení do databáze uživatele s správné databázové role. Poklepejte na přihlášení a vyberte kartu Mapování uživatelů. Chcete-li například ověřit uživatele, musíte povolit\_databázovou roli aspnet Membership\_BasicAccess. Chcete-li vytvořit nové uživatele, je třeba\_povolit roli databáze Aspnet Membership\_FullAccess (viz obrázek 10).

**Obrázek 10 – Přidání rolí databáze aplikačních služeb**

![clip_image020](authenticating-users-with-forms-authentication-cs/_static/image10.jpg)

#### <a name="summary"></a>Souhrn

V tomto kurzu jste se naučili používat ověřování pomocí formulářů při vytváření ASP.NET aplikace MVC. Nejprve jste se naučili vytvářet nové uživatele a role využitím nástroje pro správu webu. Dále jste se dozvěděli, jak pomocí atributu [Authorize] zabránit neoprávněným uživatelům v vyvolání akcí řadiče. Nakonec jste se dozvěděli, jak nakonfigurovat aplikaci MVC pro ukládání informací o uživatelích a rolích v produkční databázi.

> [!div class="step-by-step"]
> [Další](authenticating-users-with-windows-authentication-cs.md)
