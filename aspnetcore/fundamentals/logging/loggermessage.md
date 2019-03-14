---
title: Vysoce výkonné protokolování pomocí LoggerMessage v ASP.NET Core
author: guardrex
description: Další informace o použití LoggerMessage k vytváření delegátů možné ukládat do mezipaměti, které vyžadují méně přidělení objektů pro scénáře protokolování vysoce výkonné.
ms.author: riande
ms.date: 11/03/2017
uid: fundamentals/logging/loggermessage
ms.openlocfilehash: a0080a20fed2d8fc295e55822c11d5731c6910ca
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57073228"
---
# <a name="high-performance-logging-with-loggermessage-in-aspnet-core"></a><span data-ttu-id="04349-103">Vysoce výkonné protokolování pomocí LoggerMessage v ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="04349-103">High-performance logging with LoggerMessage in ASP.NET Core</span></span>

<span data-ttu-id="04349-104">Podle [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="04349-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="04349-105">[LoggerMessage](/dotnet/api/microsoft.extensions.logging.loggermessage) funkcí vytvořit možné ukládat do mezipaměti delegáty, které vyžadují méně přidělení objektů a snížené nadměrnou výpočetní zátěž ve srovnání s [metody rozšíření protokolování](/dotnet/api/Microsoft.Extensions.Logging.LoggerExtensions), jako například `LogInformation`, `LogDebug`, a `LogError`.</span><span class="sxs-lookup"><span data-stu-id="04349-105">[LoggerMessage](/dotnet/api/microsoft.extensions.logging.loggermessage) features create cacheable delegates that require fewer object allocations and reduced computational overhead compared to [logger extension methods](/dotnet/api/Microsoft.Extensions.Logging.LoggerExtensions), such as `LogInformation`, `LogDebug`, and `LogError`.</span></span> <span data-ttu-id="04349-106">Pro scénáře protokolování vysoce výkonné, použijte `LoggerMessage` vzor.</span><span class="sxs-lookup"><span data-stu-id="04349-106">For high-performance logging scenarios, use the `LoggerMessage` pattern.</span></span>

<span data-ttu-id="04349-107">`LoggerMessage` poskytuje následující výhody výkonu prostřednictvím metody rozšíření protokolování:</span><span class="sxs-lookup"><span data-stu-id="04349-107">`LoggerMessage` provides the following performance advantages over Logger extension methods:</span></span>

* <span data-ttu-id="04349-108">Metody rozšíření protokolování vyžadují "zabalení" (převod) typy hodnot, jako například `int`, do `object`.</span><span class="sxs-lookup"><span data-stu-id="04349-108">Logger extension methods require "boxing" (converting) value types, such as `int`, into `object`.</span></span> <span data-ttu-id="04349-109">`LoggerMessage` Vzor se vyhnete zabalení pomocí statické `Action` pole a metody rozšíření se silnými typy parametrů.</span><span class="sxs-lookup"><span data-stu-id="04349-109">The `LoggerMessage` pattern avoids boxing by using static `Action` fields and extension methods with strongly-typed parameters.</span></span>
* <span data-ttu-id="04349-110">Metody rozšíření protokolování musí parsovat šablonu zprávy (pojmenované formátovací řetězec) pokaždé, když je zapsat zprávu protokolu.</span><span class="sxs-lookup"><span data-stu-id="04349-110">Logger extension methods must parse the message template (named format string) every time a log message is written.</span></span> <span data-ttu-id="04349-111">`LoggerMessage` vyžaduje pouze pokud zpráva je definován jednou analýze šablony.</span><span class="sxs-lookup"><span data-stu-id="04349-111">`LoggerMessage` only requires parsing a template once when the message is defined.</span></span>

<span data-ttu-id="04349-112">[Zobrazení nebo stažení ukázkového kódu](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/loggermessage/sample/) ([stažení](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="04349-112">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/loggermessage/sample/) ([how to download](xref:index#how-to-download-a-sample))</span></span>

<span data-ttu-id="04349-113">Ukázková aplikace předvádí `LoggerMessage` funkce s nabídkou Základní sledování systému.</span><span class="sxs-lookup"><span data-stu-id="04349-113">The sample app demonstrates `LoggerMessage` features with a basic quote tracking system.</span></span> <span data-ttu-id="04349-114">Aplikace přidá a odstraní uvozovky použití databáze v paměti.</span><span class="sxs-lookup"><span data-stu-id="04349-114">The app adds and deletes quotes using an in-memory database.</span></span> <span data-ttu-id="04349-115">Tyto operace jsou prováděny, zprávy protokolu jsou generovány pomocí `LoggerMessage` vzor.</span><span class="sxs-lookup"><span data-stu-id="04349-115">As these operations occur, log messages are generated using the `LoggerMessage` pattern.</span></span>

## <a name="loggermessagedefine"></a><span data-ttu-id="04349-116">LoggerMessage.Define</span><span class="sxs-lookup"><span data-stu-id="04349-116">LoggerMessage.Define</span></span>

<span data-ttu-id="04349-117">[Definování (LogLevel, ID události, řetězce)](/dotnet/api/microsoft.extensions.logging.loggermessage.define) vytvoří `Action` delegování pro protokolování zprávy.</span><span class="sxs-lookup"><span data-stu-id="04349-117">[Define(LogLevel, EventId, String)](/dotnet/api/microsoft.extensions.logging.loggermessage.define) creates an `Action` delegate for logging a message.</span></span> <span data-ttu-id="04349-118">`Define` přetížení povolit předávání až šest parametry typu řetězec s názvem formátu (šablona).</span><span class="sxs-lookup"><span data-stu-id="04349-118">`Define` overloads permit passing up to six type parameters to a named format string (template).</span></span>

<span data-ttu-id="04349-119">Řetězec k dispozici na `Define` metoda je šablony a ne interpolovaného řetězce.</span><span class="sxs-lookup"><span data-stu-id="04349-119">The string provided to the `Define` method is a template and not an interpolated string.</span></span> <span data-ttu-id="04349-120">Zástupné symboly jsou vyplněny v pořadí, že jsou uvedeny typy.</span><span class="sxs-lookup"><span data-stu-id="04349-120">Placeholders are filled in the order that the types are specified.</span></span> <span data-ttu-id="04349-121">Zástupné názvy v šabloně by měl být popisný a konzistentní vzhledem k aplikacím v rámci šablony.</span><span class="sxs-lookup"><span data-stu-id="04349-121">Placeholder names in the template should be descriptive and consistent across templates.</span></span> <span data-ttu-id="04349-122">Slouží jako názvy vlastností v rámci strukturovaná data protokolu.</span><span class="sxs-lookup"><span data-stu-id="04349-122">They serve as property names within structured log data.</span></span> <span data-ttu-id="04349-123">Doporučujeme [Pascal malých a velkých písmen](/dotnet/standard/design-guidelines/capitalization-conventions) pro zástupné názvy.</span><span class="sxs-lookup"><span data-stu-id="04349-123">We recommend [Pascal casing](/dotnet/standard/design-guidelines/capitalization-conventions) for placeholder names.</span></span> <span data-ttu-id="04349-124">Například `{Count}`, `{FirstName}`.</span><span class="sxs-lookup"><span data-stu-id="04349-124">For example, `{Count}`, `{FirstName}`.</span></span>

<span data-ttu-id="04349-125">Jednotlivé zprávy protokolu `Action` uchovávat v datovém typu statické pole vytvořeného touto `LoggerMessage.Define`.</span><span class="sxs-lookup"><span data-stu-id="04349-125">Each log message is an `Action` held in a static field created by `LoggerMessage.Define`.</span></span> <span data-ttu-id="04349-126">Například ukázkové aplikace vytvoří pole pro popis zprávy protokolu pro požadavek GET na indexovou stránku (*Internal/LoggerExtensions.cs*):</span><span class="sxs-lookup"><span data-stu-id="04349-126">For example, the sample app creates a field to describe a log message for a GET request for the Index page (*Internal/LoggerExtensions.cs*):</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet1)]

<span data-ttu-id="04349-127">Pro `Action`, zadejte:</span><span class="sxs-lookup"><span data-stu-id="04349-127">For the `Action`, specify:</span></span>

* <span data-ttu-id="04349-128">Úroveň protokolování</span><span class="sxs-lookup"><span data-stu-id="04349-128">The log level.</span></span>
* <span data-ttu-id="04349-129">Události jedinečný identifikátor ([EventId](/dotnet/api/microsoft.extensions.logging.eventid)) s názvem metody statické rozšíření.</span><span class="sxs-lookup"><span data-stu-id="04349-129">A unique event identifier ([EventId](/dotnet/api/microsoft.extensions.logging.eventid)) with the name of the static extension method.</span></span>
* <span data-ttu-id="04349-130">Šablona zprávy (s názvem formátovací řetězec).</span><span class="sxs-lookup"><span data-stu-id="04349-130">The message template (named format string).</span></span> 

<span data-ttu-id="04349-131">Žádost o indexovou stránku ukázkových aplikací sad:</span><span class="sxs-lookup"><span data-stu-id="04349-131">A request for the Index page of the sample app sets the:</span></span>

* <span data-ttu-id="04349-132">Úroveň protokolování `Information`.</span><span class="sxs-lookup"><span data-stu-id="04349-132">Log level to `Information`.</span></span>
* <span data-ttu-id="04349-133">Id události k `1` názvem `IndexPageRequested` metody.</span><span class="sxs-lookup"><span data-stu-id="04349-133">Event id to `1` with the name of the `IndexPageRequested` method.</span></span>
* <span data-ttu-id="04349-134">Šablona zprávy (s názvem formátovací řetězec) na řetězec.</span><span class="sxs-lookup"><span data-stu-id="04349-134">Message template (named format string) to a string.</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet5)]

