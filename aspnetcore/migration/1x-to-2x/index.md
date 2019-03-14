---
title: Migrace z technologie ASP.NET Core 1.x do 2.0
author: scottaddie
description: Tento článek popisuje požadavky a nejběžnější kroky migrace projektu aplikace ASP.NET Core 1.x do ASP.NET Core 2.0.
ms.author: scaddie
ms.custom: mvc
ms.date: 10/24/2018
uid: migration/1x-to-2x/index
---
# <a name="migrate-from-aspnet-core-1x-to-20"></a><span data-ttu-id="0ad39-103">Migrace z technologie ASP.NET Core 1.x do 2.0</span><span class="sxs-lookup"><span data-stu-id="0ad39-103">Migrate from ASP.NET Core 1.x to 2.0</span></span>

<span data-ttu-id="0ad39-104">Podle [Scott Addie](https://github.com/scottaddie)</span><span class="sxs-lookup"><span data-stu-id="0ad39-104">By [Scott Addie](https://github.com/scottaddie)</span></span>

<span data-ttu-id="0ad39-105">V tomto článku jsme vás provede aktualizaci existující projekt ASP.NET Core 1.x do ASP.NET Core 2.0.</span><span class="sxs-lookup"><span data-stu-id="0ad39-105">In this article, we walk you through updating an existing ASP.NET Core 1.x project to ASP.NET Core 2.0.</span></span> <span data-ttu-id="0ad39-106">Migrace aplikace ASP.NET Core 2.0 umožňuje využít výhod [řadu nových funkcí a vylepšení výkonu](xref:aspnetcore-2.0).</span><span class="sxs-lookup"><span data-stu-id="0ad39-106">Migrating your application to ASP.NET Core 2.0 enables you to take advantage of [many new features and performance improvements](xref:aspnetcore-2.0).</span></span>

<span data-ttu-id="0ad39-107">Stávající aplikace ASP.NET Core 1.x vycházejí z šablony projektu pro konkrétní verzi.</span><span class="sxs-lookup"><span data-stu-id="0ad39-107">Existing ASP.NET Core 1.x applications are based off of version-specific project templates.</span></span> <span data-ttu-id="0ad39-108">Jak rozhraní ASP.NET Core vyvíjí, proto šablony projektů a proveďte počáteční kód v nich obsažené.</span><span class="sxs-lookup"><span data-stu-id="0ad39-108">As the ASP.NET Core framework evolves, so do the project templates and the starter code contained within them.</span></span> <span data-ttu-id="0ad39-109">Kromě aktualizací rozhraní ASP.NET Core, je potřeba aktualizovat kód pro vaši aplikaci.</span><span class="sxs-lookup"><span data-stu-id="0ad39-109">In addition to updating the ASP.NET Core framework, you need to update the code for your application.</span></span>

<a name="prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="0ad39-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="0ad39-110">Prerequisites</span></span>

<span data-ttu-id="0ad39-111">Zobrazit [Začínáme s ASP.NET Core](xref:getting-started).</span><span class="sxs-lookup"><span data-stu-id="0ad39-111">See [Get Started with ASP.NET Core](xref:getting-started).</span></span>

<a name="tfm"></a>

## <a name="update-target-framework-moniker-tfm"></a><span data-ttu-id="0ad39-112">Aktualizovat Moniker cílového rozhraní (TFM)</span><span class="sxs-lookup"><span data-stu-id="0ad39-112">Update Target Framework Moniker (TFM)</span></span>

<span data-ttu-id="0ad39-113">Používejte projekty cílené na .NET Core [TFM](/dotnet/standard/frameworks#referring-to-frameworks) verze větší než nebo rovna hodnotě .NET Core 2.0.</span><span class="sxs-lookup"><span data-stu-id="0ad39-113">Projects targeting .NET Core should use the [TFM](/dotnet/standard/frameworks#referring-to-frameworks) of a version greater than or equal to .NET Core 2.0.</span></span> <span data-ttu-id="0ad39-114">Hledat `<TargetFramework>` uzlu v *.csproj* souboru a nahraďte jeho vnitřní text s `netcoreapp2.0`:</span><span class="sxs-lookup"><span data-stu-id="0ad39-114">Search for the `<TargetFramework>` node in the *.csproj* file, and replace its inner text with `netcoreapp2.0`:</span></span>

[!code-xml[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App.csproj?range=3)]

<span data-ttu-id="0ad39-115">Projekty cílené na rozhraní .NET Framework by měl používat TFM verze větší než nebo rovna hodnotě rozhraní .NET Framework 4.6.1.</span><span class="sxs-lookup"><span data-stu-id="0ad39-115">Projects targeting .NET Framework should use the TFM of a version greater than or equal to .NET Framework 4.6.1.</span></span> <span data-ttu-id="0ad39-116">Hledat `<TargetFramework>` uzlu v *.csproj* souboru a nahraďte jeho vnitřní text s `net461`:</span><span class="sxs-lookup"><span data-stu-id="0ad39-116">Search for the `<TargetFramework>` node in the *.csproj* file, and replace its inner text with `net461`:</span></span>

[!code-xml[](../1x-to-2x/samples/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App.csproj?range=4)]

> [!NOTE]
> <span data-ttu-id="0ad39-117">.NET core 2.0 nabízí mnohem větší plochu povrchu než .NET Core 1.x.</span><span class="sxs-lookup"><span data-stu-id="0ad39-117">.NET Core 2.0 offers a much larger surface area than .NET Core 1.x.</span></span> <span data-ttu-id="0ad39-118">Pokud na rozhraní .NET Framework pouze z důvodu chybějící rozhraní API v .NET Core 1.x cílí na .NET Core 2.0 je pravděpodobně fungovat.</span><span class="sxs-lookup"><span data-stu-id="0ad39-118">If you're targeting .NET Framework solely because of missing APIs in .NET Core 1.x, targeting .NET Core 2.0 is likely to work.</span></span>

<a name="global-json"></a>

## <a name="update-net-core-sdk-version-in-globaljson"></a><span data-ttu-id="0ad39-119">Aktualizovat verzi .NET Core SDK v global.json</span><span class="sxs-lookup"><span data-stu-id="0ad39-119">Update .NET Core SDK version in global.json</span></span>

<span data-ttu-id="0ad39-120">Pokud vaše řešení závisí [ *global.json* ](/dotnet/core/tools/global-json) soubor mířila na konkrétní verzi .NET Core SDK, aktualizovat jeho `version` vlastnost na používání verze 2.0 na vašem počítači nainstalovaný:</span><span class="sxs-lookup"><span data-stu-id="0ad39-120">If your solution relies upon a [*global.json*](/dotnet/core/tools/global-json) file to target a specific .NET Core SDK version, update its `version` property to use the 2.0 version installed on your machine:</span></span>

[!code-json[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/global.json?highlight=3)]

<a name="package-reference"></a>

## <a name="update-package-references"></a><span data-ttu-id="0ad39-121">Aktualizovat odkazy na balíček</span><span class="sxs-lookup"><span data-stu-id="0ad39-121">Update package references</span></span>

<span data-ttu-id="0ad39-122">*.Csproj* soubor v projektu 1.x uvádí každý balíček NuGet používá v projektu.</span><span class="sxs-lookup"><span data-stu-id="0ad39-122">The *.csproj* file in a 1.x project lists each NuGet package used by the project.</span></span>

<span data-ttu-id="0ad39-123">V projektu aplikace ASP.NET Core 2.0 cílí na .NET Core 2.0, jeden [Microsoft.aspnetcore.all](xref:fundamentals/metapackage) odkazovat *.csproj* soubor nahradí kolekce balíčků:</span><span class="sxs-lookup"><span data-stu-id="0ad39-123">In an ASP.NET Core 2.0 project targeting .NET Core 2.0, a single [metapackage](xref:fundamentals/metapackage) reference in the *.csproj* file replaces the collection of packages:</span></span>

[!code-xml[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App.csproj?range=8-10)]

<span data-ttu-id="0ad39-124">Všechny funkce technologie ASP.NET Core 2.0 a Entity Framework Core 2.0 jsou součástí Microsoft.aspnetcore.all.</span><span class="sxs-lookup"><span data-stu-id="0ad39-124">All the features of ASP.NET Core 2.0 and Entity Framework Core 2.0 are included in the metapackage.</span></span>

<span data-ttu-id="0ad39-125">Projekty ASP.NET Core 2.0, které cílí na rozhraní .NET Framework by měl dál odkazovat na jednotlivé balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="0ad39-125">ASP.NET Core 2.0 projects targeting .NET Framework should continue to reference individual NuGet packages.</span></span> <span data-ttu-id="0ad39-126">Aktualizace `Version` atribut jednotlivých `<PackageReference />` uzlu 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="0ad39-126">Update the `Version` attribute of each `<PackageReference />` node to 2.0.0.</span></span>

<span data-ttu-id="0ad39-127">Například tady je seznam `<PackageReference />` uzly použité ve obvyklou pro projekty ASP.NET Core 2.0 cílí na rozhraní .NET Framework:</span><span class="sxs-lookup"><span data-stu-id="0ad39-127">For example, here's the list of `<PackageReference />` nodes used in a typical ASP.NET Core 2.0 project targeting .NET Framework:</span></span>

[!code-xml[](../1x-to-2x/samples/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App.csproj?range=9-22)]

<a name="dot-net-cli-tool-reference"></a>

## <a name="update-net-core-cli-tools"></a><span data-ttu-id="0ad39-128">Aktualizace nástrojů rozhraní příkazového řádku .NET Core</span><span class="sxs-lookup"><span data-stu-id="0ad39-128">Update .NET Core CLI tools</span></span>

<span data-ttu-id="0ad39-129">V *.csproj* soubor, aktualizovat `Version` atribut jednotlivých `<DotNetCliToolReference />` uzlu 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="0ad39-129">In the *.csproj* file, update the `Version` attribute of each `<DotNetCliToolReference />` node to 2.0.0.</span></span>

<span data-ttu-id="0ad39-130">Například tady je seznam nástrojů rozhraní příkazového řádku používané obvyklou pro projekty ASP.NET Core 2.0 cílí na .NET Core 2.0:</span><span class="sxs-lookup"><span data-stu-id="0ad39-130">For example, here's the list of CLI tools used in a typical ASP.NET Core 2.0 project targeting .NET Core 2.0:</span></span>

[!code-xml[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App.csproj?range=12-16)]

<a name="package-target-fallback"></a>

## <a name="rename-package-target-fallback-property"></a><span data-ttu-id="0ad39-131">Přejmenovat vlastnost záložní cíl balíčku</span><span class="sxs-lookup"><span data-stu-id="0ad39-131">Rename Package Target Fallback property</span></span>

<span data-ttu-id="0ad39-132">*.Csproj* soubor projektu 1.x použít `PackageTargetFallback` uzlu a proměnné:</span><span class="sxs-lookup"><span data-stu-id="0ad39-132">The *.csproj* file of a 1.x project used a `PackageTargetFallback` node and variable:</span></span>

[!code-xml[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App.csproj?range=5)]

<span data-ttu-id="0ad39-133">Přejmenovat uzel a proměnnou pro `AssetTargetFallback`:</span><span class="sxs-lookup"><span data-stu-id="0ad39-133">Rename both the node and variable to `AssetTargetFallback`:</span></span>

[!code-xml[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App.csproj?range=4)]

<a name="program-cs"></a>

## <a name="update-main-method-in-programcs"></a><span data-ttu-id="0ad39-134">Aktualizujte metodu Main v souboru Program.cs</span><span class="sxs-lookup"><span data-stu-id="0ad39-134">Update Main method in Program.cs</span></span>

<span data-ttu-id="0ad39-135">V projektech 1.x `Main` metoda *Program.cs* podívali takto:</span><span class="sxs-lookup"><span data-stu-id="0ad39-135">In 1.x projects, the `Main` method of *Program.cs* looked like this:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Program.cs?name=snippet_ProgramCs&highlight=8-19)]

