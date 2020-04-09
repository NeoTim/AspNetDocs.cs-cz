---
uid: web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
title: Ověřování a autorizace ve webovém rozhraní API ASP.NET | Dokumenty společnosti Microsoft
author: MikeWasson
description: Poskytuje obecný přehled ověřování a autorizace v ASP.NET webovérozhraní API.
ms.author: riande
ms.date: 11/27/2012
ms.assetid: 6dfb51ea-9f4d-4e70-916c-8ef8344a88d6
msc.legacyurl: /web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 368d2b9456d12b2bb4063a23333e5c8837faa3b8
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676256"
---
# <a name="authentication-and-authorization-in-aspnet-web-api"></a>Ověřování a autorizace ve webovém rozhraní API ASP.NET

podle [Mike Wasson](https://github.com/MikeWasson)

Vytvořili jste webové rozhraní API, ale nyní chcete řídit přístup k němu. V této sérii článků se podíváme na některé možnosti zabezpečení webového rozhraní API před neoprávněnými uživateli. Tato řada bude zahrnovat ověřování i autorizaci.

- *Ověřování* je znát identitu uživatele. Alice se například přihlásí pomocí svého uživatelského jména a hesla a server použije heslo k ověření Alice.
- *Autorizace* rozhoduje, zda má uživatel povoleno provést akci. Alice má například oprávnění k získání prostředku, ale ne k vytvoření prostředku.

První článek v řadě poskytuje obecný přehled ověřování a autorizace v ASP.NET webové rozhraní API. Další témata popisují běžné scénáře ověřování pro webové rozhraní API.

> [!NOTE]
> Díky lidem, kteří přezkoumali tuto sérii a poskytli cennou zpětnou vazbu: Rick Anderson, Levi Broderick, Barry Dorrans, Tom Dykstra, Hongmei Ge, David Matson, Daniel Roth, Tim Teebken.

## <a name="authentication"></a>Authentication

Webové rozhraní API předpokládá, že k ověřování dochází v hostiteli. Pro webhosting je hostitelem služby IIS, která používá moduly HTTP pro ověřování. Projekt můžete nakonfigurovat tak, aby používal některý z ověřovacích modulů integrovaných do služby IIS nebo ASP.NET, nebo můžete napsat vlastní modul HTTP k provedení vlastního ověřování.

Když hostitel ověří uživatele, vytvoří *objekt zabezpečení*, což je objekt [IPrincipal,](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) který představuje kontext zabezpečení, pod kterým je spuštěn kód. Hostitel připojí objekt zabezpečení k aktuálnímu vláknu nastavením **Thread.CurrentPrincipal**. Objekt zabezpečení obsahuje přidružený objekt **Identity,** který obsahuje informace o uživateli. Pokud je uživatel ověřen, vlastnost **Identity.IsAuthenticated** vrátí **hodnotu true**. U anonymních požadavků **vrátí funkce IsAuthenticated** **hodnotu false**. Další informace o objektových objektech naleznete [v tématu Zabezpečení založené na rolích](https://msdn.microsoft.com/library/shz8h065.aspx).

### <a name="http-message-handlers-for-authentication"></a>Obslužné rutiny zpráv HTTP pro ověřování

Namísto použití hostitele pro ověřování můžete umístit logiku ověřování do [obslužné rutiny zprávy HTTP](../advanced/http-message-handlers.md). V takovém případě obslužná rutina zprávy zkontroluje požadavek HTTP a nastaví jistinu.

Kdy byste měli použít obslužné rutiny zpráv pro ověřování? Zde jsou některé kompromisy:

- Modul HTTP vidí všechny požadavky, které procházejí kanálem ASP.NET. Obslužná rutina zprávy vidí pouze požadavky, které jsou směrovány do webového rozhraní API.
- Můžete nastavit obslužné rutiny zpráv podle trasy, které umožňují použít schéma ověřování pro konkrétní trasu.
- Moduly HTTP jsou specifické pro iis. Obslužné rutiny zpráv jsou nezávislá na hostiteli, takže je lze použít jak s webhostingem, tak s vlastním hostingem.
- Moduly HTTP se účastní protokolování služby IIS, auditování a tak dále.
- Moduly HTTP jsou spuštěny dříve v kanálu. Pokud zpracováváte ověřování v obslužné rutině zprávy, objekt zabezpečení se nenastaví, dokud se obslužná rutina nespustí. Kromě toho hlavní vrátí zpět na předchozí hlavní, když odpověď opustí obslužnou rutinu zprávy.

Obecně platí, že pokud nepotřebujete podporovat vlastní hostování, modul HTTP je lepší volbou. Pokud potřebujete podporovat vlastní hostování, zvažte obslužnou rutinu zprávy.

### <a name="setting-the-principal"></a>Nastavení hlavního povinného

Pokud vaše aplikace provádí vlastní logiku ověřování, musíte nastavit objekt zabezpečení na dvou místech:

- **Thread.CurrentPrincipal**. Tato vlastnost je standardní způsob, jak nastavit objekt zabezpečení vlákna v .NET.
- **HttpContext.Current.User**. Tato vlastnost je specifická pro ASP.NET.

Následující kód ukazuje, jak nastavit jistinu:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

Pro web-hosting, musíte nastavit hlavní na obou místech; v opačném případě může být kontext zabezpečení nekonzistentní. Pro vlastní hostování je však **HttpContext.Current** null. Chcete-li zajistit, aby váš kód byl hostitel-agnostik, proto zkontrolujte null před přiřazením **HttpContext.Current**, jak je znázorněno.

## <a name="authorization"></a>Autorizace

Autorizace se stane později v kanálu, blíže k řadiči. To vám umožní provádět podrobnější volby při udělení přístupu k prostředkům.

- *Filtry autorizace* jsou spuštěny před akcí kontroleru. Pokud požadavek není autorizován, filtr vrátí odpověď na chybu a akce není vyvolána.
- V rámci akce kontroleru můžete získat aktuální objekt zabezpečení z **ApiController.User** vlastnost. Můžete například filtrovat seznam prostředků na základě uživatelského jména a vrátit tak pouze ty prostředky, které patří tomuto uživateli.

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a>Použití atributu [Authorize]

Webové rozhraní API poskytuje integrovaný filtr autorizace [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx). Tento filtr zkontroluje, zda je uživatel ověřen. Pokud ne, vrátí stavový kód HTTP 401 (Neautorizováno), aniž by se odvolal na akci.

Filtr můžete použít globálně, na úrovni kontroleru nebo na úrovni jednotlivých akcí.

**Globálně**: Chcete-li omezit přístup pro každý řadič webového rozhraní API, přidejte filtr **AuthorizeAttribute** do globálního seznamu filtrů:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

**Řadič**: Chcete-li omezit přístup pro konkrétní řadič, přidejte filtr jako atribut k řadiči:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

**Akce**: Chcete-li omezit přístup pro určité akce, přidejte atribut do metody akce:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

Případně můžete omezit řadič a pak povolit anonymní přístup k `[AllowAnonymous]` určité akce pomocí atributu. V následujícím příkladu `Post` je metoda omezena, ale `Get` metoda umožňuje anonymní přístup.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

V předchozích příkladech filtr umožňuje všem ověřeným uživatelům přístup k metodám s omezeným přístupem. pouze anonymní uživatelé jsou drženi mimo. Můžete také omezit přístup na konkrétní uživatele nebo uživatele v určitých rolích:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> Filtr **AuthorizeAttribute** pro řadiče webového rozhraní API je umístěn v oboru názvů **System.Web.Http.** V oboru názvů **System.Web.Mvc** existuje podobný filtr pro řadiče MVC, který není kompatibilní s řadiči webového rozhraní API.

### <a name="custom-authorization-filters"></a>Vlastní filtry autorizace

Chcete-li napsat vlastní autorizační filtr, odvoděte jeden z těchto typů:

- **AuthorizeAttribute**. Rozšiřte tuto třídu tak, aby prováděla logiku autorizace na základě aktuálního uživatele a rolí uživatele.
- **Autorizační atribut FilterAttribute**. Rozšiřte tuto třídu tak, aby prováděla synchronní logiku autorizace, která nemusí být nutně založena na aktuálním uživateli nebo roli.
- **IAuthorizationFilter**. Implementujte toto rozhraní k provedení asynchronní logiky autorizace. například pokud logika autorizace provádí asynchronní vstupně-v nebo síťová volání. (Pokud je logika autorizace vázána na procesor, je jednodušší odvodit z **AuthorizationFilterAttribute**, protože pak není nutné psát asynchronní metodu.)

Následující diagram znázorňuje hierarchii tříd y pro třídu **AuthorizeAttribute.**

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a>Autorizace uvnitř akce řadiče

V některých případech můžete povolit požadavek pokračovat, ale změnit chování na základě jistiny. Například informace, které vrátíte může změnit v závislosti na roli uživatele. V rámci metody kontroleru můžete získat aktuální objekt zabezpečení z **ApiController.User** vlastnost.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]