<span data-ttu-id="04349-135">Strukturované protokolování úložiště použít název události při se dodává s id události rozšiřuje protokolování.</span><span class="sxs-lookup"><span data-stu-id="04349-135">Structured logging stores may use the event name when it's supplied with the event id to enrich logging.</span></span> <span data-ttu-id="04349-136">Například [Serilog](https://github.com/serilog/serilog-extensions-logging) používá název události.</span><span class="sxs-lookup"><span data-stu-id="04349-136">For example, [Serilog](https://github.com/serilog/serilog-extensions-logging) uses the event name.</span></span>

<span data-ttu-id="04349-137">`Action` Vyvolat prostřednictvím metody rozšíření silného typu.</span><span class="sxs-lookup"><span data-stu-id="04349-137">The `Action` is invoked through a strongly-typed extension method.</span></span> <span data-ttu-id="04349-138">`IndexPageRequested` Metoda zaznamená zprávu pro požadavek GET Index stránky v ukázkové aplikaci:</span><span class="sxs-lookup"><span data-stu-id="04349-138">The `IndexPageRequested` method logs a message for an Index page GET request in the sample app:</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet9)]

<span data-ttu-id="04349-139">`IndexPageRequested` je volána v protokolovací nástroj v `OnGetAsync` metoda *Pages/Index.cshtml.cs*:</span><span class="sxs-lookup"><span data-stu-id="04349-139">`IndexPageRequested` is called on the logger in the `OnGetAsync` method in *Pages/Index.cshtml.cs*:</span></span>