<span data-ttu-id="0ad39-136">V projektech pro 2.0 `Main` metoda *Program.cs* zjednodušili jsme:</span><span class="sxs-lookup"><span data-stu-id="0ad39-136">In 2.0 projects, the `Main` method of *Program.cs* has been simplified:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/Program.cs?highlight=8-11)]

<span data-ttu-id="0ad39-137">Přijetí této nové 2.0 vzor se důrazně doporučuje a je funkce produktu, jako je třeba [migrace Entity Framework (EF) Core](xref:data/ef-mvc/migrations) pracovat.</span><span class="sxs-lookup"><span data-stu-id="0ad39-137">The adoption of this new 2.0 pattern is highly recommended and is required for product features like [Entity Framework (EF) Core Migrations](xref:data/ef-mvc/migrations) to work.</span></span> <span data-ttu-id="0ad39-138">Například systém `Update-Database` z okna konzoly Správce balíčků nebo `dotnet ef database update` z příkazu řádku (na projekty byly převedeny do ASP.NET Core 2.0) generuje následující chybu:</span><span class="sxs-lookup"><span data-stu-id="0ad39-138">For example, running `Update-Database` from the Package Manager Console window or `dotnet ef database update` from the command line (on projects converted to ASP.NET Core 2.0) generates the following error:</span></span>

