---
uid: config-builder
title: Konfigurace počítačů pro technologii ASP.NET
author: rick-anderson
description: Další informace o získání konfigurační data ze zdrojů než hodnoty web.config z externích zdrojů.
ms.author: riande
ms.date: 10/29/2018
ms.technology: aspnet
msc.type: content
ms.openlocfilehash: 443b33b5c3b964f731999834db580a6abbf6617b
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59420416"
---
# <a name="configuration-builders-for-aspnet"></a><span data-ttu-id="b4e90-103">Konfigurace počítačů pro technologii ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b4e90-103">Configuration builders for ASP.NET</span></span>

<span data-ttu-id="b4e90-104">Podle [Stephen Molloy](https://github.com/StephenMolloy) a [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="b4e90-104">By [Stephen Molloy](https://github.com/StephenMolloy) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="b4e90-105">Konfigurace počítačů poskytují moderní a agilní mechanismus pro aplikace v ASP.NET k získání hodnoty konfigurace z externích zdrojů.</span><span class="sxs-lookup"><span data-stu-id="b4e90-105">Configuration builders provide a modern and agile mechanism for ASP.NET apps to get configuration values from external sources.</span></span>

<span data-ttu-id="b4e90-106">Konfigurace počítačů:</span><span class="sxs-lookup"><span data-stu-id="b4e90-106">Configuration builders:</span></span>

* <span data-ttu-id="b4e90-107">Jsou k dispozici v rozhraní .NET Framework 4.7.1 a novějším.</span><span class="sxs-lookup"><span data-stu-id="b4e90-107">Are available in .NET Framework 4.7.1 and later.</span></span>
* <span data-ttu-id="b4e90-108">Nabízejí flexibilní mechanismus pro čtení konfigurační hodnoty.</span><span class="sxs-lookup"><span data-stu-id="b4e90-108">Provide a flexible mechanism for reading configuration values.</span></span>
* <span data-ttu-id="b4e90-109">Řešení některých základních potřeb aplikace tak, jak přesunout do kontejneru a fokusem prostředí v cloudu.</span><span class="sxs-lookup"><span data-stu-id="b4e90-109">Address some of the basic needs of apps as they move into a container and cloud focused environment.</span></span>
* <span data-ttu-id="b4e90-110">Můžete použít ke zlepšení ochrany konfigurační data kreslením z dříve k dispozici zdrojů (například Azure Key Vault a proměnnými prostředí) v konfigurační systém .NET.</span><span class="sxs-lookup"><span data-stu-id="b4e90-110">Can be used to improve protection of configuration data by drawing from sources previously unavailable (for example, Azure Key Vault and environment variables) in the .NET configuration system.</span></span>

## <a name="keyvalue-configuration-builders"></a><span data-ttu-id="b4e90-111">Tvůrci konfigurace klíč hodnota</span><span class="sxs-lookup"><span data-stu-id="b4e90-111">Key/value configuration builders</span></span>

<span data-ttu-id="b4e90-112">Běžný scénář, který může být zpracována tvůrci konfigurace je mechanismus nahrazení základní klíč/hodnota pro konfigurační oddíly funkce, které se řídí vzorem klíč/hodnota.</span><span class="sxs-lookup"><span data-stu-id="b4e90-112">A common scenario that can be handled by configuration builders is to provide a basic key/value replacement mechanism for configuration sections that follow a key/value pattern.</span></span> <span data-ttu-id="b4e90-113">Rozhraní .NET Framework konceptu ConfigurationBuilders není omezena pouze na konkrétní konfigurační oddíly funkce nebo vzorce.</span><span class="sxs-lookup"><span data-stu-id="b4e90-113">The .NET Framework concept of ConfigurationBuilders is not limited to specific configuration sections or patterns.</span></span> <span data-ttu-id="b4e90-114">Nicméně mnoho tvůrci konfigurace v `Microsoft.Configuration.ConfigurationBuilders` ([githubu](https://github.com/aspnet/MicrosoftConfigurationBuilders), [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)) práce v rámci vzoru klíč/hodnota.</span><span class="sxs-lookup"><span data-stu-id="b4e90-114">However, many of the configuration builders in `Microsoft.Configuration.ConfigurationBuilders` ([github](https://github.com/aspnet/MicrosoftConfigurationBuilders), [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)) work within the key/value pattern.</span></span>

## <a name="keyvalue-configuration-builders-settings"></a><span data-ttu-id="b4e90-115">Nastavení tvůrci konfigurace klíč hodnota</span><span class="sxs-lookup"><span data-stu-id="b4e90-115">Key/value configuration builders settings</span></span>

<span data-ttu-id="b4e90-116">Následující nastavení se vztahuje na všechny konfigurace Tvůrce klíč/hodnota v `Microsoft.Configuration.ConfigurationBuilders`.</span><span class="sxs-lookup"><span data-stu-id="b4e90-116">The following settings apply to all key/value configuration builders in `Microsoft.Configuration.ConfigurationBuilders`.</span></span>

### <a name="mode"></a><span data-ttu-id="b4e90-117">Režim</span><span class="sxs-lookup"><span data-stu-id="b4e90-117">Mode</span></span>

<span data-ttu-id="b4e90-118">Tvůrci konfiguraci pomocí externího zdroje informací klíč/hodnota k naplnění vybraný klíč/hodnota prvků konfigurace systému.</span><span class="sxs-lookup"><span data-stu-id="b4e90-118">The configuration builders use an external source of key/value information to populate selected key/value elements of the configuration system.</span></span> <span data-ttu-id="b4e90-119">Konkrétně `<appSettings/>` a `<connectionStrings/>` oddíly přijímat zvláštní zacházení z konfigurace počítačů.</span><span class="sxs-lookup"><span data-stu-id="b4e90-119">Specifically, the `<appSettings/>` and `<connectionStrings/>` sections receive special treatment from the configuration builders.</span></span> <span data-ttu-id="b4e90-120">Tvůrci pracovat v tří režimů:</span><span class="sxs-lookup"><span data-stu-id="b4e90-120">The builders work in three modes:</span></span>

* `Strict` <span data-ttu-id="b4e90-121">– Výchozí režim.</span><span class="sxs-lookup"><span data-stu-id="b4e90-121">- The default mode.</span></span> <span data-ttu-id="b4e90-122">V tomto režimu konfigurace Tvůrce pracuje pouze se dobře známé klíč/hodnota-zaměřenou na konfigurační oddíly funkce.</span><span class="sxs-lookup"><span data-stu-id="b4e90-122">In this mode, the configuration builder only operates on well-known key/value-centric configuration sections.</span></span> `Strict` <span data-ttu-id="b4e90-123">Režim zobrazí každý klíč v části.</span><span class="sxs-lookup"><span data-stu-id="b4e90-123">mode enumerates each key in the section.</span></span> <span data-ttu-id="b4e90-124">Pokud se najde odpovídající klíče v externím zdroji:</span><span class="sxs-lookup"><span data-stu-id="b4e90-124">If a matching key is found in the external source:</span></span>

   * <span data-ttu-id="b4e90-125">Tvůrci konfigurace nahraďte hodnotu v konfigurační sekci výslednou hodnotu z externího zdroje.</span><span class="sxs-lookup"><span data-stu-id="b4e90-125">The configuration builders replace the value in the resulting configuration section with the value from the external source.</span></span>
* `Greedy` <span data-ttu-id="b4e90-126">– Tento režim je úzce souvisí s `Strict` režimu.</span><span class="sxs-lookup"><span data-stu-id="b4e90-126">- This mode is closely related to `Strict` mode.</span></span> <span data-ttu-id="b4e90-127">Místo omezeno na klíče, které již existují v původní konfiguraci:</span><span class="sxs-lookup"><span data-stu-id="b4e90-127">Rather than being limited to keys that already exist in the original configuration:</span></span>

  * <span data-ttu-id="b4e90-128">Konfigurace počítačů přidá všechny páry klíč/hodnota z externího zdroje do výsledné konfigurační oddíl.</span><span class="sxs-lookup"><span data-stu-id="b4e90-128">The configuration builders adds all key/value pairs from the external source into the resulting configuration section.</span></span>

* `Expand` <span data-ttu-id="b4e90-129">-Funguje v nezpracovaném kódu XML předtím, než je analyzován do konfiguračního oddílu objektu.</span><span class="sxs-lookup"><span data-stu-id="b4e90-129">- Operates on the raw XML before it's parsed into a configuration section object.</span></span> <span data-ttu-id="b4e90-130">To můžete představit jako rozšíření tokenů v řetězci.</span><span class="sxs-lookup"><span data-stu-id="b4e90-130">It can be thought of as an expansion of tokens in a string.</span></span> <span data-ttu-id="b4e90-131">Libovolná součást Nezpracovaný řetězec XML, který odpovídá vzoru `${token}` je kandidát pro rozšíření tokenu.</span><span class="sxs-lookup"><span data-stu-id="b4e90-131">Any part of the raw XML string that matches the pattern `${token}` is a candidate for token expansion.</span></span> <span data-ttu-id="b4e90-132">Pokud není nalezena žádná odpovídající hodnota v externím zdroji, token, který se nemění.</span><span class="sxs-lookup"><span data-stu-id="b4e90-132">If no corresponding value is found in the external source, then the token is not changed.</span></span> <span data-ttu-id="b4e90-133">Tvůrci v tomto režimu nejsou omezeny `<appSettings/>` a `<connectionStrings/>` oddíly.</span><span class="sxs-lookup"><span data-stu-id="b4e90-133">Builders in this mode are not limited to the `<appSettings/>` and `<connectionStrings/>` sections.</span></span>

<span data-ttu-id="b4e90-134">Následující kód z *web.config* umožňuje [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) v `Strict` režimu:</span><span class="sxs-lookup"><span data-stu-id="b4e90-134">The following markup from *web.config* enables the [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) in `Strict` mode:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebDefault.config?name=snippet)]

<span data-ttu-id="b4e90-135">Následující kód čtení `<appSettings/>` a `<connectionStrings/>` je znázorněno v předchozím *web.config* souboru:</span><span class="sxs-lookup"><span data-stu-id="b4e90-135">The following code reads the `<appSettings/>` and `<connectionStrings/>` shown in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/About.aspx.cs)]