[!code-csharp[](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=3)]

<span data-ttu-id="04349-140">Zkontrolujte výstup na konzole aplikace:</span><span class="sxs-lookup"><span data-stu-id="04349-140">Inspect the app's console output:</span></span>

```console
info: LoggerMessageSample.Pages.IndexModel[1]
      => RequestId:0HL90M6E7PHK4:00000001 RequestPath:/ => /Index
      GET request for Index page
```

<span data-ttu-id="04349-141">Pro předání parametrů do zprávy protokolu, definujte až šest typů, při vytváření statické pole.</span><span class="sxs-lookup"><span data-stu-id="04349-141">To pass parameters to a log message, define up to six types when creating the static field.</span></span> <span data-ttu-id="04349-142">Ukázková aplikace zaznamenává řetězec při přidávání nabídky definováním `string` zadejte `Action` pole:</span><span class="sxs-lookup"><span data-stu-id="04349-142">The sample app logs a string when adding a quote by defining a `string` type for the `Action` field:</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet2)]

<span data-ttu-id="04349-143">Šablona zprávy protokolu delegáta přijímá jeho zástupné hodnoty z typů, které jsou k dispozici.</span><span class="sxs-lookup"><span data-stu-id="04349-143">The delegate's log message template receives its placeholder values from the types provided.</span></span> <span data-ttu-id="04349-144">Ukázková aplikace definuje delegáta pro přidání poptávku, kde parametr nabídky `string`:</span><span class="sxs-lookup"><span data-stu-id="04349-144">The sample app defines a delegate for adding a quote where the quote parameter is a `string`:</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet6)]

