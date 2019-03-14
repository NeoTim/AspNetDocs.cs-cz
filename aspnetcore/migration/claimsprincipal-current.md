---
title: Migrace z ClaimsPrincipal.Current
author: mjrousos
description: Zjistěte, jak opustit ClaimsPrincipal.Current a získejte aktuálně ověřeného uživatele identity a deklarací identity v ASP.NET Core.
ms.author: scaddie
ms.custom: mvc
ms.date: 05/04/2018
uid: migration/claimsprincipal-current
ms.openlocfilehash: 35c3389798041e141c45bf0a76fa9d7285212768
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57070420"
---
# <a name="migrate-from-claimsprincipalcurrent"></a>Migrace z ClaimsPrincipal.Current

V projektech ASP.NET 4.x, bylo běžné použití [ClaimsPrincipal.Current](/dotnet/api/system.security.claims.claimsprincipal.current) načíst aktuální ověření identity uživatele a deklarace identity. V ASP.NET Core, tato vlastnost je již nastavena. Kód, který byl v závislosti na něm je potřeba aktualizovat tak, aby získejte aktuálně ověřeného uživatele identity různými způsoby.

## <a name="context-specific-data-instead-of-static-data"></a>Specifickým pro kontext dat namísto statických dat

Při použití technologie ASP.NET Core, obě hodnoty `ClaimsPrincipal.Current` a `Thread.CurrentPrincipal` nejsou nastavené. Tyto vlastnosti obě představují statický stav, který ASP.NET Core se obecně vyhnete. Místo toho je architektura ASP.NET Core pro načtení závislostí (jako je aktuální uživatel identity) z kolekcí specifickým pro kontext služby (pomocí jeho [injektáž závislostí](xref:fundamentals/dependency-injection) modelu (DI)). Co je víc, `Thread.CurrentPrincipal` je statická, vlákno, takže se nemusí zachování změn v některých scénářích asynchronní (a `ClaimsPrincipal.Current` jen volá `Thread.CurrentPrincipal` ve výchozím nastavení).

Pochopit druhy problémů vlákno může způsobit statické členy v asynchronní scénáře, zvažte následující fragment kódu:

```csharp
// Create a ClaimsPrincipal and set Thread.CurrentPrincipal
var identity = new ClaimsIdentity();
identity.AddClaim(new Claim(ClaimTypes.Name, "User1"));
Thread.CurrentPrincipal = new ClaimsPrincipal(identity);

// Check the current user
Console.WriteLine($"Current user: {Thread.CurrentPrincipal?.Identity.Name}");

// For the method to complete asynchronously
await Task.Yield();

// Check the current user after
Console.WriteLine($"Current user: {Thread.CurrentPrincipal?.Identity.Name}");
```

Předchozí kód ukázkových sad `Thread.CurrentPrincipal` a ověří jeho hodnotu před a po čekání na asynchronní volání. `Thread.CurrentPrincipal` je specifický pro *vlákno* na kterém je nastavena a metoda je pravděpodobně pokračovat v provádění v jiném vlákně po await. V důsledku toho `Thread.CurrentPrincipal` je k dispozici, když je nejprve zaškrtnuté políčko, ale má hodnotu null po volání `await Task.Yield()`.

Identity aktuálního uživatele z aplikace DI služby kolekce je více možností intenzivního testování, příliš, protože testovací identity můžete snadno vloženy.

## <a name="retrieve-the-current-user-in-an-aspnet-core-app"></a>Načíst aktuální uživatel v aplikaci ASP.NET Core

Existuje několik možností pro načtení aktuálně ověřeného uživatele `ClaimsPrincipal` v ASP.NET Core místo `ClaimsPrincipal.Current`:

* **ControllerBase.User**. Kontrolery MVC můžete přistupovat k aktuálně ověřeného uživatele s jejich [uživatele](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.user) vlastnost.
* **HttpContext.User**. Součásti s přístupem k aktuální `HttpContext` (například middleware) můžete získat aktuální uživatel `ClaimsPrincipal` z [HttpContext.User](/dotnet/api/microsoft.aspnetcore.http.httpcontext.user).
* **Předat z volající**. Knihovny bez přístupu k aktuální `HttpContext` jsou často volány z řadiče nebo middlewarových komponent a může mít aktuální uživatel identitě předané jako argument.
* **IHttpContextAccessor**. Projekt migruje na ASP.NET Core může být příliš velký, aby ke všem místům nezbytné snadno předat identity aktuálního uživatele. V takových případech [IHttpContextAccessor](/dotnet/api/microsoft.aspnetcore.http.ihttpcontextaccessor) lze použít jako alternativní řešení. `IHttpContextAccessor` získat přístup k aktuálním `HttpContext` (pokud existuje). Krátkodobé řešení pro získání aktuálního uživatele identity v kódu, který se ještě neaktualizoval pro práci s architekturou ASP.NET Core řízené DI by byl:

  * Ujistěte se, `IHttpContextAccessor` k dispozici v kontejneru DI voláním [AddHttpContextAccessor](https://github.com/aspnet/Hosting/issues/793) v `Startup.ConfigureServices`.
  * Získat instanci `IHttpContextAccessor` během spouštění a uložte ho do statické proměnné. Instance je k dispozici pro kód, který byl dříve načítání aktuálního uživatele z statickou vlastnost.
  * Načíst aktuální uživatel `ClaimsPrincipal` pomocí `HttpContextAccessor.HttpContext?.User`. Pokud se tento kód používá mimo kontext požadavku protokolu HTTP `HttpContext` má hodnotu null.

Poslední možnost, pomocí `IHttpContextAccessor`, bylo v rozporu s ASP.NET Core zásad (statické závislostí preferují vloženého závislosti). Chcete nakonec odebrat závislost na statické `IHttpContextAccessor` pomocné rutiny. Může být užitečné most, ale při migraci velké existujících aplikací ASP.NET, které dřív používali `ClaimsPrincipal.Current`.