<span data-ttu-id="b4e90-136">Předchozí kód nastaví hodnoty vlastností:</span><span class="sxs-lookup"><span data-stu-id="b4e90-136">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="b4e90-137">Hodnoty *web.config* souboru, pokud nejsou nastavené klíče v seznamu proměnných prostředí.</span><span class="sxs-lookup"><span data-stu-id="b4e90-137">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="b4e90-138">Hodnoty prostředí proměnné, když nastavení.</span><span class="sxs-lookup"><span data-stu-id="b4e90-138">The values of the environment variable, if set.</span></span>

<span data-ttu-id="b4e90-139">Například `ServiceID` bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="b4e90-139">For example, `ServiceID` will contain:</span></span>

* <span data-ttu-id="b4e90-140">"ServiceID hodnotu ze souboru web.config", pokud je proměnná prostředí `ServiceID` není nastaven.</span><span class="sxs-lookup"><span data-stu-id="b4e90-140">"ServiceID value from web.config", if the environment variable `ServiceID` is not set.</span></span>
* <span data-ttu-id="b4e90-141">Hodnota `ServiceID` prostředí proměnné, když nastavení.</span><span class="sxs-lookup"><span data-stu-id="b4e90-141">The value of the `ServiceID` environment variable, if set.</span></span>

<span data-ttu-id="b4e90-142">Na následujícím obrázku `<appSettings/>` klíče/hodnoty z předchozího *web.config* souboru sadu v editoru prostředí:</span><span class="sxs-lookup"><span data-stu-id="b4e90-142">The following image shows the `<appSettings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![editor prostředí](config-builder/static/env.png)

<span data-ttu-id="b4e90-144">Poznámka: Můžete potřebovat ukončit a restartovat Visual Studio pro zobrazení změn v proměnných prostředí.</span><span class="sxs-lookup"><span data-stu-id="b4e90-144">Note: You might need to exit and restart Visual Studio to see changes in environment variables.</span></span>

### <a name="prefix-handling"></a><span data-ttu-id="b4e90-145">Předpona zpracování</span><span class="sxs-lookup"><span data-stu-id="b4e90-145">Prefix handling</span></span>

<span data-ttu-id="b4e90-146">Předpony klíčů můžete zjednodušit nastavení klíče, protože:</span><span class="sxs-lookup"><span data-stu-id="b4e90-146">Key prefixes can simplify setting keys because:</span></span>

* <span data-ttu-id="b4e90-147">Konfigurace rozhraní .NET Framework je složitá a vnořené.</span><span class="sxs-lookup"><span data-stu-id="b4e90-147">The .NET Framework configuration is complex and nested.</span></span>
* <span data-ttu-id="b4e90-148">Externí klíč/hodnota zdroje jsou často na úrovni basic a bez stromové struktury podle povahy.</span><span class="sxs-lookup"><span data-stu-id="b4e90-148">External key/value sources are commonly basic and flat by nature.</span></span> <span data-ttu-id="b4e90-149">Například nejsou vnořené proměnné prostředí.</span><span class="sxs-lookup"><span data-stu-id="b4e90-149">For example, environment variables are not nested.</span></span>

<span data-ttu-id="b4e90-150">Použít některou z následujících dvou přístupů vkládat obě `<appSettings/>` a `<connectionStrings/>` do konfigurace prostřednictvím proměnné prostředí:</span><span class="sxs-lookup"><span data-stu-id="b4e90-150">Use any of the following approaches to inject both `<appSettings/>` and `<connectionStrings/>` into the configuration via environment variables:</span></span>

* <span data-ttu-id="b4e90-151">S `EnvironmentConfigBuilder` ve výchozím `Strict` režimu a odpovídající názvy klíčů v konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="b4e90-151">With the `EnvironmentConfigBuilder` in the default `Strict` mode and the appropriate key names in the configuration file.</span></span> <span data-ttu-id="b4e90-152">Předchozí kód a kód používá tento přístup.</span><span class="sxs-lookup"><span data-stu-id="b4e90-152">The preceding code and markup takes this approach.</span></span> <span data-ttu-id="b4e90-153">Tento přístup můžete **není** stejně jako s názvem klíče v obou `<appSettings/>` a `<connectionStrings/>`.</span><span class="sxs-lookup"><span data-stu-id="b4e90-153">Using this approach you can **not** have identically named keys in both `<appSettings/>` and `<connectionStrings/>`.</span></span>
* <span data-ttu-id="b4e90-154">Použijte dva `EnvironmentConfigBuilder`ve `Greedy` režimu s odlišné předpony a `stripPrefix`.</span><span class="sxs-lookup"><span data-stu-id="b4e90-154">Use two `EnvironmentConfigBuilder`s in `Greedy` mode with distinct prefixes and `stripPrefix`.</span></span> <span data-ttu-id="b4e90-155">Díky tomuto přístupu může číst aplikace `<appSettings/>` a `<connectionStrings/>` bez nutnosti aktualizovat konfigurační soubor.</span><span class="sxs-lookup"><span data-stu-id="b4e90-155">With this approach, the app can read `<appSettings/>` and `<connectionStrings/>` without needing to update the configuration file.</span></span> <span data-ttu-id="b4e90-156">Další části [stripPrefix](#stripprefix), ukazuje, jak to provést.</span><span class="sxs-lookup"><span data-stu-id="b4e90-156">The next section,  [stripPrefix](#stripprefix),  shows how to do this.</span></span>
* <span data-ttu-id="b4e90-157">Použijte dva `EnvironmentConfigBuilder`ve `Greedy` režimu s odlišné předpony.</span><span class="sxs-lookup"><span data-stu-id="b4e90-157">Use two `EnvironmentConfigBuilder`s in `Greedy` mode with distinct prefixes.</span></span> <span data-ttu-id="b4e90-158">Díky tomuto přístupu nemůže mít duplicitní názvy klíčů jako názvy klíčů se musí lišit podle předpony.</span><span class="sxs-lookup"><span data-stu-id="b4e90-158">With this approach you can't have duplicate key names as key names must differ by prefix.</span></span>  <span data-ttu-id="b4e90-159">Příklad:</span><span class="sxs-lookup"><span data-stu-id="b4e90-159">For example:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefix.config?name=snippet&highlight=11-99)]

<span data-ttu-id="b4e90-160">S předchozím kódu je možné zadat konfiguraci pro dvě různé oddíly stejného zdroje bez stromové struktury klíč/hodnota.</span><span class="sxs-lookup"><span data-stu-id="b4e90-160">With the preceding markup, the same flat key/value source can be used to populate configuration for two different sections.</span></span>

<span data-ttu-id="b4e90-161">Na následujícím obrázku `<appSettings/>` a `<connectionStrings/>` klíče/hodnoty z předchozího *web.config* souboru sadu v editoru prostředí:</span><span class="sxs-lookup"><span data-stu-id="b4e90-161">The following image shows the `<appSettings/>` and `<connectionStrings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![editor prostředí](config-builder/static/prefix.png)