<span data-ttu-id="04349-145">Statické rozšíření metoda pro přidání nabídky `QuoteAdded`, přijímá nabídku hodnotu argumentu a předává jej do `Action` delegáta:</span><span class="sxs-lookup"><span data-stu-id="04349-145">The static extension method for adding a quote, `QuoteAdded`, receives the quote argument value and passes it to the `Action` delegate:</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet10)]

<span data-ttu-id="04349-146">V modelu stránky indexovou stránku (*Pages/Index.cshtml.cs*), `QuoteAdded` je volána k protokolování zprávy:</span><span class="sxs-lookup"><span data-stu-id="04349-146">In the Index page's page model (*Pages/Index.cshtml.cs*), `QuoteAdded` is called to log the message:</span></span>

[!code-csharp[](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet3&highlight=6)]

<span data-ttu-id="04349-147">Zkontrolujte výstup na konzole aplikace:</span><span class="sxs-lookup"><span data-stu-id="04349-147">Inspect the app's console output:</span></span>

```console
info: LoggerMessageSample.Pages.IndexModel[2]
      => RequestId:0HL90M6E7PHK5:0000000A RequestPath:/ => /Index
      Quote added (Quote = 'You can avoid reality, but you cannot avoid the consequences of avoiding reality. - Ayn Rand')
```

<span data-ttu-id="04349-148">Implementuje ukázkové aplikace `try` &ndash; `catch` vzor pro odstranění nabídky.</span><span class="sxs-lookup"><span data-stu-id="04349-148">The sample app implements a `try`&ndash;`catch` pattern for quote deletion.</span></span> <span data-ttu-id="04349-149">Informační zpráva je zaprotokolována pro úspěšné operaci.</span><span class="sxs-lookup"><span data-stu-id="04349-149">An informational message is logged for a successful delete operation.</span></span> <span data-ttu-id="04349-150">Operace odstranění je zaznamenána chybová zpráva, když dojde k výjimce.</span><span class="sxs-lookup"><span data-stu-id="04349-150">An error message is logged for a delete operation when an exception is thrown.</span></span> <span data-ttu-id="04349-151">Zpráva protokolu pro neúspěšné operace odstranění obsahuje trasování zásobníku výjimek (*Internal/LoggerExtensions.cs*):</span><span class="sxs-lookup"><span data-stu-id="04349-151">The log message for the unsuccessful delete operation includes the exception stack trace (*Internal/LoggerExtensions.cs*):</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet3)]

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet7)]

