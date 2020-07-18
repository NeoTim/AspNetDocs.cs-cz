---
uid: config-builder
title: Tvůrci konfigurace pro ASP.NET
author: rick-anderson
description: Naučte se, jak získat konfigurační data z jiných zdrojů než web.config hodnot z externích zdrojů.
ms.author: riande
ms.date: 7/17/2020
msc.type: content
ms.openlocfilehash: 1f95efcceb2ecf33fece12174cecf65cd8b27675
ms.sourcegitcommit: 000cbcd1de66fe8a766f203ef2d6f009e4435f53
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/16/2020
ms.locfileid: "86424797"
---
# <a name="configuration-builders-for-aspnet"></a>Tvůrci konfigurace pro ASP.NET

Od [Stephen Molloy](https://github.com/StephenMolloy) a [Rick Anderson](https://twitter.com/RickAndMSFT)

Tvůrci konfigurace poskytují moderní a agilní mechanizmus pro aplikace ASP.NET k získání hodnot konfigurace z externích zdrojů.

Tvůrci konfigurace:

* Jsou k dispozici v .NET Framework 4.7.1 a novějším.
* Poskytněte flexibilní mechanizmus pro čtení hodnot konfigurace.
* Při přesunu do kontejneru a prostředí zaměřeného na Cloud se řeší některé základní požadavky aplikací.
* Dá se použít ke zlepšení ochrany konfiguračních dat vykreslováním ze zdrojů, které byly dřív nedostupné (například Azure Key Vault a proměnných prostředí) v konfiguračním systému .NET.

## <a name="keyvalue-configuration-builders"></a>Tvůrci konfigurace klíč/hodnota

Běžným scénářem, který mohou být zpracovány konfiguračními sestavami, je poskytnout základní mechanismus pro nahrazení klíč/hodnota pro konfigurační oddíly, které následují po vzorci klíč/hodnota. .NET Framework koncept ConfigurationBuilders není omezený na konkrétní konfigurační oddíly nebo vzory. Mnoho konfiguračních tvůrců v nástroji `Microsoft.Configuration.ConfigurationBuilders` ([GitHub](https://github.com/aspnet/MicrosoftConfigurationBuilders), [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)) ale funguje v rámci vzoru klíč/hodnota.

## <a name="keyvalue-configuration-builders-settings"></a>Nastavení tvůrců konfigurace klíč/hodnota

Následující nastavení platí pro všechna sestavení konfigurace klíč/hodnota v `Microsoft.Configuration.ConfigurationBuilders` .

### <a name="mode"></a>Mode

Tvůrci konfigurace používají externí zdroj informací o klíčích a hodnotách k naplnění vybraných prvků klíč/hodnota konfiguračního systému. Konkrétně `<appSettings/>` `<connectionStrings/>` oddíly a dostanou speciální zpracování od tvůrců konfigurace. Tvůrci pracují ve třech režimech:

* `Strict`– Výchozí režim. V tomto režimu nástroj Configuration Builder pracuje pouze s dobře známými konfiguračními oddíly orientovanými na klíč/hodnotu. `Strict`režim vytvoří výčet jednotlivých klíčů v části. Pokud je v externím zdroji nalezen shodný klíč:

   * Tvůrci konfigurace nahradí hodnotu ve výsledném oddílu konfigurace hodnotou z externího zdroje.
* `Greedy`– Tento režim je úzce spojený s `Strict` režimem. Místo toho, aby se omezily na klíče, které už existují v původní konfiguraci:

  * Tvůrci konfigurace přidají všechny páry klíč/hodnota z externího zdroje do výsledného konfiguračního oddílu.

* `Expand`– Funguje v nezpracovaném formátu XML před tím, než se analyzuje do objektu konfiguračního oddílu. Lze si představit jako rozšíření tokenů v řetězci. Jakákoli část nezpracovaného řetězce XML, který odpovídá vzoru, `${token}` je kandidátem pro rozšíření tokenu. Pokud se v externím zdroji nenajde žádná odpovídající hodnota, token se nemění. Tvůrci v tomto režimu nejsou omezeni pouze na `<appSettings/>` oddíly a `<connectionStrings/>` .

Následující kód z *web.config* umožňuje [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) v `Strict` režimu:

[!code-xml[Main](config-builder/MyConfigBuilders/WebDefault.config?name=snippet)]

Následující kód přečte `<appSettings/>` a `<connectionStrings/>` zobrazí se v předchozím souboru *web.config* :

[!code-csharp[Main](config-builder/MyConfigBuilders/About.aspx.cs)]

Předchozí kód nastaví hodnoty vlastností na:

* Hodnoty v souboru *web.config* , pokud klíče nejsou nastaveny v proměnných prostředí.
* Hodnoty proměnné prostředí, je-li nastavena.

Například `ServiceID` bude obsahovat:

* "Idslužby hodnota z web.config", pokud není nastavena proměnná prostředí `ServiceID` .
* Hodnota `ServiceID` proměnné prostředí, je-li nastavena.

Následující obrázek ukazuje `<appSettings/>` klíče/hodnoty z předchozí *web.config* sady souborů v editoru prostředí:

![Editor prostředí](config-builder/static/env.png)

Poznámka: Pokud chcete zobrazit změny v proměnných prostředí, možná budete muset aplikaci Visual Studio ukončit a restartovat.

### <a name="prefix-handling"></a>Zpracování předpon

Klíčové předpony můžou zjednodušit nastavení klíčů z těchto důvodů:

* Konfigurace .NET Framework je složitá a vnořená.
* Zdroje externích klíčů a hodnot jsou běžně základní a ploché podle povahy. Například proměnné prostředí nejsou vnořené.

K vložení obou z následujících přístupů do `<appSettings/>` `<connectionStrings/>` konfigurace prostřednictvím proměnných prostředí můžete použít tyto přístupy:

* S `EnvironmentConfigBuilder` ve výchozím `Strict` režimu a příslušnými názvy klíčů v konfiguračním souboru. Předchozí kód a kód přebírají tento přístup. Pomocí tohoto přístupu **nemůžete** mít v a i stejné pojmenované klíče `<appSettings/>` `<connectionStrings/>` .
* Použijte dva `EnvironmentConfigBuilder` typy v v `Greedy` režimu s jedinečnými předponami a `stripPrefix` . S tímto přístupem může aplikace číst `<appSettings/>` a `<connectionStrings/>` bez nutnosti aktualizovat konfigurační soubor. V další části [stripPrefix](#stripprefix)se dozvíte, jak to provést.
* Použijte dva `EnvironmentConfigBuilder` typy v v `Greedy` režimu s jedinečnými předponami. U tohoto přístupu nemůžete mít duplicitní názvy klíčů, protože názvy klíčů se musí lišit podle předpony.  Příklad:

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefix.config?name=snippet&highlight=11-99)]

S předchozím označením je možné použít stejný zdroj nestrukturovaného klíče nebo hodnoty k naplnění konfigurace dvou různých oddílů.

Následující obrázek ukazuje `<appSettings/>` `<connectionStrings/>` klíče a hodnoty z předchozí *web.config* sady souborů v editoru prostředí:

![Editor prostředí](config-builder/static/prefix.png)

Následující kód přečte `<appSettings/>` klíče a `<connectionStrings/>` hodnoty, které jsou obsaženy v předchozím *web.config* souboru:

[!code-csharp[Main](config-builder/MyConfigBuilders/Contact.aspx.cs?name=snippet)]

Předchozí kód nastaví hodnoty vlastností na:

* Hodnoty v souboru *web.config* , pokud klíče nejsou nastaveny v proměnných prostředí.
* Hodnoty proměnné prostředí, je-li nastavena.

Například pomocí předchozího souboru *web.config* , klíče/hodnoty v předchozí imagi editoru prostředí a předchozího kódu jsou nastaveny následující hodnoty:

|  Klíč              | Hodnota |
| ----------------- | ------------ |
|     AppSetting_ServiceID           | AppSetting_ServiceID z proměnných ENV|
|    AppSetting_default            | AppSetting_default hodnota z ENV |
|       ConnStr_default         | ConnStr_default Val ze ENV|

### <a name="stripprefix"></a>stripPrefix

`stripPrefix`: Boolean, výchozí hodnota `false` . 

Předchozí kód XML odděluje nastavení aplikace z připojovacích řetězců, ale vyžaduje, aby všechny klíče v souboru *web.config* používaly zadanou předponu. Například předpona `AppSetting` musí být přidána do `ServiceID` klíče ("AppSetting_ServiceID"). V nástroji se `stripPrefix` předpona nepoužívá v souboru *web.config* . Ve zdroji tvůrce konfigurace je vyžadována předpona (například v prostředí). Předpokládáme, že bude používat většina vývojářů `stripPrefix` .

Aplikace obvykle vycházejí z předpony. Následující *web.config* vyříznout předponu:

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefixStrip.config?name=snippet&highlight=14,19)]