<span data-ttu-id="b4e90-163">Následující kód čtení `<appSettings/>` a `<connectionStrings/>` klíče/hodnoty obsažené v předchozím *web.config* souboru:</span><span class="sxs-lookup"><span data-stu-id="b4e90-163">The following code reads the `<appSettings/>` and `<connectionStrings/>` keys/values contained in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/Contact.aspx.cs?name=snippet)]

<span data-ttu-id="b4e90-164">Předchozí kód nastaví hodnoty vlastností:</span><span class="sxs-lookup"><span data-stu-id="b4e90-164">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="b4e90-165">Hodnoty *web.config* souboru, pokud nejsou nastavené klíče v seznamu proměnných prostředí.</span><span class="sxs-lookup"><span data-stu-id="b4e90-165">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="b4e90-166">Hodnoty prostředí proměnné, když nastavení.</span><span class="sxs-lookup"><span data-stu-id="b4e90-166">The values of the environment variable, if set.</span></span>

<span data-ttu-id="b4e90-167">Například použití předchozího *web.config* souboru, jsou nastavené klíče/hodnoty v předchozím obrázku editor prostředí a předchozí kód, následující hodnoty:</span><span class="sxs-lookup"><span data-stu-id="b4e90-167">For example, using the previous *web.config* file, the keys/values in the previous  environment editor image, and the previous code, the following values are set:</span></span>

|  <span data-ttu-id="b4e90-168">Key</span><span class="sxs-lookup"><span data-stu-id="b4e90-168">Key</span></span>              | <span data-ttu-id="b4e90-169">Hodnota</span><span class="sxs-lookup"><span data-stu-id="b4e90-169">Value</span></span> |
| ----------------- | ------------ |
|     <span data-ttu-id="b4e90-170">AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="b4e90-170">AppSetting_ServiceID</span></span>           | <span data-ttu-id="b4e90-171">AppSetting_ServiceID Obálka proměnných</span><span class="sxs-lookup"><span data-stu-id="b4e90-171">AppSetting_ServiceID from env variables</span></span>|
|    <span data-ttu-id="b4e90-172">AppSetting_default</span><span class="sxs-lookup"><span data-stu-id="b4e90-172">AppSetting_default</span></span>            | <span data-ttu-id="b4e90-173">AppSetting_default hodnotu z prostředí</span><span class="sxs-lookup"><span data-stu-id="b4e90-173">AppSetting_default value from env</span></span> |
|       <span data-ttu-id="b4e90-174">ConnStr_default</span><span class="sxs-lookup"><span data-stu-id="b4e90-174">ConnStr_default</span></span>         | <span data-ttu-id="b4e90-175">Val ConnStr_default z env</span><span class="sxs-lookup"><span data-stu-id="b4e90-175">ConnStr_default val from env</span></span>|

### <a name="stripprefix"></a><span data-ttu-id="b4e90-176">stripPrefix</span><span class="sxs-lookup"><span data-stu-id="b4e90-176">stripPrefix</span></span>

`stripPrefix`<span data-ttu-id="b4e90-177">: logickou hodnotu, výchozí hodnota je `false`.</span><span class="sxs-lookup"><span data-stu-id="b4e90-177">: boolean, defaults to `false`.</span></span> 

<span data-ttu-id="b4e90-178">Předchozí kód XML odděluje nastavení aplikace připojovací řetězce, ale vyžaduje všechny klíče v *web.config* souboru pomocí zadané předpony.</span><span class="sxs-lookup"><span data-stu-id="b4e90-178">The preceding XML markup separates app settings from connection strings but requires all the keys in the *web.config* file to use the specified prefix.</span></span> <span data-ttu-id="b4e90-179">Například předponu `AppSetting` musí být přidané do `ServiceID` klíč ("AppSetting_ServiceID").</span><span class="sxs-lookup"><span data-stu-id="b4e90-179">For example, the prefix `AppSetting` must be added to the `ServiceID` key ("AppSetting_ServiceID").</span></span> <span data-ttu-id="b4e90-180">S `stripPrefix`, předpona, která se nepoužívá *web.config* souboru.</span><span class="sxs-lookup"><span data-stu-id="b4e90-180">With `stripPrefix`, the prefix is not used in the *web.config* file.</span></span> <span data-ttu-id="b4e90-181">Předpona, která se vyžaduje Tvůrce zdroj konfigurace (například v prostředí.) Předpokládáme, že se Většina vývojářů používá `stripPrefix`.</span><span class="sxs-lookup"><span data-stu-id="b4e90-181">The prefix is required in the configuration builder source (for example, in the environment.) We anticipate most developers will use `stripPrefix`.</span></span>

<span data-ttu-id="b4e90-182">Aplikace obvykle pruhu vypnout předponu.</span><span class="sxs-lookup"><span data-stu-id="b4e90-182">Applications typically strip off the prefix.</span></span> <span data-ttu-id="b4e90-183">Následující *web.config* odstraní předpona:</span><span class="sxs-lookup"><span data-stu-id="b4e90-183">The following *web.config* strips the prefix:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefixStrip.config?name=snippet&highlight=14,19)]

