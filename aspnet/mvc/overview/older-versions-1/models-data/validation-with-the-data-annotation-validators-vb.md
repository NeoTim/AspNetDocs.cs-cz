---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
title: Ověření pomocí validátorů anotace dat (VB) | Dokumenty společnosti Microsoft
author: rick-anderson
description: Využijte binder modelu poznámky k ověření v rámci aplikace ASP.NET MVC. Naučte se používat různé typy validátoru...
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 0d23ff2b-f2ec-434a-be3b-1180beeccba3
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
msc.type: authoredcontent
ms.openlocfilehash: cabdf6dab9e5de53a45adcf126705533fca02de7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542635"
---
# <a name="validation-with-the-data-annotation-validators-vb"></a>Ověřování validátory datových poznámek (VB)

podle [společnosti Microsoft](https://github.com/microsoft)

> Využijte binder modelu poznámky k ověření v rámci aplikace ASP.NET MVC. Naučte se používat různé typy atributů validátoru a pracovat s nimi v microsoft entity frameworku.

V tomto kurzu se dozvíte, jak používat validátory anotace dat k ověření v aplikaci ASP.NET MVC. Výhodou použití validátorů anotace dat je, že umožňují provádět ověření jednoduše přidáním jednoho nebo více atributů – například atributu Required nebo StringLength – do vlastnosti třídy.

Před použitím validátorů anotace dat je nutné stáhnout datové poznámky model pořadače. Ukázku datových anotací model binder si můžete stáhnout z webových stránek CodePlex kliknutím [zde](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471).

Je důležité si uvědomit, že data poznámky model binder není oficiální součástí rozhraní Microsoft ASP.NET MVC. Přestože data poznámky model pořadač byl vytvořen týmem Microsoft ASP.NET MVC, Společnost Microsoft nenabízí oficiální podporu produktu pro data poznámky model pořadač popsané a používané v tomto kurzu.

## <a name="using-the-data-annotation-model-binder"></a>Použití pořadače modelu poznámky dat

Chcete-li použít pořadač modelu datových anotací v aplikaci mvc ASP.NET, musíte nejprve přidat odkaz na sestavení Microsoft.Web.Mvc.DataAnnotations.dll a sestavení System.ComponentModel.DataAnnotations.dll. Vyberte volbu nabídky **Projekt, Přidat odkaz**. Dále klikněte na kartu **Procházet** a vyhledejte umístění, kde jste stáhli (a rozbalili) ukázku datové poznámky model binder (viz **obrázek 1).**

[![](validation-with-the-data-annotation-validators-vb/_static/image2.png)](validation-with-the-data-annotation-validators-vb/_static/image1.png)

**Obrázek 1**: Přidání odkazu na pořadač modelu datových poznámk[(Kliknutím zobrazíte obrázek v plné velikosti)](validation-with-the-data-annotation-validators-vb/_static/image3.png)

Vyberte sestavení Microsoft.Web.Mvc.DataAnnotations.dll a sestavení System.ComponentModel.DataAnnotations.dll a klepněte na tlačítko **OK.**

Sestavení System.ComponentModel.DataAnnotations.dll, které je součástí aktualizace .NET Framework Service Pack 1 s vazbami modelu datových anotací, nelze použít. Je nutné použít verzi sestavení System.ComponentModel.DataAnnotations.dll, která je součástí ukázkového stažení modelu datových poznámk.

Nakonec je třeba zaregistrovat DataAnnotations Model Binder v souboru Global.asax. Přidejte následující řádek kódu\_do obslužné rutiny události Start() aplikace tak, aby metoda Start() aplikace\_vypadala takto:

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample1.vb)]

Tento řádek kódu registruje DataAnnotationsModelBinder jako výchozí pořadač modelu pro celou ASP.NET aplikaci MVC.

## <a name="using-the-data-annotation-validator-attributes"></a>Použití atributů validátoru anotace dat