V předchozím souboru *web.config* `default` klíč je v `<appSettings/>` a `<connectionStrings/>` .

Následující obrázek ukazuje `<appSettings/>` `<connectionStrings/>` klíče a hodnoty z předchozí *web.config* sady souborů v editoru prostředí:

![Editor prostředí](config-builder/static/prefix.png)

Následující kód přečte `<appSettings/>` klíče a `<connectionStrings/>` hodnoty, které jsou obsaženy v předchozím *web.config* souboru:

[!code-csharp[Main](config-builder/MyConfigBuilders/About2.aspx.cs?name=snippet)]

Předchozí kód nastaví hodnoty vlastností na:

* Hodnoty v souboru *web.config* , pokud klíče nejsou nastaveny v proměnných prostředí.
* Hodnoty proměnné prostředí, je-li nastavena.

Například pomocí předchozího souboru *web.config* , klíče/hodnoty v předchozí imagi editoru prostředí a předchozího kódu jsou nastaveny následující hodnoty:

|  Klíč              | Hodnota |
| ----------------- | ------------ |
|     Idslužby           | AppSetting_ServiceID z proměnných ENV|
|    default            | AppSetting_default hodnota z ENV |
|    default         | ConnStr_default Val ze ENV|

### <a name="tokenpattern"></a>tokenPattern