```
Unable to create an object of type '<Context>'. Add an implementation of 'IDesignTimeDbContextFactory<Context>' to the project, or see https://go.microsoft.com/fwlink/?linkid=851728 for additional patterns supported at design time.
```

<a name="add-modify-configuration"></a>

## <a name="add-configuration-providers"></a><span data-ttu-id="0ad39-139">Přidejte poskytovatele konfigurace</span><span class="sxs-lookup"><span data-stu-id="0ad39-139">Add configuration providers</span></span>

<span data-ttu-id="0ad39-140">V projektech 1.x přidání zprostředkovatele konfigurace aplikace byla nakonfigurovat pomocí `Startup` konstruktoru.</span><span class="sxs-lookup"><span data-stu-id="0ad39-140">In 1.x projects, adding configuration providers to an app was accomplished via the `Startup` constructor.</span></span> <span data-ttu-id="0ad39-141">Součástí kroky vytvoření instance `ConfigurationBuilder`, načítání příslušných poskytovatelů (proměnné prostředí, nastavení aplikace atd.) a inicializuje se členem `IConfigurationRoot`.</span><span class="sxs-lookup"><span data-stu-id="0ad39-141">The steps involved creating an instance of `ConfigurationBuilder`, loading applicable providers (environment variables, app settings, etc.), and initializing a member of `IConfigurationRoot`.</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Startup.cs?name=snippet_1xStartup)]