<span data-ttu-id="b4e90-184">V předchozím *web.config* souboru, `default` klíč je v obou `<appSettings/>` a `<connectionStrings/>`.</span><span class="sxs-lookup"><span data-stu-id="b4e90-184">In the preceding *web.config* file, the `default` key is in both the `<appSettings/>` and `<connectionStrings/>`.</span></span>

<span data-ttu-id="b4e90-185">Na následujícím obrázku `<appSettings/>` a `<connectionStrings/>` klíče/hodnoty z předchozího *web.config* souboru sadu v editoru prostředí:</span><span class="sxs-lookup"><span data-stu-id="b4e90-185">The following image shows the `<appSettings/>` and `<connectionStrings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![editor prostředí](config-builder/static/prefix.png)

<span data-ttu-id="b4e90-187">Následující kód čtení `<appSettings/>` a `<connectionStrings/>` klíče/hodnoty obsažené v předchozím *web.config* souboru:</span><span class="sxs-lookup"><span data-stu-id="b4e90-187">The following code reads the `<appSettings/>` and `<connectionStrings/>` keys/values contained in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/About2.aspx.cs?name=snippet)]

<span data-ttu-id="b4e90-188">Předchozí kód nastaví hodnoty vlastností:</span><span class="sxs-lookup"><span data-stu-id="b4e90-188">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="b4e90-189">Hodnoty *web.config* souboru, pokud nejsou nastavené klíče v seznamu proměnných prostředí.</span><span class="sxs-lookup"><span data-stu-id="b4e90-189">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="b4e90-190">Hodnoty prostředí proměnné, když nastavení.</span><span class="sxs-lookup"><span data-stu-id="b4e90-190">The values of the environment variable, if set.</span></span>

<span data-ttu-id="b4e90-191">Například použití předchozího *web.config* souboru, jsou nastavené klíče/hodnoty v předchozím obrázku editor prostředí a předchozí kód, následující hodnoty:</span><span class="sxs-lookup"><span data-stu-id="b4e90-191">For example, using the previous *web.config* file, the keys/values in the previous  environment editor image, and the previous code, the following values are set:</span></span>

|  <span data-ttu-id="b4e90-192">Key</span><span class="sxs-lookup"><span data-stu-id="b4e90-192">Key</span></span>              | <span data-ttu-id="b4e90-193">Value</span><span class="sxs-lookup"><span data-stu-id="b4e90-193">Value</span></span> |
| ----------------- | ------------ |
|     <span data-ttu-id="b4e90-194">ID služby</span><span class="sxs-lookup"><span data-stu-id="b4e90-194">ServiceID</span></span>           | <span data-ttu-id="b4e90-195">AppSetting_ServiceID Obálka proměnných</span><span class="sxs-lookup"><span data-stu-id="b4e90-195">AppSetting_ServiceID from env variables</span></span>|
|    <span data-ttu-id="b4e90-196">default</span><span class="sxs-lookup"><span data-stu-id="b4e90-196">default</span></span>            | <span data-ttu-id="b4e90-197">AppSetting_default hodnotu z prostředí</span><span class="sxs-lookup"><span data-stu-id="b4e90-197">AppSetting_default value from env</span></span> |
|    <span data-ttu-id="b4e90-198">default</span><span class="sxs-lookup"><span data-stu-id="b4e90-198">default</span></span>         | <span data-ttu-id="b4e90-199">Val ConnStr_default z env</span><span class="sxs-lookup"><span data-stu-id="b4e90-199">ConnStr_default val from env</span></span>|

### <a name="tokenpattern"></a><span data-ttu-id="b4e90-200">tokenPattern</span><span class="sxs-lookup"><span data-stu-id="b4e90-200">tokenPattern</span></span>

`tokenPattern`<span data-ttu-id="b4e90-201">: Řetězec, výchozí hodnota je</span><span class="sxs-lookup"><span data-stu-id="b4e90-201">: String, defaults to</span></span> `@"\$\{(\w+)\}"`

<span data-ttu-id="b4e90-202">`Expand` Chování tvůrci vyhledá nezpracovaném kódu XML pro tokeny, které vypadají jako `${token}`.</span><span class="sxs-lookup"><span data-stu-id="b4e90-202">The `Expand` behavior of the builders searches the raw XML for tokens that look like `${token}`.</span></span> <span data-ttu-id="b4e90-203">Vyhledávání se provádí s regulárním výrazem výchozí `@"\$\{(\w+)\}"`.</span><span class="sxs-lookup"><span data-stu-id="b4e90-203">Searching is done with the default regular expression `@"\$\{(\w+)\}"`.</span></span> <span data-ttu-id="b4e90-204">Množinu znaků, který odpovídá `\w` je přísnější než XML a mnoho zdrojů konfiguraci umožňují.</span><span class="sxs-lookup"><span data-stu-id="b4e90-204">The set of characters that matches `\w` is more strict than XML and many configuration sources allow.</span></span> <span data-ttu-id="b4e90-205">Použití `tokenPattern` při více znaků, než `@"\$\{(\w+)\}"` jsou nezbytné název tokenu.</span><span class="sxs-lookup"><span data-stu-id="b4e90-205">Use `tokenPattern` when more characters than `@"\$\{(\w+)\}"` are required in the token name.</span></span>

`tokenPattern`<span data-ttu-id="b4e90-206">: Řetězec:</span><span class="sxs-lookup"><span data-stu-id="b4e90-206">: String:</span></span>

* <span data-ttu-id="b4e90-207">Umožňuje vývojářům měnit regulární výraz, který se použije k porovnání s tokenu.</span><span class="sxs-lookup"><span data-stu-id="b4e90-207">Allows developers to change the regex that is used for token matching.</span></span>
* <span data-ttu-id="b4e90-208">Abyste měli jistotu, že je ve správném formátu, nebezpečné regulární výraz se provádí bez ověření.</span><span class="sxs-lookup"><span data-stu-id="b4e90-208">No validation is done to make sure it is a well-formed, non-dangerous regex.</span></span>
* <span data-ttu-id="b4e90-209">Musí obsahovat skupinu zachycení.</span><span class="sxs-lookup"><span data-stu-id="b4e90-209">It must contain a capture group.</span></span> <span data-ttu-id="b4e90-210">Celý regulární výraz se musí shodovat celý token.</span><span class="sxs-lookup"><span data-stu-id="b4e90-210">The entire regex must match the entire token.</span></span> <span data-ttu-id="b4e90-211">První zachycení musí být název tokenu k vyhledání ve zdroji konfigurace.</span><span class="sxs-lookup"><span data-stu-id="b4e90-211">The first capture must be the token name to look up in the configuration source.</span></span>

## <a name="configuration-builders-in-microsoftconfigurationconfigurationbuilders"></a><span data-ttu-id="b4e90-212">Konfigurace počítačů v Microsoft.Configuration.ConfigurationBuilders</span><span class="sxs-lookup"><span data-stu-id="b4e90-212">Configuration builders in Microsoft.Configuration.ConfigurationBuilders</span></span>

### <a name="environmentconfigbuilder"></a><span data-ttu-id="b4e90-213">EnvironmentConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="b4e90-213">EnvironmentConfigBuilder</span></span>

```xml
<add name="Environment"
    [mode|prefix|stripPrefix|tokenPattern] 
    type="Microsoft.Configuration.ConfigurationBuilders.EnvironmentConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Environment" />
