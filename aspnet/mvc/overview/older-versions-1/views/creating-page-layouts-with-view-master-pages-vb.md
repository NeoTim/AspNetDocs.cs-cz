---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
title: Vytváření rozložení stránek pomocí stránek předlohy zobrazení (VB) | Dokumenty společnosti Microsoft
author: rick-anderson
description: V tomto kurzu se dozvíte, jak vytvořit společné rozložení stránky pro více stránek v aplikaci s využitím zobrazení stránek předlohy. Můžete použít...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: d34f90a1-6de3-482a-a326-f87fdcbaaaff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 37b8d858c72357ebbe51458f76511a9672b01b4d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542492"
---
# <a name="creating-page-layouts-with-view-master-pages-vb"></a>Vytvoření rozložení stránek pomocí stránek předlohy pro zobrazení (VB)

podle [společnosti Microsoft](https://github.com/microsoft)

[Stáhnout PDF](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_VB.pdf)

> V tomto kurzu se dozvíte, jak vytvořit společné rozložení stránky pro více stránek v aplikaci s využitím zobrazení stránek předlohy. Pomocí vzorové stránky zobrazení můžete například definovat rozložení stránky se dvěma sloupci a použít rozložení se dvěma sloupci pro všechny stránky ve webové aplikaci.

## <a name="creating-page-layouts-with-view-master-pages"></a>Vytváření rozložení stránek pomocí stránek předlohy zobrazení

V tomto kurzu se dozvíte, jak vytvořit společné rozložení stránky pro více stránek v aplikaci s využitím zobrazení stránek předlohy. Pomocí vzorové stránky zobrazení můžete například definovat rozložení stránky se dvěma sloupci a použít rozložení se dvěma sloupci pro všechny stránky ve webové aplikaci.

Můžete také využít výhod vzorových stránek zobrazení ke sdílení společného obsahu na více stránkách aplikace. Na příklad můžete umístit logo webu, navigační odkazy a bannerové reklamy na stránku předlohy zobrazení. Tímto způsobem by každá stránka ve vaší aplikaci automaticky zobrazovala tento obsah.

V tomto kurzu se dozvíte, jak vytvořit novou stránku předlohy zobrazení a vytvořit novou stránku obsahu zobrazení na základě stránky předlohy.

### <a name="creating-a-view-master-page"></a>Vytvoření stránky předlohy zobrazení

Začněme vytvořením stránky předlohy zobrazení, která definuje rozložení se dvěma sloupci. Novou stránku předlohy zobrazení přidáte do projektu MVC tak, že kliknete pravým tlačítkem myši na složku Zobrazení\Sdíleno, vyberete možnost Nabídky **Přidat, Nová položka**a vyberete šablonu předlohy předlohy předlohy zobrazení MVC (viz obrázek 1).

[![Přidání stránky předlohy zobrazení](creating-page-layouts-with-view-master-pages-vb/_static/image2.png)](creating-page-layouts-with-view-master-pages-vb/_static/image1.png)

**Obrázek 01**: Přidání stránky předlohy zobrazení[(Kliknutím zobrazíte obrázek v plné velikosti)](creating-page-layouts-with-view-master-pages-vb/_static/image3.png)

V aplikaci můžete vytvořit více než jednu stránku předlohy zobrazení. Každá stránka předlohy zobrazení může definovat jiné rozložení stránky. Můžete například chtít, aby určité stránky měly rozložení se dvěma sloupci a jiné stránky měly rozložení se třemi sloupci.

Stránka předlohy zobrazení vypadá velmi podobně jako standardní ASP.NET zobrazení MVC. Na rozdíl od normálního zobrazení však stránka `<asp:ContentPlaceHolder>` předlohy zobrazení obsahuje jednu nebo více značek. Značky `<contentplaceholder>` se používají k označení oblastí stránky předlohy, které lze přepsat na jednotlivé stránce obsahu.

Například stránka předlohy zobrazení v seznamu 1 definuje rozložení se dvěma sloupci. Obsahuje dvě `<contentplaceholder>` značky. Jeden `<ContentPlaceHolder>` pro každý sloupec.

**Výpis 1 –`Views\Shared\Site.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample1.aspx)]

Text stránky předlohy zobrazení v `<div>` seznamu 1 obsahuje dvě značky, které odpovídají dvěma sloupcům. Třída sloupce Šablona stylů Kaskádové `<div>` se použije na obě značky. Tato třída je definována v šabloně stylů deklarované v horní části stránky předlohy. Přepnutím do návrhového zobrazení můžete zobrazit náhled, jak bude stránka předlohy zobrazení vykreslena. Klikněte na kartu Návrh v levém dolním rohu editoru zdrojového kódu (viz obrázek 2).

[![Náhled stránky předlohy v návrháři](creating-page-layouts-with-view-master-pages-vb/_static/image5.png)](creating-page-layouts-with-view-master-pages-vb/_static/image4.png)

**Obrázek 02**: Náhled stránky předlohy v návrháři[(Klepnutím zobrazíte obrázek v plné velikosti)](creating-page-layouts-with-view-master-pages-vb/_static/image6.png)

### <a name="creating-a-view-content-page"></a>Vytvoření stránky obsahu zobrazení

Po vytvoření stránky předlohy zobrazení můžete vytvořit jednu nebo více stránek obsahu zobrazení na základě stránky předlohy zobrazení. Stránku obsahu zobrazení indexu pro domácí řadič můžete například vytvořit tak, že kliknete pravým tlačítkem myši na složku Zobrazení\Domů, vyberete **přidat, novou položku**, vyberete **šablonu Stránky obsahu zobrazení MVC,** zadáte název Index.aspx a kliknete na tlačítko Přidat (viz obrázek 3).

[![Přidání stránky obsahu zobrazení](creating-page-layouts-with-view-master-pages-vb/_static/image8.png)](creating-page-layouts-with-view-master-pages-vb/_static/image7.png)

**Obrázek 03**: Přidání stránky obsahu zobrazení[(Kliknutím zobrazíte obrázek v plné velikosti)](creating-page-layouts-with-view-master-pages-vb/_static/image9.png)

Po klepnutí na tlačítko Přidat se zobrazí nový dialog, který umožňuje vybrat stránku předlohy zobrazení, kterou chcete přidružit ke stránce obsahu zobrazení (viz obrázek 4). Můžete přejít na stránku předlohy zobrazení Site.master, kterou jsme vytvořili v předchozí části.

[![Výběr stránky předlohy](creating-page-layouts-with-view-master-pages-vb/_static/image11.png)](creating-page-layouts-with-view-master-pages-vb/_static/image10.png)

**Obrázek 04**: Výběr stránky předlohy[(Kliknutím zobrazíte obrázek v plné velikosti)](creating-page-layouts-with-view-master-pages-vb/_static/image12.png)

Po vytvoření nové stránky obsahu zobrazení založené na vzorové stránce Site.master získáte soubor v seznamu 2.

**Výpis 2 –`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample2.aspx)]

