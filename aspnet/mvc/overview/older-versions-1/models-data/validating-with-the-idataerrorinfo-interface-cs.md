---
uid: mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-cs
title: Ověřování v rozhraní IDataErrorInfo (C#) | Dokumentace Microsoftu
author: StephenWalther
description: Stephen Walther se dozvíte, jak zobrazit chybové zprávy ověření na vlastních implementací rozhraní IDataErrorInfo v třídě modelu.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 4733b9f1-9999-48fb-8b73-6038fbcc5ecb
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: 3e1399d17840a2f5301349cb91deb07b0cc34363
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59421976"
---
# <a name="validating-with-the-idataerrorinfo-interface-c"></a>Ověřování v rozhraní IDataErrorInfo (C#)

podle [Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther se dozvíte, jak zobrazit chybové zprávy ověření na vlastních implementací rozhraní IDataErrorInfo v třídě modelu.


Cílem tohoto kurzu je vysvětlit jedním z přístupů k provedení ověření v aplikaci ASP.NET MVC. Zjistíte, jak zabránit odeslání formuláře HTML bez zadání hodnot požadovaných polí. V tomto kurzu se dozvíte, jak provádět ověření pomocí rozhraní IErrorDataInfo.

## <a name="assumptions"></a>Předpoklady

V tomto kurzu použiju MoviesDB databáze a tabulky databáze filmů. Tato tabulka obsahuje následující sloupce:

<a id="0.5_table01"></a>


| **Název sloupce** | **Datový typ** | **Povolit hodnoty Null** |
| --- | --- | --- |
| ID | Int | False |
| Název | Nvarchar(100) | False |
| Ředitel | Nvarchar(100) | False |
| DateReleased | DateTime | False |


V tomto kurzu pomocí Microsoft Entity Framework vytvořit Moje databáze třídy modelu. Třída film vygenerovaným rozhraním Entity Framework se zobrazí na obrázku 1.


[![Video entity](validating-with-the-idataerrorinfo-interface-cs/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image1.png)

**Obrázek 01**: Movie entity ([kliknutím ji zobrazíte obrázek v plné velikosti](validating-with-the-idataerrorinfo-interface-cs/_static/image2.png))


> [!NOTE] 
> 
> Další informace o použití rozhraní Entity Framework pro generování tříd modelu vaší databáze najdete v tématu Moje kurz s názvem vytváření tříd modelu s použitím rozhraní Entity Framework.


## <a name="the-controller-class"></a>Třída Kontroleru

Používáme kontroler Home na filmy seznamu a vytvořit nové filmy. Kód pro tuto třídu je obsažen v informacích 1.

**Výpis 1 - Controllers\HomeController.cs**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample1.cs)]

Třída kontroleru Domovská stránka v informacích 1 obsahuje dvě Create() akce. První akci zobrazí formulář HTML pro vytvoření nové video. Druhou akci Create() provádí skutečné vložit tento nový film do databáze. Druhou akci Create() je voláno, když se odešle formulář zobrazí první Create() akcí na server.

Všimněte si, že druhou akci Create() obsahuje následující řádky kódu:

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample2.cs)]

Vlastnost IsValid vrátí hodnotu false, když dojde k chybě ověřování. V takovém případě se zobrazí znovu vytvořit zobrazení, která obsahuje formulář HTML pro vytváření videa.

## <a name="creating-a-partial-class"></a>Vytvoření částečné třídy

Třída Video je vygenerovaným rozhraním Entity Framework. Pokud rozbalte soubor MoviesDBModel.edmx v okně Průzkumník řešení a otevřete soubor MoviesDBModel.Designer.cs v editoru kódu vidíte kód pro třídu Movie (viz obrázek 2).


[![Kód pro entitu Movie](validating-with-the-idataerrorinfo-interface-cs/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image3.png)

**Obrázek 02**: Kód pro entitu Movie ([kliknutím ji zobrazíte obrázek v plné velikosti](validating-with-the-idataerrorinfo-interface-cs/_static/image4.png))


Třída Video je částečnou třídu. To znamená, že můžeme přidat jiné částečné třídy se stejným názvem k rozšíření funkčnosti film třídy. Přidáme náš logiku ověřování novou třídu.

Přidáte třídu v informacích 2 do složky modely.

**Výpis 2 - Models\Movie.cs**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample3.cs)]

Všimněte si, že třída v informacích 2 zahrnuje *částečné* modifikátor. Jakékoliv metody nebo vlastnosti, které přidáte do této třídy, se stanou součástí třídy film vygenerovaným rozhraním Entity Framework.

## <a name="adding-onchanging-and-onchanged-partial-methods"></a>Přidání OnChanging a OnChanged částečné metody

Když Entity Frameworku vygeneruje třídu entity, Entity Framework přidá částečné metody do třídy automaticky. Entity Framework generuje OnChanging a OnChanged částečné metody, které odpovídají každá vlastnost třídy.

V případě třídy film Entity Framework vytvoří následující metody:

- OnIdChanging
- OnIdChanged
- OnTitleChanging
- OnTitleChanged
- OnDirectorChanging
- OnDirectorChanged
- OnDateReleasedChanging
- OnDateReleasedChanged