<span data-ttu-id="0ad39-142">Předchozí příklad načte `Configuration` člena s nastavením konfigurace z *appsettings.json* a také všechny *appsettings.\< EnvironmentName\>.json* odpovídající soubor `IHostingEnvironment.EnvironmentName` vlastnost.</span><span class="sxs-lookup"><span data-stu-id="0ad39-142">The preceding example loads the `Configuration` member with configuration settings from *appsettings.json* as well as any *appsettings.\<EnvironmentName\>.json* file matching the `IHostingEnvironment.EnvironmentName` property.</span></span> <span data-ttu-id="0ad39-143">Umístění těchto souborů je na stejné cestě jako *Startup.cs*.</span><span class="sxs-lookup"><span data-stu-id="0ad39-143">The location of these files is at the same path as *Startup.cs*.</span></span>

<span data-ttu-id="0ad39-144">V projektech, 2.0 často používaný kód konfigurace přináší 1.x projekty spustí pozadí.</span><span class="sxs-lookup"><span data-stu-id="0ad39-144">In 2.0 projects, the boilerplate configuration code inherent to 1.x projects runs behind-the-scenes.</span></span> <span data-ttu-id="0ad39-145">Proměnné prostředí a nastavení aplikace jsou načteny při spuštění.</span><span class="sxs-lookup"><span data-stu-id="0ad39-145">For example, environment variables and app settings are loaded at startup.</span></span> <span data-ttu-id="0ad39-146">Ekvivalent *Startup.cs* kódu je omezená na `IConfiguration` inicializace pomocí vloženého instance:</span><span class="sxs-lookup"><span data-stu-id="0ad39-146">The equivalent *Startup.cs* code is reduced to `IConfiguration` initialization with the injected instance:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App/Startup.cs?name=snippet_2xStartup)]