<span data-ttu-id="04349-152">Všimněte si, jak je výjimka předaný delegátovi v `QuoteDeleteFailed`:</span><span class="sxs-lookup"><span data-stu-id="04349-152">Note how the exception is passed to the delegate in `QuoteDeleteFailed`:</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet11)]

<span data-ttu-id="04349-153">V modelu stránky pro indexovou stránku odstranění úspěšné nabídky volá `QuoteDeleted` metodu na protokolovacího nástroje.</span><span class="sxs-lookup"><span data-stu-id="04349-153">In the page model for the Index page, a successful quote deletion calls the `QuoteDeleted` method on the logger.</span></span> <span data-ttu-id="04349-154">Pokud není nalezen nabídky pro odstranění, `ArgumentNullException` je vyvolána výjimka.</span><span class="sxs-lookup"><span data-stu-id="04349-154">When a quote isn't found for deletion, an `ArgumentNullException` is thrown.</span></span> <span data-ttu-id="04349-155">Výjimka je zachycena ve `try` &ndash; `catch` příkazu nebude úspěšné a voláním `QuoteDeleteFailed` metodu na protokolovací nástroj v `catch` blok (*Pages/Index.cshtml.cs*):</span><span class="sxs-lookup"><span data-stu-id="04349-155">The exception is trapped by the `try`&ndash;`catch` statement and logged by calling the `QuoteDeleteFailed` method on the logger in the `catch` block (*Pages/Index.cshtml.cs*):</span></span>

[!code-csharp[](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet5&highlight=14,18)]

<span data-ttu-id="04349-156">Pokud je nabídka byla úspěšně odstraněna, zkontrolujte výstup na konzole aplikace:</span><span class="sxs-lookup"><span data-stu-id="04349-156">When a quote is successfully deleted, inspect the app's console output:</span></span>

```console
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:00000016 RequestPath:/ => /Index
      Quote deleted (Quote = 'You can avoid reality, but you cannot avoid the consequences of avoiding reality. - Ayn Rand' Id = 1)
```

<span data-ttu-id="04349-157">Při odstranění nabídky nezdaří, zkontrolujte, zda výstup na konzole aplikace.</span><span class="sxs-lookup"><span data-stu-id="04349-157">When quote deletion fails, inspect the app's console output.</span></span> <span data-ttu-id="04349-158">Všimněte si, že výjimka je součástí zprávy protokolu:</span><span class="sxs-lookup"><span data-stu-id="04349-158">Note that the exception is included in the log message:</span></span>

```console
fail: LoggerMessageSample.Pages.IndexModel[5]
      => RequestId:0HL90M6E7PHK5:00000010 RequestPath:/ => /Index
      Quote delete failed (Id = 999)
System.ArgumentNullException: Value cannot be null.
Parameter name: entity
   at Microsoft.EntityFrameworkCore.Utilities.Check.NotNull[T](T value, String parameterName)
   at Microsoft.EntityFrameworkCore.DbContext.Remove[TEntity](TEntity entity)
   at Microsoft.EntityFrameworkCore.Internal.InternalDbSet`1.Remove(TEntity entity)
   at LoggerMessageSample.Pages.IndexModel.<OnPostDeleteQuoteAsync>d__14.MoveNext() in 
      <PATH>\sample\Pages\Index.cshtml.cs:line 87