Při použití data poznámky model binder, použijete atributy validátoru k provedení ověření. Obor názvů System.ComponentModel.DataAnnotations obsahuje následující atributy validátoru:

- Rozsah – umožňuje ověřit, zda hodnota vlastnosti spadá mezi zadaný rozsah hodnot.
- RegularExpression – Umožňuje ověřit, zda hodnota vlastnosti odpovídá zadanému vzoru regulárního výrazu.
- Povinné – Umožňuje označit vlastnost podle potřeby.
- StringLength – Umožňuje zadat maximální délku vlastnosti řetězce.
- Ověření – základní třída pro všechny atributy validátoru.

> [!NOTE] 
> 
> Pokud vaše potřeby ověření nejsou splněny některé standardní validátory pak máte vždy možnost vytvořit vlastní atribut validátoru deducem nový atribut validátoru ze základního atributu Validation.

Třída Product v **seznamu 1** ukazuje, jak používat tyto atributy validátoru. Vlastnosti Název, Popis a UnitPrice jsou označeny podle potřeby. Vlastnost Name musí mít délku řetězce, která je menší než 10 znaků. Nakonec UnitPrice vlastnost musí odpovídat vzor regulárního výrazu, který představuje částku měny.

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample2.vb)]

**Výpis 1**: Modely\Product.vb

Třída Product ukazuje, jak použít jeden další atribut: atribut DisplayName. Atribut DisplayName umožňuje změnit název vlastnosti, když je vlastnost zobrazena v chybové zprávě. Namísto zobrazení chybové zprávy "Pole UnitPrice je povinné" můžete zobrazit chybovou zprávu "Pole Cena je povinné".

> [!NOTE] 
> 
> Pokud chcete zcela přizpůsobit chybovou zprávu zobrazenou validátorem, můžete přiřadit vlastní chybovou zprávu vlastnosti ErrorMessage validátoru takto:`<Required(ErrorMessage:="This field needs a value!")>`

Třídu Produkt můžete použít ve **výpisu 1** s akcí Vytvořit() kontrolora v **výpisu 2**. Tato akce kontroler znovu zobrazí vytvořit pohled, když stav modelu obsahuje nějaké chyby.

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample3.vb)]

**Výpis 2**: Řadiče\ProductController.vb

Nakonec můžete vytvořit zobrazení v **výpisu 3** klepnutím pravým tlačítkem myši na akci Vytvořit() a výběrem možnosti nabídky **Přidat zobrazení**. Vytvořte zobrazení silného typu s třídou Product jako třídou modelu. V rozevíracím seznamu obsahu zobrazení vyberte **Vytvořit** (viz **obrázek 2).**

[![](validation-with-the-data-annotation-validators-vb/_static/image5.png)](validation-with-the-data-annotation-validators-vb/_static/image4.png)

**Obrázek 2**: Přidání zobrazení vytvoření

[!code-aspx[Main](validation-with-the-data-annotation-validators-vb/samples/sample4.aspx)]

**Výpis 3**: Zobrazení\Produkt\Vytvořit.aspx

> [!NOTE] 
> 
> Odeberte pole Id z formuláře Vytvořit generovaného možností nabídky **Přidat zobrazení.** Vzhledem k tomu, že pole Id odpovídá sloupci Identita, nechcete uživatelům povolit zadání hodnoty pro toto pole.

Pokud odešlete formulář pro vytvoření produktu a nezadáte hodnoty pro požadovaná pole, zobrazí se chybové zprávy ověření na **obrázku 3.**

[![](validation-with-the-data-annotation-validators-vb/_static/image7.png)](validation-with-the-data-annotation-validators-vb/_static/image6.png)

**Obrázek 3**: Chybějící povinná pole

Pokud zadáte neplatnou částku měny, zobrazí se chybová zpráva **na obrázku 4.**

[![](validation-with-the-data-annotation-validators-vb/_static/image9.png)](validation-with-the-data-annotation-validators-vb/_static/image8.png)