<span data-ttu-id="0ad39-147">Chcete-li odebrat výchozí poskytovatele přidal `WebHostBuilder.CreateDefaultBuilder`, vyvolat `Clear` metodu na `IConfigurationBuilder.Sources` vlastnosti uvnitř `ConfigureAppConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="0ad39-147">To remove the default providers added by `WebHostBuilder.CreateDefaultBuilder`, invoke the `Clear` method on the `IConfigurationBuilder.Sources` property inside of `ConfigureAppConfiguration`.</span></span> <span data-ttu-id="0ad39-148">Přidání zprostředkovatele zpět, využívat `ConfigureAppConfiguration` metoda *Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="0ad39-148">To add providers back, utilize the `ConfigureAppConfiguration` method in *Program.cs*:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App/Program.cs?name=snippet_ProgramMainConfigProviders&highlight=9-14)]

<span data-ttu-id="0ad39-149">Konfigurace používané `CreateDefaultBuilder` metoda v předchozím fragmentu kódu můžete vidět [tady](https://github.com/aspnet/MetaPackages/blob/rel/2.0.0/src/Microsoft.AspNetCore/WebHost.cs#L152).</span><span class="sxs-lookup"><span data-stu-id="0ad39-149">The configuration used by the `CreateDefaultBuilder` method in the preceding code snippet can be seen [here](https://github.com/aspnet/MetaPackages/blob/rel/2.0.0/src/Microsoft.AspNetCore/WebHost.cs#L152).</span></span>

<span data-ttu-id="0ad39-150">Další informace najdete v tématu [konfigurace v ASP.NET Core](xref:fundamentals/configuration/index).</span><span class="sxs-lookup"><span data-stu-id="0ad39-150">For more information, see [Configuration in ASP.NET Core](xref:fundamentals/configuration/index).</span></span>

<a name="db-init-code"></a>

## <a name="move-database-initialization-code"></a><span data-ttu-id="0ad39-151">Přesunutí databáze inicializační kód</span><span class="sxs-lookup"><span data-stu-id="0ad39-151">Move database initialization code</span></span>

<span data-ttu-id="0ad39-152">V projektech 1.x pomocí EF Core 1.x, příkazy jako `dotnet ef migrations add` provede následující akce:</span><span class="sxs-lookup"><span data-stu-id="0ad39-152">In 1.x projects using EF Core 1.x, a command such as `dotnet ef migrations add` does the following:</span></span>

1. <span data-ttu-id="0ad39-153">Vytvoří instanci `Startup` instance</span><span class="sxs-lookup"><span data-stu-id="0ad39-153">Instantiates a `Startup` instance</span></span>
1. <span data-ttu-id="0ad39-154">Vyvolá `ConfigureServices` metody pro registraci všech služeb s injektáž závislostí (včetně `DbContext` typy)</span><span class="sxs-lookup"><span data-stu-id="0ad39-154">Invokes the `ConfigureServices` method to register all services with dependency injection (including `DbContext` types)</span></span>
1. <span data-ttu-id="0ad39-155">Provádí potřebné úkoly</span><span class="sxs-lookup"><span data-stu-id="0ad39-155">Performs its requisite tasks</span></span>

<span data-ttu-id="0ad39-156">V 2.0 projektů pomocí EF Core 2.0 `Program.BuildWebHost` se vyvolá k získání aplikační služby.</span><span class="sxs-lookup"><span data-stu-id="0ad39-156">In 2.0 projects using EF Core 2.0, `Program.BuildWebHost` is invoked to obtain the application services.</span></span> <span data-ttu-id="0ad39-157">Na rozdíl od 1.x, tato akce nemá další vedlejší účinek vyvolání `Startup.Configure`.</span><span class="sxs-lookup"><span data-stu-id="0ad39-157">Unlike 1.x, this has the additional side effect of invoking `Startup.Configure`.</span></span> <span data-ttu-id="0ad39-158">Pokud vaše aplikace 1.x vyvolat databáze inicializační kód v jeho `Configure` metodu, může dojít k neočekávaným problémům.</span><span class="sxs-lookup"><span data-stu-id="0ad39-158">If your 1.x app invoked database initialization code in its `Configure` method, unexpected problems can occur.</span></span> <span data-ttu-id="0ad39-159">Například pokud databáze ještě neexistuje, osazení kód se spustí před spuštěním příkazu migrace EF Core.</span><span class="sxs-lookup"><span data-stu-id="0ad39-159">For example, if the database doesn't yet exist, the seeding code runs before the EF Core Migrations command execution.</span></span> <span data-ttu-id="0ad39-160">Způsobí, že tento problém `dotnet ef migrations list` příkaz selhat, pokud databáze ještě neexistuje.</span><span class="sxs-lookup"><span data-stu-id="0ad39-160">This problem causes a `dotnet ef migrations list` command to fail if the database doesn't yet exist.</span></span>

<span data-ttu-id="0ad39-161">Uvažujme následující kód inicializace 1.x počáteční hodnoty v `Configure` metoda *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="0ad39-161">Consider the following 1.x seed initialization code in the `Configure` method of *Startup.cs*:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Startup.cs?name=snippet_ConfigureSeedData&highlight=8)]

<span data-ttu-id="0ad39-162">V projektech, 2.0, přesunout `SeedData.Initialize` volání `Main` metoda *Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="0ad39-162">In 2.0 projects, move the `SeedData.Initialize` call to the `Main` method of *Program.cs*:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/Program2.cs?name=snippet_Main2Code&highlight=10)]

<span data-ttu-id="0ad39-163">Od verze 2.0, je špatný postup k ničemu `BuildWebHost` s výjimkou sestavení a konfiguraci webového hostitele.</span><span class="sxs-lookup"><span data-stu-id="0ad39-163">As of 2.0, it's bad practice to do anything in `BuildWebHost` except build and configure the web host.</span></span> <span data-ttu-id="0ad39-164">Cokoli, co se týká spuštění aplikace by měly být zpracovány mimo `BuildWebHost` &mdash; obvykle v `Main` metoda *Program.cs*.</span><span class="sxs-lookup"><span data-stu-id="0ad39-164">Anything that's about running the application should be handled outside of `BuildWebHost` &mdash; typically in the `Main` method of *Program.cs*.</span></span>

<a name="view-compilation"></a>

## <a name="review-razor-view-compilation-setting"></a><span data-ttu-id="0ad39-165">Zkontrolujte nastavení kompilace zobrazení Razor</span><span class="sxs-lookup"><span data-stu-id="0ad39-165">Review Razor view compilation setting</span></span>

<span data-ttu-id="0ad39-166">Rychlejší spuštění aplikace a menší publikované sady jsou naprosto vám.</span><span class="sxs-lookup"><span data-stu-id="0ad39-166">Faster application startup time and smaller published bundles are of utmost importance to you.</span></span> <span data-ttu-id="0ad39-167">Z těchto důvodů [kompilace zobrazení Razor](xref:mvc/views/view-compilation) je povolené ve výchozím nastavení v ASP.NET Core 2.0.</span><span class="sxs-lookup"><span data-stu-id="0ad39-167">For these reasons, [Razor view compilation](xref:mvc/views/view-compilation) is enabled by default in ASP.NET Core 2.0.</span></span>

<span data-ttu-id="0ad39-168">Nastavení `MvcRazorCompileOnPublish` vlastnost na hodnotu true se už nevyžaduje.</span><span class="sxs-lookup"><span data-stu-id="0ad39-168">Setting the `MvcRazorCompileOnPublish` property to true is no longer required.</span></span> <span data-ttu-id="0ad39-169">Pokud se zakázání kompilace zobrazení, vlastnosti mohou být odebrány *.csproj* souboru.</span><span class="sxs-lookup"><span data-stu-id="0ad39-169">Unless you're disabling view compilation, the property may be removed from the *.csproj* file.</span></span>

<span data-ttu-id="0ad39-170">Při cílení na rozhraní .NET Framework, je stále potřeba explicitně odkazovat [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation) balíčku NuGet ve vaší *.csproj* souboru:</span><span class="sxs-lookup"><span data-stu-id="0ad39-170">When targeting .NET Framework, you still need to explicitly reference the [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation) NuGet package in your *.csproj* file:</span></span>

[!code-xml[](../1x-to-2x/samples/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App.csproj?range=15)]

<a name="app-insights"></a>

## <a name="rely-on-application-insights-light-up-features"></a><span data-ttu-id="0ad39-171">Spolehněte se na funkce "světla nahoru" Application Insights</span><span class="sxs-lookup"><span data-stu-id="0ad39-171">Rely on Application Insights "light-up" features</span></span>

<span data-ttu-id="0ad39-172">Snadné nastavení instrumentace aplikací výkonu je důležité.</span><span class="sxs-lookup"><span data-stu-id="0ad39-172">Effortless setup of application performance instrumentation is important.</span></span> <span data-ttu-id="0ad39-173">Nyní se můžete spolehnout na novém [Application Insights](/azure/application-insights/app-insights-overview) "světla nahoru" funkcí nástroje Visual Studio 2017 k dispozici.</span><span class="sxs-lookup"><span data-stu-id="0ad39-173">You can now rely on the new [Application Insights](/azure/application-insights/app-insights-overview) "light-up" features available in the Visual Studio 2017 tooling.</span></span>

<span data-ttu-id="0ad39-174">Projekty ASP.NET Core 1.1 vytvořené v sadě Visual Studio 2017 přidat Application Insights ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="0ad39-174">ASP.NET Core 1.1 projects created in Visual Studio 2017 added Application Insights by default.</span></span> <span data-ttu-id="0ad39-175">Pokud nepoužíváte sadu SDK Application Insights přímo, mimo *Program.cs* a *Startup.cs*, postupujte podle těchto kroků:</span><span class="sxs-lookup"><span data-stu-id="0ad39-175">If you're not using the Application Insights SDK directly, outside of *Program.cs* and *Startup.cs*, follow these steps:</span></span>

1. <span data-ttu-id="0ad39-176">Pokud je zaměřen na .NET Core, odeberte následující `<PackageReference />` uzlu z *.csproj* souboru:</span><span class="sxs-lookup"><span data-stu-id="0ad39-176">If targeting .NET Core, remove the following `<PackageReference />` node from the *.csproj* file:</span></span>

    [!code-xml[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App.csproj?range=10)]

2. <span data-ttu-id="0ad39-177">Pokud cílí na .NET Core, odeberte `UseApplicationInsights` volání metody rozšíření z *Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="0ad39-177">If targeting .NET Core, remove the `UseApplicationInsights` extension method invocation from *Program.cs*:</span></span>

    [!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Program.cs?name=snippet_ProgramCsMain&highlight=8)]

3. <span data-ttu-id="0ad39-178">Odeberte volání rozhraní API služby Application Insights na straně klienta z *_Layout.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="0ad39-178">Remove the Application Insights client-side API call from *_Layout.cshtml*.</span></span> <span data-ttu-id="0ad39-179">To zahrnuje následující dva řádky kódu:</span><span class="sxs-lookup"><span data-stu-id="0ad39-179">It comprises the following two lines of code:</span></span>

    [!code-cshtml[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Views/Shared/_Layout.cshtml?range=1,19&dedent=4)]

<span data-ttu-id="0ad39-180">Pokud používáte sadu SDK Application Insights přímo, Uděláte to tak dál.</span><span class="sxs-lookup"><span data-stu-id="0ad39-180">If you are using the Application Insights SDK directly, continue to do so.</span></span> <span data-ttu-id="0ad39-181">Rozhraní příkazového řádku 2.0 [Microsoft.aspnetcore.all](xref:fundamentals/metapackage) obsahuje nejnovější verzi služby Application Insights, takže pokud už odkazuje na starší verze, zobrazí se chyba downgrade balíčku.</span><span class="sxs-lookup"><span data-stu-id="0ad39-181">The 2.0 [metapackage](xref:fundamentals/metapackage) includes the latest version of Application Insights, so a package downgrade error appears if you're referencing an older version.</span></span>

<a name="auth-and-identity"></a>

## <a name="adopt-authenticationidentity-improvements"></a><span data-ttu-id="0ad39-182">Přijmout vylepšení ověřování a identita</span><span class="sxs-lookup"><span data-stu-id="0ad39-182">Adopt authentication/Identity improvements</span></span>

<span data-ttu-id="0ad39-183">ASP.NET Core 2.0 je nový model ověřování a počet významných změn ASP.NET Core Identity.</span><span class="sxs-lookup"><span data-stu-id="0ad39-183">ASP.NET Core 2.0 has a new authentication model and a number of significant changes to ASP.NET Core Identity.</span></span> <span data-ttu-id="0ad39-184">Pokud jste vytvořili projekt s jednotlivými uživatelskými účty, které jsou povolené, nebo pokud jste ručně přidali ověřování nebo Identity, najdete v článku [migrovat ověřování a identita na technologii ASP.NET Core 2.0](xref:migration/1x-to-2x/identity-2x).</span><span class="sxs-lookup"><span data-stu-id="0ad39-184">If you created your project with Individual User Accounts enabled, or if you have manually added authentication or Identity, see [Migrate Authentication and Identity to ASP.NET Core 2.0](xref:migration/1x-to-2x/identity-2x).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0ad39-185">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="0ad39-185">Additional resources</span></span>

* [<span data-ttu-id="0ad39-186">Rozbíjející změny v ASP.NET Core 2.0</span><span class="sxs-lookup"><span data-stu-id="0ad39-186">Breaking Changes in ASP.NET Core 2.0</span></span>](https://github.com/aspnet/announcements/issues?page=1&q=is%3Aissue+is%3Aopen+label%3A2.0.0+label%3A%22Breaking+change%22&utf8=%E2%9C%93)
