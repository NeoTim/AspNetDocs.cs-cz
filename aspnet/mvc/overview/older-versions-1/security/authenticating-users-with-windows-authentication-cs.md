---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-cs
title: Ověřování uživatelů pomocí ověřování systému Windows (C#) | Dokumenty společnosti Microsoft
author: rick-anderson
description: Naučte se používat ověřování systému Windows v kontextu aplikace MVC. Dozvíte se, jak povolit ověřování systému Windows v rámci webové aplikace co ...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 418bb07e-f369-4119-b4b0-08f890f7abb2
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: fb6ba3d52d7c70d61c6aa16b4ada67cc6bdd4f96
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540737"
---
# <a name="authenticating-users-with-windows-authentication-c"></a>Ověřování uživatelů pomocí ověřování systému Windows (C#)

podle [společnosti Microsoft](https://github.com/microsoft)

> Naučte se používat ověřování systému Windows v kontextu aplikace MVC. Dozvíte se, jak povolit ověřování systému Windows v rámci webového konfiguračního souboru aplikace a jak konfigurovat ověřování pomocí služby IIS. Nakonec se dozvíte, jak pomocí atributu [Authorize] omezit přístup k akcím řadiče na konkrétní uživatele nebo skupiny systému Windows.

Cílem tohoto kurzu je vysvětlit, jak můžete využít funkce zabezpečení integrované do Internetové informační služby k ochraně hesel zobrazení v aplikacích MVC. Dozvíte se, jak povolit akce kontroleru, které mají být vyvolány pouze konkrétní uživatelé systému Windows nebo uživatelé, kteří jsou členy konkrétní skupiny systému Windows.

Použití ověřování systému Windows dává smysl při vytváření interního webu společnosti (intranetového webu) a chcete, aby uživatelé mohli při přístupu na web používat svá standardní uživatelská jména a hesla systému Windows. Pokud vytváříte vnější web (internetový web), zvažte místo toho použití ověřování pomocí formulářů.

#### <a name="enabling-windows-authentication"></a>Povolení ověřování systému Windows

Při vytváření nové aplikace ASP.NET MVC není ověřování systému Windows ve výchozím nastavení povoleno. Ověřování pomocí formulářů je výchozí typ ověřování povolený pro aplikace MVC. Ověřování systému Windows je nutné povolit úpravou souboru webové konfigurace aplikace MVC (web.config). Vyhledejte &lt;&gt; část ověřování a upravte ji tak, aby používala systém Windows místo ověřování pomocí formulářů takto:

[!code-xml[Main](authenticating-users-with-windows-authentication-cs/samples/sample1.xml)]

Povolíte-li ověřování systému Windows, bude webový server odpovědný za ověřování uživatelů. Obvykle existují dva různé typy webových serverů, které se používají při vytváření a nasazování aplikace ASP.NET MVC.

Nejprve při vývoji aplikace MVC použijete webový server ASP.NET Development, který je součástí sady Visual Studio. Ve výchozím nastavení ASP.NET Development Web Server spouští všechny stránky v kontextu aktuálního účtu systému Windows (bez ohledu na účet, který jste použili k přihlášení k systému Windows).

Webový server ASP.NET Development také podporuje ověřování NTLM. Ověřování NTLM můžete povolit tak, že kliknete pravým tlačítkem myši na název projektu v okně Průzkumník řešení a vyberete vlastnosti. Dále vyberte webovou kartu a zaškrtněte políčko NTLM (viz obrázek 1).

**Obrázek 1 – Povolení ověřování NTLM pro webový server ASP.NET Development**

![clip_image002](authenticating-users-with-windows-authentication-cs/_static/image1.jpg)

Pro produkční webovou aplikaci používáte službu IIS jako webový server. Službu IIS podporuje několik typů ověřování, včetně:

- Základní ověřování – definováno jako součást protokolu HTTP 1.0. Odesílá uživatelská jména a hesla ve prostém textu (Base64 kódované) přes Internet. - Digest Ověřování - Odešle hash hesla, místo hesla samotného, přes internet. - Integrované ověřování systému Windows (NTLM) – nejlepší typ ověřování pro použití v intranetových prostředích pomocí oken. - Ověřování certifikátu – umožňuje ověřování pomocí certifikátu na straně klienta. Certifikát se mapuje na uživatelský účet systému Windows.

> [!NOTE] 
> 
> Podrobnější přehled těchto různých typů ověřování naleznete [https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx)v tématu .

Pomocí Správce Internetové informační služby můžete povolit určitý typ ověřování. Uvědomte si, že všechny typy ověřování nejsou k dispozici v případě každého operačního systému. Pokud navíc používáte službu IIS 7.0 se systémem Windows Vista, budete muset před zobrazením ve Správci Internetové informační služby povolit různé typy ověřování systému Windows. Otevřete **Ovládací panely, Programy, programy a funkce, zapněte nebo vypněte funkce systému Windows**a rozbalte uzel Internetové informační služby (viz obrázek 2).

**Obrázek 2 – Povolení funkcí služby IIS systému Windows**

![clip_image004](authenticating-users-with-windows-authentication-cs/_static/image2.jpg)

Pomocí Internetové informační služby můžete povolit nebo zakázat různé typy ověřování. Obrázek 3 například znázorňuje zakázání anonymního ověřování a povolení integrovaného ověřování systému Windows (NTLM) při použití služby IIS 7.0.

**Obrázek 3 – Povolení integrovaného ověřování systému Windows**

![clip_image006](authenticating-users-with-windows-authentication-cs/_static/image3.jpg)

#### <a name="authorizing-windows-users-and-groups"></a>Autorizace uživatelů a skupin systému Windows

Po povolení ověřování systému Windows můžete pomocí atributu [Authorize] řídit přístup k řadičům nebo akcím řadiče. Tento atribut lze použít pro celý řadič MVC nebo konkrétní akce řadiče.

Například home controller v listing 1 zveřejňuje tři akce s názvem Index(), CompanySecrets(), a StephenSecrets(). Akce Index() může vyvolat kdokoli. Akce CompanySecrets() však mohou vyvolat pouze členové skupiny místní manažeři systému Windows. Nakonec pouze uživatel domény systému Windows s názvem Stephen (v doméně Redmond) můžete vyvolat StephenSecrets() akce.

**Výpis 1 – Řadiče\HomeController.cs**

[!code-csharp[Main](authenticating-users-with-windows-authentication-cs/samples/sample2.cs)]

> [!NOTE] 
> 
> Z důvodu řízení uživatelských účtů systému Windows (UAC) se bude místní skupina Administrators při práci se systémem Windows Vista nebo Windows Server 2008 chovat jinak než ostatní skupiny. Atribut [Authorize] nerozpozná správně člena místní skupiny Administrators, pokud nezměníte nastavení nástroje Nastavení nástroje Nastavení přístupu k systému Připojení k systému Připojení k systému Připojení k systému Souborů a dat v počítači.

Přesně to, co se stane, když se pokusíte vyvolat akci řadiče, aniž by byla správná oprávnění závisí na typu ověřování povoleno. Ve výchozím nastavení, při použití ASP.NET Development Server, stačí získat prázdnou stránku. Stránka je doručena se **stavem odpovědi 401 Není autorizována** odpověď HTTP.

Pokud na druhé straně používáte službu IIS se zakázaným anonymním ověřováním a ověřováním basic, zobrazí se při každém požadavku na chráněnou stránku přihlašovací dialogové okno ( viz obrázek 4).

**Obrázek 4 – Dialogové okno základního přihlášení při ověřování**

![clip_image008](authenticating-users-with-windows-authentication-cs/_static/image4.jpg)

#### <a name="summary"></a>Souhrn

Tento kurz vysvětlil, jak můžete použít ověřování systému Windows v kontextu aplikace ASP.NET MVC. Zjistili jste, jak povolit ověřování systému Windows v rámci webového konfiguračního souboru aplikace a jak konfigurovat ověřování pomocí služby IIS. Nakonec jste se naučili, jak pomocí atributu [Authorize] omezit přístup k akcím řadiče na konkrétní uživatele nebo skupiny systému Windows.

> [!div class="step-by-step"]
> [Předchozí](authenticating-users-with-forms-authentication-cs.md)
> [další](preventing-javascript-injection-attacks-cs.md)