`tokenPattern`: Řetězec, výchozí hodnota`@"\$\{(\w+)\}"`

`Expand`Chování tvůrců prohledává nezpracovaný kód XML pro tokeny, které vypadají jako `${token}` . Hledání se provádí s výchozím regulárním výrazem `@"\$\{(\w+)\}"` . Sada znaků, které odpovídají, `\w` je větší než XML a mnoho zdrojů konfigurace povoluje. Použijte, `tokenPattern` Pokud `@"\$\{(\w+)\}"` název tokenu vyžaduje více znaků, než je vyžadováno.

`tokenPattern`Řetezce

* Umožňuje vývojářům změnit regulární výraz, který se používá pro odpovídající tokeny.
* Neprovádí se žádné ověření, abyste se ujistili, že se jedná o správný regulární výraz, který není bezpečný.
* Musí obsahovat skupinu zachycení. Celý regulární výraz se musí shodovat s celým tokenem. První zachycení musí být název tokenu, aby bylo možné vyhledat zdroj konfigurace.

## <a name="configuration-builders-in-microsoftconfigurationconfigurationbuilders"></a>Tvůrci konfigurace v Microsoft.Configuration.ConfigurationBuilders

### <a name="environmentconfigbuilder"></a>EnvironmentConfigBuilder