Všimněte si, `<asp:Content>` že toto zobrazení obsahuje `<asp:ContentPlaceHolder>` značku, která odpovídá každé značky na stránce předlohy zobrazení. Každá `<asp:Content>` značka obsahuje atribut ContentPlaceHolderID, `<asp:ContentPlaceHolder>` který odkazuje na konkrétní, který přepíše.

Všimněte si dále, že stránka zobrazení obsahu v výpisu 2 neobsahuje žádnou z běžných značek HTML pro otevírání a zavírání. Například neobsahuje otevírání a `<html>` zavírání nebo `<head>` značky. Všechny běžné otevírací a uzavírací značky jsou obsaženy na stránce předlohy zobrazení.

Veškerý obsah, který chcete zobrazit na stránce obsahu `<asp:Content>` zobrazení, musí být umístěn do značky. Pokud umístíte jakýkoli obsah HTML nebo jiný obsah mimo tyto značky, zobrazí se při pokusu o zobrazení stránky chyba.

Není nutné přepsat každou `<asp:ContentPlaceHolder>` značku ze stránky předlohy na stránce zobrazení obsahu. Značku je třeba přepsat `<asp:ContentPlaceHolder>` pouze v případě, že chcete značku nahradit určitým obsahem.

Například upravené zobrazení indexu v seznamu `<asp:Content>` 3 obsahuje pouze dvě značky. Každá značka `<asp:Content>` obsahuje nějaký text.