Před změnou odpovídající vlastnosti je volána metoda OnChanging vpravo. Po změně vlastnosti je volána metoda OnChanged vpravo.

Můžete využít výhod těchto částečné metody třídy film přidat logiku ověřování. Aktualizace třídy filmu v informacích 3 ověřuje, že nadpis a ředitel pro vlastnosti se přiřazují neprázdných hodnot.

> [!NOTE] 
> 
> Částečná metoda je metoda definovaná ve třídě, není nutná pro implementaci. Pokud není implementovat částečnou metodu kompilátor odebere podpis metody a všechny volání metody tady nejsou žádné běhové náklady spojené s částečnou metodu. V editoru Visual Studio Code, můžete přidat částečná metoda zadáním klíčového slova *částečné* následovaný mezerami, chcete-li zobrazit seznam částečných zobrazení k implementaci.


**Výpis 3 - Models\Movie.cs**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample4.cs)]

Například pokud se pokusíte přiřadit vlastnosti název prázdný řetězec, chybovou zprávu přiřadí se mu na slovník s názvem \_chyby.

V tomto okamžiku nic ve skutečnosti se stane, když přiřadíte prázdný řetězec pro vlastnost názvu a chyba se přidá do soukromého \_pole chyby. Musíme implementovat v rozhraní IDataErrorInfo umožní vystavit tyto chyby ověření do rozhraní ASP.NET MVC.

## <a name="implementing-the-idataerrorinfo-interface"></a>Implementace rozhraní IDataErrorInfo

V rozhraní IDataErrorInfo byl součástí rozhraní .NET framework od první verze. Toto rozhraní je velmi jednoduché rozhraní:

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample5.cs)]

Pokud třída implementuje rozhraní IDataErrorInfo, rozhraní ASP.NET MVC bude používat toto rozhraní, při vytváření instance třídy. Například kontroler Home Create() akce přijímá instanci třídy filmu:

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample6.cs)]

Architektura ASP.NET MVC vytvoří instanci film předán Create() akce pomocí vazače modelu (DefaultModelBinder). Vazač modelu zodpovídá za vytvoření instance objektu film navázáním pole formuláře HTML na instanci objektu video.

DefaultModelBinder zjišťuje, zda třída implementuje rozhraní IDataErrorInfo. Pokud třída implementuje toto rozhraní vazače modelu vyvolá IDataErrorInfo.this indexeru pro každou vlastnost třídy. Pokud indexeru vrátí chybovou zprávu přidá vazač modelu tato chybová zpráva pro modelování stav automaticky.

DefaultModelBinder také kontroluje IDataErrorInfo.Error vlastnost. Tato vlastnost je určena k reprezentaci chyby ověřování podle jiné vlastnosti přidružené k třídě. Můžete například chtít vynutit ověřovací pravidlo, které závisí na hodnotách více vlastností třídy Video. V takovém případě by vrátit chybu ověření z vlastnosti chyby.

Aktualizované třídy filmu v informacích 4 implementuje rozhraní IDataErrorInfo.

**Část 4 – Models\Movie.cs (implementuje IDataErrorInfo)**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample7.cs)]

V informacích 4 kontroluje vlastnost indexeru \_předaný kolekce chyb, pokud obsahuje klíč, který odpovídá názvu vlastnosti indexeru. Pokud se nezobrazí žádná chyba ověření přidružený k vlastnosti je vrácen prázdný řetězec.

Není nutné upravovat kontroler Home žádným způsobem pomocí upravené třídy film. Stránky zobrazené na obrázku 3 znázorňuje, co se stane, když je zadána žádná hodnota pro název nebo ředitel pole formuláře.


[![Automatické vytváření metody akce](validating-with-the-idataerrorinfo-interface-cs/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image5.png)

**Obrázek 03**: Formulář s chybějící hodnoty ([kliknutím ji zobrazíte obrázek v plné velikosti](validating-with-the-idataerrorinfo-interface-cs/_static/image6.png))


Všimněte si, že hodnota DateReleased proběhne automaticky. Protože vlastnost DateReleased nepřijímá hodnoty NULL, DefaultModelBinder Chyba ověřování pro tuto vlastnost automaticky při vygeneruje nemá hodnotu. Pokud chcete upravit chybové zprávy pro vlastnost DateReleased budete muset vytvořit vlastní vazač modelu.

## <a name="summary"></a>Souhrn

V tomto kurzu jste zjistili, jak používat rozhraní IDataErrorInfo ke generování chybových zpráv ověření. Nejprve jsme vytvořili částečné třídy film, který rozšiřuje funkce částečné třídy film vygenerovaným rozhraním Entity Framework. Dále jsme přidali logiku ověřování k film třídy OnTitleChanging() OnDirectorChanging() částečné metody a. Nakonec jsme implementovali v rozhraní IDataErrorInfo aby bylo možné zveřejnit tyto zprávy ověření na rozhraní ASP.NET MVC.

> [!div class="step-by-step"]
> [Předchozí](performing-simple-validation-cs.md)
> [další](validating-with-a-service-layer-cs.md)