```xml
<add name="Environment"
    [mode|prefix|stripPrefix|tokenPattern] 
    type="Microsoft.Configuration.ConfigurationBuilders.EnvironmentConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Environment" />
```

[EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):

* Je nejjednodušší pro sestavovatele konfigurace.
* Přečte hodnoty z prostředí.
* Nemá žádné další možnosti konfigurace.
* `name`Hodnota atributu je libovolná.

**Poznámka:** V prostředí kontejneru Windows jsou proměnné nastavené v době běhu vloženy pouze do prostředí procesu EntryPoint. Aplikace, které běží jako služba nebo jiný než vstupní bod, nevezmou tyto proměnné, pokud nejsou jinak vloženy pomocí mechanismu v kontejneru. V [případě](https://github.com/Microsoft/iis-docker/pull/41) / kontejnerů založených na službě IIS[ASP.NET](https://github.com/Microsoft/aspnet-docker)je aktuální verze [ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41) v tuto dobu zpracovává pouze v rámci aplikace *DefaultAppPool* . Jiné varianty kontejneru založené na systému Windows můžou potřebovat vyvinout vlastní mechanizmy injektáže pro procesy, které nejsou typu EntryPoint.

### <a name="usersecretsconfigbuilder"></a>UserSecretsConfigBuilder

> [!WARNING]
> Nikdy neukládejte hesla, citlivé připojovací řetězce ani další citlivá data ve zdrojovém kódu. Provozní tajemství by se neměla používat pro vývoj nebo testování.

```xml
<add name="UserSecrets"
    [mode|prefix|stripPrefix|tokenPattern]
    (userSecretsId="{secret string, typically a GUID}" | userSecretsFile="~\secrets.file")
    [optional="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.UserSecrets" />
```

Tento nástroj Configuration Manager poskytuje funkci podobnou [ASP.NET Core správce tajných klíčů](/aspnet/core/security/app-secrets).

[UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/) se dá použít v projektech .NET Framework, ale musí se zadat soubor tajných klíčů. Alternativně můžete definovat `UserSecretsId` vlastnost v souboru projektu a vytvořit nezpracovaný soubor tajných klíčů ve správném umístění pro čtení. Chcete-li zachovat externí závislosti mimo váš projekt, tajný soubor je ve formátu XML. Formátování XML je podrobné informace o implementaci a formát by neměl spoléhat na. Pokud potřebujete sdílet *secrets.js* k souboru s projekty .NET Core, zvažte použití [SimpleJsonConfigBuilder](#simplejsonconfigbuilder). `SimpleJsonConfigBuilder`Formát pro .NET Core by měl být také považován za podrobnosti implementace, které se mohou změnit.

Konfigurační atributy pro `UserSecretsConfigBuilder` :

* `userSecretsId`– Jedná se o upřednostňovanou metodu pro identifikaci souboru tajných kódů XML. Funguje podobně jako rozhraní .NET Core, které používá `UserSecretsId` vlastnost projektu k uložení tohoto identifikátoru. Řetězec musí být jedinečný, nemusí se jednat o identifikátor GUID. Pomocí tohoto atributu se `UserSecretsConfigBuilder` podívejte do známého místního umístění ( `%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml` ) pro soubor tajných kódů, který patří k tomuto identifikátoru.
* `userSecretsFile`– Volitelný atribut určující soubor obsahující tajné klíče. `~`Znak lze použít na začátku pro odkaz na kořen aplikace. Buď je tento atribut, nebo `userSecretsId` atribut povinný. Pokud jsou zadány obě, `userSecretsFile` má přednost.
* `optional`: Boolean, výchozí hodnota `true` – zakáže výjimku, pokud nebyl nalezen soubor tajných klíčů. 
* `name`Hodnota atributu je libovolná.

Soubor tajných kódů má následující formát:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<root>
  <secrets ver="1.0">
    <secret name="secret key name" value="secret value" />
  </secrets>
</root>
```

### <a name="azurekeyvaultconfigbuilder"></a>AzureKeyVaultConfigBuilder

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

[AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/) čte hodnoty uložené v [Azure Key Vault](/azure/key-vault/key-vault-whatis).

`vaultName`je vyžadováno (buď název trezoru, nebo identifikátor URI k trezoru). Ostatní atributy umožňují řízení, ke kterému trezoru se má připojit, ale jsou nezbytné pouze v případě, že aplikace neběží v prostředí, které pracuje s nástrojem `Microsoft.Azure.Services.AppAuthentication` . Knihovna ověřování služeb Azure slouží k automatickému výběru informací o připojení z prováděcího prostředí, pokud je to možné. K automatickému výběru informací o připojení můžete potlačit zadáním připojovacího řetězce.

* `vaultName`– Vyžaduje se `uri` , pokud není zadaný. Určuje název trezoru v předplatném Azure, ze kterého se mají číst páry klíč/hodnota.
* `connectionString`– Připojovací řetězec, který je použitelný pro [AzureServiceTokenProvider](https://docs.microsoft.com/azure/key-vault/service-to-service-authentication#connection-string-support)
* `uri`– Připojí se k jiným poskytovatelům Key Vault se zadanou `uri` hodnotou. Pokud není zadaný, Azure ( `vaultName` ) je poskytovatelem trezoru.
* `version`-Azure Key Vault poskytuje funkce správy verzí tajných kódů. `version`Je-li parametr zadán, tvůrce načte pouze tajné kódy, které odpovídají této verzi.
* `preloadSecretNames`– Ve výchozím nastavení tento tvůrce dotazuje **všechny** názvy klíčů v trezoru klíčů při inicializaci. Chcete-li zabránit čtení všech hodnot klíče, nastavte tento atribut na `false` . Nastavením tohoto parametru `false` přečtete tajné kódy po jednom. Čtení tajných kódů po jednom může být užitečné, pokud trezor umožňuje přístup "získat", ale ne "seznam". **Poznámka:** Při použití `Greedy` režimu `preloadSecretNames` musí být `true` (výchozí hodnota).

### <a name="keyperfileconfigbuilder"></a>KeyPerFileConfigBuilder

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

[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) je základní nástroj Configuration Builder, který jako zdroj hodnot používá soubory adresáře. Název souboru je klíč a obsah je hodnota. Tento nástroj Configuration Builder může být užitečný při spuštění v prostředí orchestrace kontejnerů. Systémy, jako jsou Docker Swarm a Kubernetes, poskytují `secrets` své orchestraci kontejnerů Windows v tomto způsobu, jakým je tento klíč založený na souboru.

Podrobnosti atributu:

* `directoryPath`Požadovanou. Určuje cestu pro hledání hodnot. Docker for Windows tajné klíče jsou ve výchozím nastavení ukládány do adresáře *C:\ProgramData\Docker\secrets* .
* `ignorePrefix`-Jsou vyloučeny soubory, které začínají touto předponou. Výchozí hodnota je ignore.
* `keyDelimiter`-Výchozí hodnota je `null` . Je-li tento parametr zadán, projde nástroj Configuration Builder více úrovní adresáře a sestaví názvy klíčů pomocí tohoto oddělovače. Pokud je tato hodnota `null` , nástroj Configuration Builder se vyhledá jenom na nejvyšší úrovni adresáře.
* `optional`-Výchozí hodnota je `false` . Určuje, zda má nástroj Configuration Builder způsobit chyby v případě, že zdrojový adresář neexistuje.

### <a name="simplejsonconfigbuilder"></a>SimpleJsonConfigBuilder

> [!WARNING]
> Nikdy neukládejte hesla, citlivé připojovací řetězce ani další citlivá data ve zdrojovém kódu. Provozní tajemství by se neměla používat pro vývoj nebo testování.

```xml
<add name="SimpleJson"
    [mode|prefix|stripPrefix|tokenPattern]
    jsonFile="~\config.json"
    [optional="true"]
    [jsonMode="(Flat|Sectional)"]
    type="Microsoft.Configuration.ConfigurationBuilders.SimpleJsonConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Json" />
```

Projekty .NET Core často používají soubory JSON pro konfiguraci. Tvůrce [SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) umožňuje používat v .NET Framework soubory JSON pro .NET Core. Tento nástroj Configuration Builder poskytuje základní mapování ze zdroje nestrukturovaných klíčů a hodnot do konkrétních oblastí s klíči a hodnotami konfigurace .NET Framework. Tento nástroj Configuration Builder **neposkytuje hierarchické** konfigurace. Soubor zálohy JSON je podobný slovníku, nikoli složitému hierarchickému objektu. Můžete použít hierarchický soubor s více úrovněmi. Tento poskytovatel `flatten` s hloubkou připojí název vlastnosti na každé úrovni pomocí `:` oddělovače.

Podrobnosti atributu:

* `jsonFile`Požadovanou. Určuje soubor JSON, ze kterého se má číst. `~`Znak lze použít na začátku pro odkaz na kořen aplikace.
* `optional`– Logická hodnota, výchozí hodnota je `true` . Zabraňuje vyvolání výjimek, pokud nelze najít soubor JSON.
* `jsonMode` - `[Flat|Sectional]`. `Flat` je výchozí možnost. `jsonMode`V případě je `Flat` soubor JSON jedním zdrojem nestrukturovaných klíč/hodnota. `EnvironmentConfigBuilder`A `AzureKeyVaultConfigBuilder` jsou také jedním nestrukturovaným zdrojem klíč/hodnota. Když `SimpleJsonConfigBuilder` je nakonfigurovaný v `Sectional` režimu:

  * Soubor JSON je koncepčně rozdělený přímo na nejvyšší úrovni do více slovníků.
  * Každý ze slovníků je použit pouze pro konfigurační oddíl, který odpovídá názvu vlastnosti nejvyšší úrovně, který je k nim připojen. Příklad:

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

## <a name="configuration-builders-order"></a>Pořadí sestavení konfigurace

Prohlédněte si [ConfigurationBuilders pořadí spouštění](https://github.com/aspnet/MicrosoftConfigurationBuilders/blob/master/README.md#configurationbuilders-order-of-execution) v úložišti GitHub [/MicrosoftConfigurationBuilders](https://github.com/aspnet/MicrosoftConfigurationBuilders) .

## <a name="implementing-a-custom-keyvalue-configuration-builder"></a>Implementace vlastního tvůrce konfigurace klíčů a hodnot

Pokud konfigurační tvůrci nevyhovují vašim potřebám, můžete napsat vlastní. `KeyValueConfigBuilder`Základní třída zpracovává substituční režimy a většinu nejdůležitějších otázek. Implementující projekt vyžaduje jenom:

* Dědí ze základní třídy a implementuje základní zdroj párů klíč/hodnota prostřednictvím `GetValue` a `GetAllValues` :
* Přidejte do projektu [Microsoft.Configuration.ConfigurationBuilders. Base](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) .

[!code-csharp[Main](config-builder/MyConfigBuilders/MyCustomConfigBuilder.cs)]

`KeyValueConfigBuilder`Základní třída poskytuje mnoho práce a konzistentní chování napříč sestavami konfigurace klíčů a hodnot.

## <a name="additional-resources"></a>Další zdroje

* [Úložiště GitHubu pro sestavovatele konfigurace](https://github.com/aspnet/MicrosoftConfigurationBuilders)
* [Ověřování služba-služba pro Azure Key Vault pomocí .NET](/azure/key-vault/service-to-service-authentication#connection-string-support)