**Obrázek 4**: Neplatná částka měny

## <a name="using-data-annotation-validators-with-the-entity-framework"></a>Použití validátorů anotace dat s rámcem entity

Pokud používáte Microsoft Entity Framework ke generování tříd datového modelu, pak nelze použít atributy validátoru přímo na vaše třídy. Vzhledem k tomu, že Návrhář rozhraní entity generuje třídy modelu, všechny změny, které provedete ve třídách modelu, budou přepsány při příštím provádění změn v návrháři.

Pokud chcete použít validátory s třídami generovanými entity framework pak je třeba vytvořit meta datové třídy. Validátory použijete na třídu metadat meta namísto použití validátorů na skutečnou třídu.

Představte si například, že jste vytvořili třídu Movie pomocí entity Framework (viz **obrázek 5).** Představte si, kromě toho, že chcete, aby název filmu a ředitel vlastnosti požadované vlastnosti. V takovém případě můžete vytvořit třídu částečné třídy a meta datové třídy v **výpisu 4**.

[![](validation-with-the-data-annotation-validators-vb/_static/image11.png)](validation-with-the-data-annotation-validators-vb/_static/image10.png)

**Obrázek 5**: Třída filmu generovaná rozhraním Entity Framework

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample5.vb)]

**Výpis 4**: Modely\Movie.vb

Soubor v **seznamu 4** obsahuje dvě třídy s názvem Film a MovieMetaData. Třída Movie je částečná třída. Odpovídá částečné třídy generované entity framework, který je obsažen v souboru DataModel.Designer.vb.

V současné době rozhraní .NET framework nepodporuje částečné vlastnosti. Proto neexistuje žádný způsob, jak použít atributy validátoru na vlastnosti třídy Movie definované v souboru DataModel.Designer.vb použitím atributů validátoru na vlastnosti třídy Movie definované v souboru v **seznamu 4**.

Všimněte si, že movie částečná třída je zdobena MetadataType atribut, který odkazuje na MovieMetaData třídy. Třída MovieMetaData obsahuje vlastnosti proxy vlastností třídy Movie.

Atributy validátoru jsou použity na vlastnosti třídy MovieMetaData. Vlastnosti Title, Director a DateReleased jsou označeny jako požadované vlastnosti. Vlastnost Director musí být přiřazen řetězec, který obsahuje méně než 5 znaků. Nakonec displayname atribut je použit a DateReleased vlastnost zobrazit chybovou zprávu, jako je "Datum Vydáno pole je požadováno." místo chyby "Pole DateReleased je povinné."

> [!NOTE] 
> 
> Všimněte si, že proxy vlastnosti ve třídě MovieMetaData nemusí představovat stejné typy jako odpovídající vlastnosti ve třídě Movie. Například Director Vlastnost je vlastnost řetězce ve třídě Movie a vlastnost objektu ve třídě MovieMetaData.

Stránka na **obrázku 6** znázorňuje chybové zprávy vrácené při zadávání neplatných hodnot vlastností filmu.

[![](validation-with-the-data-annotation-validators-vb/_static/image13.png)](validation-with-the-data-annotation-validators-vb/_static/image12.png)

**Obrázek 6**: Použití validátorů s rozhraním Entity Framework[(Klepnutím zobrazíte obrázek v plné velikosti)](validation-with-the-data-annotation-validators-vb/_static/image14.png)

## <a name="summary"></a>Souhrn

V tomto kurzu jste se naučili, jak využít data poznámky model binder k provedení ověření v rámci ASP.NET aplikace MVC. Jste se naučili používat různé typy atributů validátoru, jako jsou povinné a StringLength atributy. Také jste se naučili používat tyto atributy při práci s rozhraním Microsoft Entity Framework.

> [!div class="step-by-step"]
> [Předchozí](validating-with-a-service-layer-vb.md)