```

<span data-ttu-id="b4e90-214">[EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):</span><span class="sxs-lookup"><span data-stu-id="b4e90-214">The [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):</span></span>

* <span data-ttu-id="b4e90-215">Je nejjednodušší konfiguraci počítačů.</span><span class="sxs-lookup"><span data-stu-id="b4e90-215">Is the simplest of the configuration builders.</span></span>
* <span data-ttu-id="b4e90-216">Čte hodnoty z prostředí.</span><span class="sxs-lookup"><span data-stu-id="b4e90-216">Reads values from the environment.</span></span>
* <span data-ttu-id="b4e90-217">Nemá žádné další možnosti konfigurace.</span><span class="sxs-lookup"><span data-stu-id="b4e90-217">Does not have any additional configuration options.</span></span>
* <span data-ttu-id="b4e90-218">`name` Hodnota atributu je volitelný.</span><span class="sxs-lookup"><span data-stu-id="b4e90-218">The `name` attribute value is arbitrary.</span></span>

<span data-ttu-id="b4e90-219">**Poznámka:** V prostředí kontejneru Windows jsou vloženy do prostředí vstupního bodu procesu pouze proměnné nastavené v době běhu.</span><span class="sxs-lookup"><span data-stu-id="b4e90-219">**Note:** In a Windows container environment, variables set at run time are only injected into the EntryPoint process environment.</span></span> <span data-ttu-id="b4e90-220">Aplikace, na kterých běží jako služba nebo bez vstupního bodu procesu není vyzvednutí tyto proměnné není-li jinak vloží mechanismem v kontejneru.</span><span class="sxs-lookup"><span data-stu-id="b4e90-220">Apps that run as a service or a non-EntryPoint process do not pick up these variables unless they are otherwise injected through a mechanism in the container.</span></span> <span data-ttu-id="b4e90-221">Pro [IIS](https://github.com/Microsoft/iis-docker/pull/41)/[ASP.NET](https://github.com/Microsoft/aspnet-docker)– na základě kontejnerů, aktuální verze [ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41) zpracovává to *DefaultAppPool* pouze.</span><span class="sxs-lookup"><span data-stu-id="b4e90-221">For [IIS](https://github.com/Microsoft/iis-docker/pull/41)/[ASP.NET](https://github.com/Microsoft/aspnet-docker)-based containers, the current version of [ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41) handles this in the *DefaultAppPool* only.</span></span> <span data-ttu-id="b4e90-222">Ostatní varianty kontejnerů na základě Windows může být potřeba vyvíjet své vlastní mechanismus vkládání pro procesy bez vstupního bodu.</span><span class="sxs-lookup"><span data-stu-id="b4e90-222">Other Windows-based container variants may need to develop their own injection mechanism for non-EntryPoint processes.</span></span>

### <a name="usersecretsconfigbuilder"></a><span data-ttu-id="b4e90-223">UserSecretsConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="b4e90-223">UserSecretsConfigBuilder</span></span>

> [!WARNING]
> <span data-ttu-id="b4e90-224">Nikdy ukládat hesla, citlivé připojovací řetězce nebo jiných citlivých dat. ve zdrojovém kódu.</span><span class="sxs-lookup"><span data-stu-id="b4e90-224">Never store passwords, sensitive connection strings, or other sensitive data in source code.</span></span> <span data-ttu-id="b4e90-225">Tajné klíče v produkčním prostředí by se neměly pro vývoj nebo testování.</span><span class="sxs-lookup"><span data-stu-id="b4e90-225">Production secrets should not be used for development or test.</span></span>

```xml
<add name="UserSecrets"
    [mode|prefix|stripPrefix|tokenPattern]
    (userSecretsId="{secret string, typically a GUID}" | userSecretsFile="~\secrets.file")
    [optional="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.UserSecrets" />
```

<span data-ttu-id="b4e90-226">Tvůrce tato konfigurace poskytuje podobné funkce [ASP.NET Core tajný klíč správce](/aspnet/core/security/app-secrets).</span><span class="sxs-lookup"><span data-stu-id="b4e90-226">This configuration builder provides a feature similar to [ASP.NET Core Secret Manager](/aspnet/core/security/app-secrets).</span></span>

<span data-ttu-id="b4e90-227">[UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/) je možné použít v projektech .NET Framework, ale je třeba zadat soubor tajných kódů.</span><span class="sxs-lookup"><span data-stu-id="b4e90-227">The [UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/) can be used in .NET Framework projects, but a secrets file must be specified.</span></span> <span data-ttu-id="b4e90-228">Alternativně můžete definovat `UserSecretsId` vlastnost v projektu soubor a vytvořte soubor raw tajné kódy ve správném umístění pro čtení.</span><span class="sxs-lookup"><span data-stu-id="b4e90-228">Alternatively, you can define the `UserSecretsId` property in the project file and create the raw secrets file in the correct location for reading.</span></span> <span data-ttu-id="b4e90-229">Zachovat externí závislosti mimo váš projekt, soubor tajného kódu je ve formátu XML.</span><span class="sxs-lookup"><span data-stu-id="b4e90-229">To keep external dependencies out of your project, the secret file is XML formatted.</span></span> <span data-ttu-id="b4e90-230">Formát XML je k implementaci se týká a formát byste se neměli spoléhat.</span><span class="sxs-lookup"><span data-stu-id="b4e90-230">The XML formatting is an implementation detail, and the format should not be relied upon.</span></span> <span data-ttu-id="b4e90-231">Pokud je potřeba sdílet *secrets.json* soubor s projekty .NET Core, zvažte použití [SimpleJsonConfigBuilder](#simplejsonconfigbuilder).</span><span class="sxs-lookup"><span data-stu-id="b4e90-231">If you need to share a *secrets.json* file with .NET Core projects, consider using the [SimpleJsonConfigBuilder](#simplejsonconfigbuilder).</span></span> <span data-ttu-id="b4e90-232">`SimpleJsonConfigBuilder` Formátování pro .NET Core byste také zvážit podrobnost implementace může změnit.</span><span class="sxs-lookup"><span data-stu-id="b4e90-232">The `SimpleJsonConfigBuilder` format for .NET Core should also be considered an implementation detail subject to change.</span></span>

<span data-ttu-id="b4e90-233">Konfigurace atributů pro `UserSecretsConfigBuilder`:</span><span class="sxs-lookup"><span data-stu-id="b4e90-233">Configuration attributes for `UserSecretsConfigBuilder`:</span></span>

* `userSecretsId` <span data-ttu-id="b4e90-234">– Toto je upřednostňovanou metodou pro určení souboru XML tajných kódů.</span><span class="sxs-lookup"><span data-stu-id="b4e90-234">- This is the preferred method for identifying an XML secrets file.</span></span> <span data-ttu-id="b4e90-235">Pracuje podobně až po .NET Core, který používá `UserSecretsId` pro uložení tohoto identifikátoru vlastnosti projektu.</span><span class="sxs-lookup"><span data-stu-id="b4e90-235">It works similar to .NET Core, which uses a `UserSecretsId` project property to store this identifier.</span></span> <span data-ttu-id="b4e90-236">Řetězec musí být jedinečný, nemusí být identifikátor GUID.</span><span class="sxs-lookup"><span data-stu-id="b4e90-236">The string must be unique, it doesn't need to be a GUID.</span></span> <span data-ttu-id="b4e90-237">Pomocí tohoto atributu `UserSecretsConfigBuilder` dobře známé místní umístění (`%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml`) pro soubor tajných kódů, které patří do tohoto identifikátoru.</span><span class="sxs-lookup"><span data-stu-id="b4e90-237">With this attribute, the `UserSecretsConfigBuilder` look in a well-known local location (`%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml`) for a secrets file belonging to this identifier.</span></span>
* `userSecretsFile` <span data-ttu-id="b4e90-238">-Volitelný atribut určení souboru, který obsahuje tajné klíče.</span><span class="sxs-lookup"><span data-stu-id="b4e90-238">- An optional attribute specifying the file containing the secrets.</span></span> <span data-ttu-id="b4e90-239">`~` Znak lze použít na začátku tak, aby odkazovaly kořenový adresář aplikace.</span><span class="sxs-lookup"><span data-stu-id="b4e90-239">The `~` character can be used at the start to reference the application root.</span></span> <span data-ttu-id="b4e90-240">Buď tento atribut nebo `userSecretsId` atribut je vyžadován.</span><span class="sxs-lookup"><span data-stu-id="b4e90-240">Either this attribute or the `userSecretsId` attribute is required.</span></span> <span data-ttu-id="b4e90-241">Pokud jsou zadány oba `userSecretsFile` přednost.</span><span class="sxs-lookup"><span data-stu-id="b4e90-241">If both are specified, `userSecretsFile` takes precedence.</span></span>
* `optional`<span data-ttu-id="b4e90-242">: logická hodnota, výchozí hodnota `true` – brání výjimku, pokud nelze najít soubor tajných kódů.</span><span class="sxs-lookup"><span data-stu-id="b4e90-242">: boolean, default value `true` - Prevents an exception if the secrets file cannot be found.</span></span> 
* <span data-ttu-id="b4e90-243">`name` Hodnota atributu je volitelný.</span><span class="sxs-lookup"><span data-stu-id="b4e90-243">The `name` attribute value is arbitrary.</span></span>

<span data-ttu-id="b4e90-244">Soubor tajných kódů má následující formát:</span><span class="sxs-lookup"><span data-stu-id="b4e90-244">The secrets file has the following format:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<root>
  <secrets ver="1.0">
    <secret name="secret key name" value="secret value" />
  </secrets>
</root>
```

### <a name="azurekeyvaultconfigbuilder"></a><span data-ttu-id="b4e90-245">AzureKeyVaultConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="b4e90-245">AzureKeyVaultConfigBuilder</span></span>

```xml
<add name="AzureKeyVault"
    [mode|prefix|stripPrefix|tokenPattern]
    (vaultName="MyVaultName" |
     uri="https:/MyVaultName.vault.azure.net")
    [connectionString="connection string"]
    [version="secrets version"]
    [preloadSecretNames="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.AzureKeyVaultConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Azure" />
```

<span data-ttu-id="b4e90-246">[AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/) čte hodnoty uložené v [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span><span class="sxs-lookup"><span data-stu-id="b4e90-246">The [AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/) reads values stored in the [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span></span>

`vaultName` <span data-ttu-id="b4e90-247">je vyžadováno (název trezoru), nebo identifikátor URI pro trezor.</span><span class="sxs-lookup"><span data-stu-id="b4e90-247">is required (either the name of the vault or a URI to the vault).</span></span> <span data-ttu-id="b4e90-248">Povolit řízení, o které trezoru pro připojení k další atributy, ale jsou nutné jenom v případě aplikace není spuštěna v prostředí, která funguje s `Microsoft.Azure.Services.AppAuthentication`.</span><span class="sxs-lookup"><span data-stu-id="b4e90-248">The other attributes allow control about which vault to connect to, but are only necessary if the application is not running in an environment that works with `Microsoft.Azure.Services.AppAuthentication`.</span></span> <span data-ttu-id="b4e90-249">Knihovny ověřování služby Azure se používá k automaticky získávají informace o připojení z prostředí pro spouštění Pokud je to možné.</span><span class="sxs-lookup"><span data-stu-id="b4e90-249">The Azure Services Authentication library is used to automatically pick up connection information from the execution environment if possible.</span></span> <span data-ttu-id="b4e90-250">Můžete přepsat automaticky vyzvednutí informace o připojení tím, že poskytuje připojovací řetězec.</span><span class="sxs-lookup"><span data-stu-id="b4e90-250">You can override automatically pick up of connection information by providing a connection string.</span></span>

* `vaultName` <span data-ttu-id="b4e90-251">– Požadováno pokud `uri` v není k dispozici.</span><span class="sxs-lookup"><span data-stu-id="b4e90-251">- Required if `uri` in not provided.</span></span> <span data-ttu-id="b4e90-252">Určuje název úložiště ve vašem předplatném Azure, ze kterého se mají číst páry klíč/hodnota.</span><span class="sxs-lookup"><span data-stu-id="b4e90-252">Specifies the name of the vault in your Azure subscription from which to read key/value pairs.</span></span>
* `connectionString` <span data-ttu-id="b4e90-253">– Připojovací řetězec použitelný [AzureServiceTokenProvider](https://docs.microsoft.com/en-us/azure/key-vault/service-to-service-authentication#connection-string-support)</span><span class="sxs-lookup"><span data-stu-id="b4e90-253">- A connection string usable by [AzureServiceTokenProvider](https://docs.microsoft.com/en-us/azure/key-vault/service-to-service-authentication#connection-string-support)</span></span>
* `uri` <span data-ttu-id="b4e90-254">-Připojení s ostatními poskytovateli služby Key Vault se zadaným `uri` hodnotu.</span><span class="sxs-lookup"><span data-stu-id="b4e90-254">- Connects to other Key Vault providers with the specified `uri` value.</span></span> <span data-ttu-id="b4e90-255">Pokud není zadán, Azure (`vaultName`) je poskytovatel trezoru.</span><span class="sxs-lookup"><span data-stu-id="b4e90-255">If not specified, Azure (`vaultName`) is the vault provider.</span></span>
* `version` <span data-ttu-id="b4e90-256">-Azure Key Vault poskytuje funkce správy verzí pro tajné kódy.</span><span class="sxs-lookup"><span data-stu-id="b4e90-256">- Azure Key Vault provides a versioning feature for secrets.</span></span> <span data-ttu-id="b4e90-257">Pokud `version` není zadána, Tvůrce pouze načte tajných kódů odpovídající této verze.</span><span class="sxs-lookup"><span data-stu-id="b4e90-257">If `version` is specified, the builder only retrieves secrets matching this version.</span></span>
* `preloadSecretNames` <span data-ttu-id="b4e90-258">– Ve výchozím nastavení tato querys Tvůrce **všechny** klíče názvy v trezoru klíčů po jeho inicializaci.</span><span class="sxs-lookup"><span data-stu-id="b4e90-258">- By default, this builder querys **all** key names in the key vault when it is initialized.</span></span> <span data-ttu-id="b4e90-259">Pokud chcete zabránit, všechny hodnoty klíče pro čtení, tento atribut nastavte na `false`.</span><span class="sxs-lookup"><span data-stu-id="b4e90-259">To prevent reading all key values, set this attribute to `false`.</span></span> <span data-ttu-id="b4e90-260">Nastavení na `false` přečte tajných kódů jeden po druhém.</span><span class="sxs-lookup"><span data-stu-id="b4e90-260">Setting this to `false` reads secrets one at a time.</span></span> <span data-ttu-id="b4e90-261">Tajné kódy, které postupně po jednom můžete užitečné, pokud trezor umožňuje přístup "Get" ale ne "seznam" přístup ke čtení.</span><span class="sxs-lookup"><span data-stu-id="b4e90-261">Reading secrets one at a time can useful if the vault allows "Get" access but not "List" access.</span></span> <span data-ttu-id="b4e90-262">**Poznámka:** Při použití `Greedy` režimu `preloadSecretNames` musí být `true` (výchozí nastavení.)</span><span class="sxs-lookup"><span data-stu-id="b4e90-262">**Note:** When using `Greedy` mode, `preloadSecretNames` must be `true` (the default.)</span></span>

### <a name="keyperfileconfigbuilder"></a><span data-ttu-id="b4e90-263">KeyPerFileConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="b4e90-263">KeyPerFileConfigBuilder</span></span>

```xml
<add name="KeyPerFile"
    [mode|prefix|stripPrefix|tokenPattern]
    (directoryPath="PathToSourceDirectory")
    [ignorePrefix="ignore."]
    [keyDelimiter=":"]
    [optional="false"]
    type="Microsoft.Configuration.ConfigurationBuilders.KeyPerFileConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.KeyPerFile" />
```

<span data-ttu-id="b4e90-264">[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) je základní konfigurace tvůrce, který používá souborů v adresáři jako zdroj hodnoty.</span><span class="sxs-lookup"><span data-stu-id="b4e90-264">[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) is a basic configuration builder that uses a directory's files as a source of values.</span></span> <span data-ttu-id="b4e90-265">Název souboru je klíč a obsah se hodnota.</span><span class="sxs-lookup"><span data-stu-id="b4e90-265">A file's name is the key, and the contents are the value.</span></span> <span data-ttu-id="b4e90-266">Tvůrce této konfigurace může být užitečné při spuštění v prostředí iniciovat organizovaně, což kontejneru.</span><span class="sxs-lookup"><span data-stu-id="b4e90-266">This configuration builder can be useful when running in an orchestrated container environment.</span></span> <span data-ttu-id="b4e90-267">Systémy, jako je Docker Swarm a Kubernetes poskytují `secrets` na své kontejnery iniciovat organizovaně, což windows tímto způsobem na soubor klíče.</span><span class="sxs-lookup"><span data-stu-id="b4e90-267">Systems like Docker Swarm and Kubernetes provide `secrets` to their orchestrated windows containers in this key-per-file manner.</span></span>

<span data-ttu-id="b4e90-268">Podrobnosti atributu:</span><span class="sxs-lookup"><span data-stu-id="b4e90-268">Attribute details:</span></span>

* `directoryPath` <span data-ttu-id="b4e90-269">-Vyžaduje.</span><span class="sxs-lookup"><span data-stu-id="b4e90-269">- Required.</span></span> <span data-ttu-id="b4e90-270">Určuje cestu k vyhledání hodnoty.</span><span class="sxs-lookup"><span data-stu-id="b4e90-270">Specifies a path to look in for values.</span></span> <span data-ttu-id="b4e90-271">Docker pro Windows se tajné kódy jsou uložené v *C:\ProgramData\Docker\secrets* adresáře ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="b4e90-271">Docker for Windows secrets are stored in the *C:\ProgramData\Docker\secrets* directory by default.</span></span>
* `ignorePrefix` <span data-ttu-id="b4e90-272">– Soubory, které začínat touto předponou budou vyloučeny.</span><span class="sxs-lookup"><span data-stu-id="b4e90-272">- Files that start with this prefix are excluded.</span></span> <span data-ttu-id="b4e90-273">Výchozí hodnota je "ignorovat.".</span><span class="sxs-lookup"><span data-stu-id="b4e90-273">Defaults to "ignore.".</span></span>
* `keyDelimiter` <span data-ttu-id="b4e90-274">– Výchozí hodnota je `null`.</span><span class="sxs-lookup"><span data-stu-id="b4e90-274">- Default value is `null`.</span></span> <span data-ttu-id="b4e90-275">-Li zadána, Tvůrce konfigurace prochází přes několik úrovní adresáře, vytváření názvy klíčů s tímto oddělovačem.</span><span class="sxs-lookup"><span data-stu-id="b4e90-275">If specified, the configuration builder traverses multiple levels of the directory, building up key names with this delimiter.</span></span> <span data-ttu-id="b4e90-276">Pokud je tato hodnota `null`, Tvůrce konfigurace prohledá pouze na nejvyšší úrovni adresáře.</span><span class="sxs-lookup"><span data-stu-id="b4e90-276">If this value is `null`, the configuration builder only looks at the top level of the directory.</span></span>
* `optional` <span data-ttu-id="b4e90-277">– Výchozí hodnota je `false`.</span><span class="sxs-lookup"><span data-stu-id="b4e90-277">-  Default value is `false`.</span></span> <span data-ttu-id="b4e90-278">Určuje, zda by měl Tvůrce konfigurace způsobit chyby, pokud zdrojový adresář neexistuje.</span><span class="sxs-lookup"><span data-stu-id="b4e90-278">Specifies whether the configuration builder should cause errors if the source directory doesn't exist.</span></span>

### <a name="simplejsonconfigbuilder"></a><span data-ttu-id="b4e90-279">SimpleJsonConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="b4e90-279">SimpleJsonConfigBuilder</span></span>

> [!WARNING]
> <span data-ttu-id="b4e90-280">Nikdy ukládat hesla, citlivé připojovací řetězce nebo jiných citlivých dat. ve zdrojovém kódu.</span><span class="sxs-lookup"><span data-stu-id="b4e90-280">Never store passwords, sensitive connection strings, or other sensitive data in source code.</span></span> <span data-ttu-id="b4e90-281">Tajné klíče v produkčním prostředí by se neměly pro vývoj nebo testování.</span><span class="sxs-lookup"><span data-stu-id="b4e90-281">Production secrets should not be used for development or test.</span></span>

```xml
<add name="SimpleJson"
    [mode|prefix|stripPrefix|tokenPattern]
    jsonFile="~\config.json"
    [optional="true"]
    [jsonMode="(Flat|Sectional)"]
    type="Microsoft.Configuration.ConfigurationBuilders.SimpleJsonConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Json" />
```

<span data-ttu-id="b4e90-282">Projekty .NET core často používají pro konfigurační soubory JSON.</span><span class="sxs-lookup"><span data-stu-id="b4e90-282">.NET Core projects frequently use JSON files for configuration.</span></span> <span data-ttu-id="b4e90-283">[SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) Tvůrce umožňuje soubory .NET Core JSON pro použití v rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="b4e90-283">The [SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) builder allows .NET Core JSON files to be used in the .NET Framework.</span></span> <span data-ttu-id="b4e90-284">Tvůrce této konfigurace je poskytuje základní mapování ze zdroje bez stromové struktury klíč/hodnota do oblasti konkrétní klíč/hodnota konfigurace rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="b4e90-284">This configuration builder is provides a basic mapping from a flat key/value source into specific key/value areas of .NET Framework configuration.</span></span> <span data-ttu-id="b4e90-285">Tato konfigurace Tvůrce nemá **není** poskytují pro hierarchické konfigurace.</span><span class="sxs-lookup"><span data-stu-id="b4e90-285">This configuration builder does **not** provide for hierarchical configurations.</span></span> <span data-ttu-id="b4e90-286">Základní soubor JSON je podobný slovník, není komplexní hierarchický objekt.</span><span class="sxs-lookup"><span data-stu-id="b4e90-286">The JSON backing file is similar to a dictionary, not a complex hierarchical object.</span></span> <span data-ttu-id="b4e90-287">Víceúrovňových hierarchických soubor lze použít.</span><span class="sxs-lookup"><span data-stu-id="b4e90-287">A multi-level hierarchical file can be used.</span></span> <span data-ttu-id="b4e90-288">Tento zprostředkovatel `flatten`s hloubkou připojením názvu vlastnosti na každé úrovni pomocí `:` jako oddělovač.</span><span class="sxs-lookup"><span data-stu-id="b4e90-288">This provider `flatten`s the depth by appending the property name at each level using `:` as a delimiter.</span></span>

<span data-ttu-id="b4e90-289">Podrobnosti atributu:</span><span class="sxs-lookup"><span data-stu-id="b4e90-289">Attribute details:</span></span>

* `jsonFile` <span data-ttu-id="b4e90-290">-Vyžaduje.</span><span class="sxs-lookup"><span data-stu-id="b4e90-290">- Required.</span></span> <span data-ttu-id="b4e90-291">Určuje soubor JSON, který se má načíst z.</span><span class="sxs-lookup"><span data-stu-id="b4e90-291">Specifies the JSON file to read from.</span></span> <span data-ttu-id="b4e90-292">`~` Znak je možné při spuštění aplikace kořen odkazu.</span><span class="sxs-lookup"><span data-stu-id="b4e90-292">The `~` character can be used at the start to reference the app root.</span></span>
* `optional` <span data-ttu-id="b4e90-293">-Logická hodnota, výchozí hodnota je `true`.</span><span class="sxs-lookup"><span data-stu-id="b4e90-293">- Boolean,  default value is `true`.</span></span> <span data-ttu-id="b4e90-294">Brání generování výjimek, pokud nelze najít soubor JSON.</span><span class="sxs-lookup"><span data-stu-id="b4e90-294">Prevents throwing exceptions if the JSON file cannot be found.</span></span>
* `jsonMode`<span data-ttu-id="b4e90-295"> - `[Flat|Sectional]\`.</span><span class="sxs-lookup"><span data-stu-id="b4e90-295"> - `[Flat|Sectional]\`.</span></span> `Flat` <span data-ttu-id="b4e90-296">je výchozí nastavení.</span><span class="sxs-lookup"><span data-stu-id="b4e90-296">is the default.</span></span> <span data-ttu-id="b4e90-297">Když `jsonMode` je `Flat`, soubor JSON je zdrojem plochý klíč/hodnota.</span><span class="sxs-lookup"><span data-stu-id="b4e90-297">When `jsonMode` is `Flat`, the JSON file is a single flat key/value source.</span></span> <span data-ttu-id="b4e90-298">`EnvironmentConfigBuilder` a `AzureKeyVaultConfigBuilder` jsou také zdrojů bez stromové struktury klíč/hodnota.</span><span class="sxs-lookup"><span data-stu-id="b4e90-298">The `EnvironmentConfigBuilder` and `AzureKeyVaultConfigBuilder` are also single flat key/value sources.</span></span> <span data-ttu-id="b4e90-299">Když `SimpleJsonConfigBuilder` je nakonfigurovaný v `Sectional` režimu:</span><span class="sxs-lookup"><span data-stu-id="b4e90-299">When the `SimpleJsonConfigBuilder` is configured in `Sectional` mode:</span></span>

  * <span data-ttu-id="b4e90-300">Soubor JSON je jenom na nejvyšší úrovni koncepčně rozdělen do více slovníky.</span><span class="sxs-lookup"><span data-stu-id="b4e90-300">The JSON file is conceptually divided just at the top level into multiple dictionaries.</span></span>
  * <span data-ttu-id="b4e90-301">Každý z slovníků platí jenom pro konfigurační oddíl, který odpovídá názvu vlastností nejvyšší úrovně připojená k nim.</span><span class="sxs-lookup"><span data-stu-id="b4e90-301">Each of the dictionaries is only applied to the configuration section that matches the top-level property name attached to them.</span></span> <span data-ttu-id="b4e90-302">Příklad:</span><span class="sxs-lookup"><span data-stu-id="b4e90-302">For example:</span></span>

```json
    {
        "appSettings" : {
            "setting1" : "value1",
            "setting2" : "value2",
            "complex" : {
                "setting1" : "complex:value1",
                "setting2" : "complex:value2",
            }
        }
    }
```

## <a name="implementing-a-custom-keyvalue-configuration-builder"></a><span data-ttu-id="b4e90-303">Implementace Tvůrce vlastní klíč/hodnota konfigurace</span><span class="sxs-lookup"><span data-stu-id="b4e90-303">Implementing a custom key/value configuration builder</span></span>

<span data-ttu-id="b4e90-304">Pokud konfigurace tvůrci nevyhovují vašim potřebám, můžete napsat vlastní.</span><span class="sxs-lookup"><span data-stu-id="b4e90-304">If the configuration builders don't meet your needs, you can write a custom one.</span></span> <span data-ttu-id="b4e90-305">`KeyValueConfigBuilder` Základní třídy se stará o nahrazení režimy a většina obavy předponu.</span><span class="sxs-lookup"><span data-stu-id="b4e90-305">The `KeyValueConfigBuilder` base class handles substitution modes and most prefix concerns.</span></span> <span data-ttu-id="b4e90-306">Projekt implementující potřebovat pouze:</span><span class="sxs-lookup"><span data-stu-id="b4e90-306">An implementing project need only:</span></span>

* <span data-ttu-id="b4e90-307">Dědit ze základní třídy a implementovat základní příčiny páry klíč/hodnota pomocí `GetValue` a `GetAllValues`:</span><span class="sxs-lookup"><span data-stu-id="b4e90-307">Inherit from the base class and implement a basic source of key/value pairs through the `GetValue` and `GetAllValues`:</span></span>
* <span data-ttu-id="b4e90-308">Přidat [Microsoft.Configuration.ConfigurationBuilders.Base](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) do projektu.</span><span class="sxs-lookup"><span data-stu-id="b4e90-308">Add the [Microsoft.Configuration.ConfigurationBuilders.Base](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) to the project.</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/MyCustomConfigBuilder.cs)]

<span data-ttu-id="b4e90-309">`KeyValueConfigBuilder` Základní třída poskytuje většinu práce a konzistentní chování napříč klíč/hodnota konfigurace počítačů.</span><span class="sxs-lookup"><span data-stu-id="b4e90-309">The `KeyValueConfigBuilder` base class provides much of the work and consistent behavior across key/value configuration builders.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b4e90-310">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="b4e90-310">Additional resources</span></span>

* [<span data-ttu-id="b4e90-311">Úložiště GitHub tvůrci konfigurace</span><span class="sxs-lookup"><span data-stu-id="b4e90-311">Configuration Builders GitHub repository</span></span>](https://github.com/aspnet/MicrosoftConfigurationBuilders)
* [<span data-ttu-id="b4e90-312">Ověřování služba služba do služby Azure Key Vault pomocí rozhraní .NET</span><span class="sxs-lookup"><span data-stu-id="b4e90-312">Service-to-service authentication to Azure Key Vault using .NET</span></span>](/azure/key-vault/service-to-service-authentication#connection-string-support)