```

## <a name="loggermessagedefinescope"></a><span data-ttu-id="04349-159">LoggerMessage.DefineScope</span><span class="sxs-lookup"><span data-stu-id="04349-159">LoggerMessage.DefineScope</span></span>

<span data-ttu-id="04349-160">[DefineScope(String)](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope) vytvoří `Func` delegování pro definování [protokolu oboru](xref:fundamentals/logging/index#log-scopes).</span><span class="sxs-lookup"><span data-stu-id="04349-160">[DefineScope(String)](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope) creates a `Func` delegate for defining a [log scope](xref:fundamentals/logging/index#log-scopes).</span></span> <span data-ttu-id="04349-161">`DefineScope` přetížení povolit předávání až tři parametry typu řetězec s názvem formátu (šablona).</span><span class="sxs-lookup"><span data-stu-id="04349-161">`DefineScope` overloads permit passing up to three type parameters to a named format string (template).</span></span>

<span data-ttu-id="04349-162">Stejně jako v případě s `Define` metoda, řetězec k dispozici na `DefineScope` metoda je šablony a ne interpolovaného řetězce.</span><span class="sxs-lookup"><span data-stu-id="04349-162">As is the case with the `Define` method, the string provided to the `DefineScope` method is a template and not an interpolated string.</span></span> <span data-ttu-id="04349-163">Zástupné symboly jsou vyplněny v pořadí, že jsou uvedeny typy.</span><span class="sxs-lookup"><span data-stu-id="04349-163">Placeholders are filled in the order that the types are specified.</span></span> <span data-ttu-id="04349-164">Zástupné názvy v šabloně by měl být popisný a konzistentní vzhledem k aplikacím v rámci šablony.</span><span class="sxs-lookup"><span data-stu-id="04349-164">Placeholder names in the template should be descriptive and consistent across templates.</span></span> <span data-ttu-id="04349-165">Slouží jako názvy vlastností v rámci strukturovaná data protokolu.</span><span class="sxs-lookup"><span data-stu-id="04349-165">They serve as property names within structured log data.</span></span> <span data-ttu-id="04349-166">Doporučujeme [Pascal malých a velkých písmen](/dotnet/standard/design-guidelines/capitalization-conventions) pro zástupné názvy.</span><span class="sxs-lookup"><span data-stu-id="04349-166">We recommend [Pascal casing](/dotnet/standard/design-guidelines/capitalization-conventions) for placeholder names.</span></span> <span data-ttu-id="04349-167">Například `{Count}`, `{FirstName}`.</span><span class="sxs-lookup"><span data-stu-id="04349-167">For example, `{Count}`, `{FirstName}`.</span></span>

<span data-ttu-id="04349-168">Definovat [protokolu oboru](xref:fundamentals/logging/index#log-scopes) použít řadu zpráv protokolu pomocí [DefineScope(String)](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope) metoda.</span><span class="sxs-lookup"><span data-stu-id="04349-168">Define a [log scope](xref:fundamentals/logging/index#log-scopes) to apply to a series of log messages using the [DefineScope(String)](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope) method.</span></span>

<span data-ttu-id="04349-169">Ukázková aplikace má **Vymazat vše** tlačítko pro odstranění všech nabídek v databázi.</span><span class="sxs-lookup"><span data-stu-id="04349-169">The sample app has a **Clear All** button for deleting all of the quotes in the database.</span></span> <span data-ttu-id="04349-170">Uvozovky budou odstraněny tak, že odeberete jeden po druhém.</span><span class="sxs-lookup"><span data-stu-id="04349-170">The quotes are deleted by removing them one at a time.</span></span> <span data-ttu-id="04349-171">Pokaždé, když se odstraní uvozovky, `QuoteDeleted` metoda je volána na protokolovacího nástroje.</span><span class="sxs-lookup"><span data-stu-id="04349-171">Each time a quote is deleted, the `QuoteDeleted` method is called on the logger.</span></span> <span data-ttu-id="04349-172">Rozsah protokolu je přidán do těchto zpráv protokolu.</span><span class="sxs-lookup"><span data-stu-id="04349-172">A log scope is added to these log messages.</span></span>

<span data-ttu-id="04349-173">Povolit `IncludeScopes` v části protokolovací nástroj konzoly *appsettings.json*:</span><span class="sxs-lookup"><span data-stu-id="04349-173">Enable `IncludeScopes` in the console logger section of *appsettings.json*:</span></span>

[!code-csharp[](loggermessage/sample/appsettings.json?highlight=3-5)]

<span data-ttu-id="04349-174">Vytvoření oboru protokolu, přidáte pole pro uložení `Func` delegování pro obor.</span><span class="sxs-lookup"><span data-stu-id="04349-174">To create a log scope, add a field to hold a `Func` delegate for the scope.</span></span> <span data-ttu-id="04349-175">Ukázková aplikace vytvoří pole s názvem `_allQuotesDeletedScope` (*Internal/LoggerExtensions.cs*):</span><span class="sxs-lookup"><span data-stu-id="04349-175">The sample app creates a field called `_allQuotesDeletedScope` (*Internal/LoggerExtensions.cs*):</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet4)]

<span data-ttu-id="04349-176">Použití `DefineScope` k vytvoření delegáta.</span><span class="sxs-lookup"><span data-stu-id="04349-176">Use `DefineScope` to create the delegate.</span></span> <span data-ttu-id="04349-177">Až tři typy lze používat jako argumenty šablony při vyvolání delegáta.</span><span class="sxs-lookup"><span data-stu-id="04349-177">Up to three types can be specified for use as template arguments when the delegate is invoked.</span></span> <span data-ttu-id="04349-178">Ukázková aplikace používá šablonu zprávy, která obsahuje počet odstraněných nabídky ( `int` typ):</span><span class="sxs-lookup"><span data-stu-id="04349-178">The sample app uses a message template that includes the number of deleted quotes (an `int` type):</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet8)]

<span data-ttu-id="04349-179">Poskytuje metodu statické rozšíření pro zprávy protokolu.</span><span class="sxs-lookup"><span data-stu-id="04349-179">Provide a static extension method for the log message.</span></span> <span data-ttu-id="04349-180">Zahrňte všechny parametry typu pro pojmenované vlastnosti, které se zobrazují v šablonu zprávy.</span><span class="sxs-lookup"><span data-stu-id="04349-180">Include any type parameters for named properties that appear in the message template.</span></span> <span data-ttu-id="04349-181">Ukázková aplikace přijímá `count` uvozovkami, aby byly odstranit a vrátí `_allQuotesDeletedScope`:</span><span class="sxs-lookup"><span data-stu-id="04349-181">The sample app takes in a `count` of quotes to delete and returns `_allQuotesDeletedScope`:</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet12)]

<span data-ttu-id="04349-182">Obor zabalí volání rozšíření protokolování `using` blok:</span><span class="sxs-lookup"><span data-stu-id="04349-182">The scope wraps the logging extension calls in a `using` block:</span></span>

[!code-csharp[](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet4&highlight=5-6,14)]

<span data-ttu-id="04349-183">Kontrola protokolu zpráv ve výstupu konzoly aplikace.</span><span class="sxs-lookup"><span data-stu-id="04349-183">Inspect the log messages in the app's console output.</span></span> <span data-ttu-id="04349-184">Následující výsledek ukazuje tři uvozovky odstranit obor zprávou protokolu zahrnout:</span><span class="sxs-lookup"><span data-stu-id="04349-184">The following result shows three quotes deleted with the log scope message included:</span></span>

```console
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:0000002E RequestPath:/ => /Index => All quotes deleted (Count = 3)
      Quote deleted (Quote = 'Quote 1' Id = 2)
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:0000002E RequestPath:/ => /Index => All quotes deleted (Count = 3)
      Quote deleted (Quote = 'Quote 2' Id = 3)
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:0000002E RequestPath:/ => /Index => All quotes deleted (Count = 3)
      Quote deleted (Quote = 'Quote 3' Id = 4)
```

## <a name="additional-resources"></a><span data-ttu-id="04349-185">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="04349-185">Additional resources</span></span>

* [<span data-ttu-id="04349-186">Protokolování</span><span class="sxs-lookup"><span data-stu-id="04349-186">Logging</span></span>](xref:fundamentals/logging/index)