**Výpis 3 –`Views\Home\Index.aspx (modified)`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample3.aspx)]

Když je požadováno zobrazení v seznamu 3, vykreslí stránku na obrázku 5. Všimněte si, že zobrazení vykreslí stránku se dvěma sloupci. Všimněte si dále, že obsah ze stránky obsahu zobrazení je sloučen s obsahem ze stránky předlohy zobrazení.

[![Stránka obsahu zobrazení rejstříku](creating-page-layouts-with-view-master-pages-vb/_static/image14.png)](creating-page-layouts-with-view-master-pages-vb/_static/image13.png)

**Obrázek 05**: Stránka obsahu zobrazení rejstříku[(Kliknutím zobrazíte obrázek v plné velikosti)](creating-page-layouts-with-view-master-pages-vb/_static/image15.png)

### <a name="modifying-view-master-page-content"></a>Úprava obsahu stránky předlohy zobrazení

Jedním z problémů, se kterými se setkáte téměř okamžitě při práci se stránkami předlohy zobrazení, je problém s úpravou obsahu stránky předlohy zobrazení, pokud jsou požadovány různé stránky obsahu zobrazení. Chcete například, aby každá stránka ve webové aplikaci měla jedinečný název. Název je však deklarován na stránce předlohy zobrazení a nikoli na stránce obsahu zobrazení. Jak tedy můžete přizpůsobit název stránky pro každou stránku obsahu zobrazení?

Název zobrazený na stránce obsahu zobrazení můžete upravit dvěma způsoby. Nejprve můžete přiřadit název stránky k atributu title `<%@ page %>` směrnice deklarované v horní části stránky obsahu zobrazení. Chcete-li například přiřadit zobrazení Rejstříku název stránky "Super velký web", můžete v horní části zobrazení rejstříku zahrnout následující direktivu:

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample4.aspx)]

Když je zobrazení Rejstříku vykresleno do prohlížeče, zobrazí se v záhlaví prohlížeče požadovaný název:

[![Záhlaví prohlížeče](creating-page-layouts-with-view-master-pages-vb/_static/image17.png)](creating-page-layouts-with-view-master-pages-vb/_static/image16.png)

Existuje jeden důležitý požadavek, který musí stránka předlohy splňovat, aby atribut title fungoval. Stránka předlohy zobrazení `<head runat="server">` musí obsahovat `<head>` značku namísto normální značky pro záhlaví. Pokud `<head>` značka neobsahuje atribut runat="server", název se nezobrazí. Výchozí stránka předlohy `<head runat="server">` zobrazení obsahuje požadovanou značku.

Alternativním přístupem k úpravě obsahu vzorové stránky z jednotlivých stránek obsahu zobrazení `<asp:ContentPlaceHolder>` je zalomení oblasti, kterou chcete upravit, ve značce. Představte si například, že chcete změnit nejen název, ale také metaznačky vykreslené stránkou předlohy. Stránka zobrazení předlohy v `<asp:ContentPlaceHolder>` seznamu `<head>` 4 obsahuje značku v rámci své značky.

**Výpis 4 –`Views\Shared\Site2.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample5.aspx)]

Všimněte `<asp:ContentPlaceHolder>` si, že značka ve výpisu 4 obsahuje výchozí obsah: výchozí název a výchozí metaznačky. Pokud tuto `<asp:ContentPlaceHolder>` značku nepřepíšete na stránce obsahu v jednotlivých zobrazeních, zobrazí se výchozí obsah.

Stránka zobrazení obsahu v seznamu `<asp:ContentPlaceHolder>` 5 značku přepíše, aby se zobrazil vlastní název a vlastní metaznačky.

**Výpis 5 –`Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample6.aspx)]

### <a name="summary"></a>Souhrn

Tento kurz vám poskytl základní úvod k zobrazení stránek předlohy a zobrazení stránek obsahu. Zjistili jste, jak vytvořit nové stránky předlohy zobrazení a vytvořit na nich stránky obsahu zobrazení. Zkoumali jsme také, jak můžete upravit obsah stránky předlohy zobrazení z konkrétní stránky obsahu zobrazení.

> [!div class="step-by-step"]
> [Předchozí](using-the-tagbuilder-class-to-build-html-helpers-vb.md)
> [další](passing-data-to-view-master-pages-vb.md)
