---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
title: Vytvoření vlastního ovládacího prvku AJAX Toolkit Extender (VB) | Dokumenty společnosti Microsoft
author: rick-anderson
description: Vlastní zařízení Extender umožňují přizpůsobit a rozšířit možnosti ovládacích prvků ASP.NET bez nutnosti vytvářet nové třídy.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 18b29834-c991-4e0c-b533-44d358fbfc9c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: adce8e23ccf0a3364ee85534e98f8ea67ae4718d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543675"
---
# <a name="creating-a-custom-ajax-control-toolkit-control-extender-vb"></a>Vytvoření vlastního rozšiřujícího ovládacího prvku AJAX Control Toolkit (VB)

podle [společnosti Microsoft](https://github.com/microsoft)

> Vlastní zařízení Extender umožňují přizpůsobit a rozšířit možnosti ovládacích prvků ASP.NET bez nutnosti vytvářet nové třídy.

V tomto kurzu se dozvíte, jak vytvořit vlastní rozšiřující ovládací prvek AJAX Control Toolkit. Vytvoříme jednoduchý, ale užitečný, nový extender, který změní stav Button z zakázáno, aby povoleno při zadávání textu do Textového pole. Po přečtení tohoto výukového programu, budete moci rozšířit ASP.NET AJAX Toolkit s vlastním ovládáním extendery.

Můžete vytvořit vlastní rozšiřující ovládací prvky pomocí sady Visual Studio nebo Visual Web Developer (ujistěte se, že máte nejnovější verzi aplikace Visual Web Developer).

## <a name="overview-of-the-disabledbutton-extender"></a>Přehled zařízení DisabledButton Extender

Náš nový rozšiřující systém ovládacího prvku se nazývá zařízení DisabledButton extender. Tento extender bude mít tři vlastnosti:

- TargetControlID - TextBox, který rozšiřuje ovládací prvek.
- TargetButtonIID - Tlačítko, které je zakázáno nebo povoleno.
- DisabledText - Text, který je zpočátku zobrazen v button. Když začnete psát, tlačítko zobrazí hodnotu vlastnosti Text tlačítka.

Zavěsíte rozšiřující zařízení DisabledButton na ovládací prvek TextBox a Button. Před zadáním libovolného textu je tlačítko zakázáno a textové pole a tlačítko vypadají takto:

[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image1.png)

[(Klikněte pro zobrazení full-size image)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image3.png)

Po zahájení psaní textu je tlačítko povoleno a textové pole a tlačítko vypadají takto:

[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image4.png)

[(Klikněte pro zobrazení full-size image)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image6.png)

Chcete-li vytvořit náš ovládací prvek extender, musíme vytvořit následující tři soubory:

- DisabledButtonExtender.vb - Tento soubor je třída řízení na straně serveru, která bude spravovat vytváření extenderu a umožní nastavit vlastnosti v době návrhu. Definuje také vlastnosti, které lze nastavit na extender. Tyto vlastnosti jsou přístupné prostřednictvím kódu a v době návrhu a odpovídají vlastnostem definovaným v souboru DisableButtonBehavior.js.
- DisabledButtonBehavior.js -- Tento soubor je místo, kde přidáte všechny logiky klientského skriptu.
- DisabledButtonDesigner.vb - Tato třída umožňuje funkce návrhu. Tuto třídu potřebujete, pokud chcete, aby rozšiřující zařízení ovládacího prvku fungovalo správně s aplikací Visual Studio/Visual Web Developer Designer.

Rozšíření ovládacího prvku se tedy skládá z ovládacího prvku na straně serveru, chování na straně klienta a třídy návrháře na straně serveru. Můžete se dozvědět, jak vytvořit všechny tři tyto soubory v následujících částech.

## <a name="creating-the-custom-extender-website-and-project"></a>Vytvoření vlastního webu a projektu zařízení Extender

Prvním krokem je vytvoření projektu a webu knihovny tříd v sadě Visual Studio/Visual Web Developer. Vytvoříme vlastní extender v projektu knihovny tříd a otestujeme vlastní extender na webu.

Začněme s webovými stránkami. Chcete-li vytvořit web, postupujte takto:

1. Vyberte možnost nabídky **Soubor, Nový web**.
2. Vyberte šablonu **ASP.NET webu.**
3. Název nové webové stránky *Website1*.
4. Klikněte na tlačítko **OK.**

Dále musíme vytvořit projekt knihovny tříd, který bude obsahovat kód pro rozšiřující ovládací prvek:

1. Vyberte možnost nabídky **Soubor, Přidat, Nový projekt**.
2. Vyberte šablonu **Knihovna tříd.**
3. Pojmenujte novou knihovnu tříd s názvem **CustomExtenders**.
4. Klikněte na tlačítko **OK.**

Po dokončení těchto kroků by okno Průzkumníka řešení mělo vypadat na obrázku 1.

[![Řešení s projektem webové stránky a knihovny tříd](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image7.png)

**Obrázek 01**: Řešení s webovými stránkami a knihovnou tříd[(Kliknutím zobrazíte obrázek v plné velikosti)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image9.png)

Dále je třeba přidat všechny potřebné odkazy na sestavení do projektu knihovny tříd:

1. Klepněte pravým tlačítkem myši na projekt Vlastní zařízení a vyberte možnost nabídky **Přidat odkaz**.
2. Vyberte kartu .NET.
3. Přidejte odkazy na následující sestavení:

    1. Soubor System.Web.dll
    2. Soubor System.Web.Extensions.dll
    3. Soubor System.Design.dll
    4. Soubor System.Web.Extensions.Design.dll
4. Vyberte kartu Procházet.
5. Přidejte odkaz na sestavení AjaxControlToolkit.dll. Toto sestavení je umístěno ve složce, do které jste stáhli sadu nástrojů AJAX Control Toolkit.

Můžete ověřit, že jste přidali všechny správné odkazy, kliknutím pravým tlačítkem myši na projekt, výběrem možnosti Vlastnosti a kliknutím na kartu Odkazy (viz obrázek 2).

[![Složka Reference s požadovanými odkazy](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image10.png)

**Obrázek 02**: Referenční složka s požadovanými odkazy[(Obrázek v plné velikosti zobrazíte](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image12.png)klepnutím).

## <a name="creating-the-custom-control-extender"></a>Vytvoření zařízení Pro rozšíření vlastního ovládacího prvku

Teď, když máme naši třídní knihovnu, můžeme začít budovat naši rozšiřující kontrolu. Začněme holými kostmi vlastní třídy řízení extenderu (viz výpis 1).

**Výpis 1 - MyCustomExtender.vb**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample1.vb)]

Existuje několik věcí, které si všimnete o třídě rozšíření ovládacího prvku v výpisu 1. Nejprve si všimněte, že třída dědí ze základní třídy ExtenderControlBase. Všechny ovládací prvky rozšiřujícísady nástrojů AJAX Control Toolkit jsou odvozeny z této základní třídy. Například základní třída zahrnuje vlastnost TargetID, která je povinnou vlastností každého rozšiřujícího ovládacího prvku.

Dále všimněte si, že třída obsahuje následující dva atributy související s klientským skriptem:

- Webový prostředek - Způsobí, že soubor bude zahrnut jako vložený prostředek v sestavení.
- ClientScriptResource - Způsobí, že prostředek skriptu, které mají být načteny ze sestavení.

Atribut WebResource se používá k vložení souboru JavaScript myControlBehavior.js do sestavení při kompilaci vlastního zařízení extender. Atribut ClientScriptResource se používá k načtení skriptu MyControlBehavior.js ze sestavení při použití vlastního zařízení extender na webové stránce.

Aby atributy WebResource a ClientScriptResource fungovaly, musíte zkompilovat soubor JavaScriptu jako vložený prostředek. Vyberte soubor v okně Průzkumník řešení, otevřete seznam vlastností a *přiřaďte* hodnotu Vložený prostředek vlastnosti **Akce sestavení.**

Všimněte si, že rozšiřující ovládací prvek ovládacího prvku také obsahuje atribut TargetControlType. Tento atribut se používá k určení typu ovládacího prvku, který je rozšířen o rozšiřující ovládací prvek. V případě výpisu 1 ovládací prvek extender se používá k rozšíření TextBox.

Nakonec všimněte si, že vlastní extender obsahuje vlastnost s názvem MyProperty. Vlastnost je označena atributem ExtenderControlProperty. Metody GetPropertyValue() a SetPropertyValue() se používají k předání hodnoty vlastnosti z rozšiřujícího zařízení ovládacího prvku na straně serveru chování na straně klienta.

Pojďme dopředu a implementovat kód pro naše DisabledButton extender. Kód pro tento extender naleznete v seznamu 2.

**Výpis 2 - DisabledButtonExtender.vb**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample2.vb)]

Zařízení DisabledButton v seznamu 2 má dvě vlastnosti s názvem TargetButtonID a DisabledText. Vlastnost IDReferenceProperty použitá na vlastnost TargetButtonID zabraňuje přiřazení jiného než ID ovládacího prvku Button této vlastnosti.

Atributy WebResource a ClientScriptResource přidruží k tomuto zařízení extender chování na straně klienta umístěné v souboru s názvem DisabledButtonBehavior.js. Tento soubor JavaScript ubereme v další části.

## <a name="creating-the-custom-extender-behavior"></a>Vytvoření vlastního chování zařízení Extender

Součást rozšíření ovládacího prvku na straně klienta se nazývá chování. Skutečná logika pro zakázání a povolení Button je obsažena v Chování DisabledButton. JavaScript kód pro chování je součástí výpisu 3.

**Výpis 3 - DisabledButton.js**

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample3.js)]

Soubor JavaScript v výpisu 3 obsahuje třídu na straně klienta s názvem DisabledButtonBehavior. Tato třída, stejně jako její dvojče na straně serveru, obsahuje dvě vlastnosti\_s názvem TargetButtonID a DisabledText, ke kterým máte přístup pomocí funkce get TargetButtonID/set\_TargetButtonID a získat\_DisabledText/set\_DisabledText.

Metoda initialize() přidruží obslužnou rutinu události keyup k cílovému prvku pro chování. Pokaždé, když zadáte písmeno do textového pole přidruženého k tomuto chování, spustí se obslužná rutina keyup. Obslužná rutina keyup buď povolí nebo zakáže Button v závislosti na tom, zda textbox přidružený k chování obsahuje libovolný text.

Nezapomeňte, že je nutné zkompilovat soubor JavaScript v výpisu 3 jako vložený prostředek. Vyberte soubor v okně Průzkumník řešení, otevřete seznam vlastností a přiřaďte hodnotu *Vložený prostředek* vlastnosti **Akce sestavení** (viz obrázek 3). Tato možnost je k dispozici v sadě Visual Studio i Visual Web Developer.

[![Přidání souboru JavaScriptu jako vloženého prostředku](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image13.png)

**Obrázek 03**: Přidání souboru JavaScript jako vložený zdroj[(Klikněte pro zobrazení full-size image)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image15.png)

## <a name="creating-the-custom-extender-designer"></a>Vytvoření vlastního návrháře zařízení extender

Je tu jedna poslední třída, kterou musíme vytvořit, abychom dokončili náš extender. Musíme vytvořit třídu návrháře v seznamu 4. Tato třída je nutné, aby extender chovat správně s Visual Studio/Visual Web Developer Designer.

**Výpis 4 - DisabledButtonDesigner.vb**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample4.vb)]

Přidružíte návrháře v listingu 4 k zařízení DisabledButton extender s atributem Designer. Atribut Designer je třeba použít pro třídu DisabledButtonExtender takto:

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample5.vb)]

## <a name="using-the-custom-extender"></a>Použití vlastního zařízení Extender

Nyní, když jsme dokončili vytváření rozšiřujícího ovládacího prvku DisabledButton, je čas jej použít v našem ASP.NET webových stránkách. Nejprve musíme přidat vlastní extender do panelu nástrojů. Postupujte následovně:

1. Otevřete ASP.NET stránku poklepáním na stránku v okně Průzkumník řešení.
2. Klepněte pravým tlačítkem myši na panel nástrojů a vyberte volbu nabídky **Zvolit položky**.
3. V dialogovém okně Zvolit položky panelu nástrojů přejděte do sestavy CustomExtenders.dll.
4. Klepnutím na tlačítko **OK** zavřete dialogové okno.

Po dokončení těchto kroků by se měl v panelu nástrojů zobrazit rozšiřující ovládací prvek DisabledButton (viz obrázek 4).

[![DisabledButton v panelu nástrojů](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image16.png)

**Obrázek 04**: DisabledButton v panelu nástrojů([Klepnutím zobrazíte obrázek v plné velikosti)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image18.png)

Dále musíme vytvořit novou stránku ASP.NET. Postupujte následovně:

1. Vytvořte novou stránku ASP.NET s názvem ShowDisabledButton.aspx.
2. Přetáhněte na stránku správce skriptů.
3. Přetáhněte ovládací prvek TextBox na stránku.
4. Přetáhněte ovládací prvek Button na stránku.
5. V okně Vlastnosti změňte vlastnost ID tlačítka na hodnotu <em>btnSave</em> a vlastnost Text na hodnotu *\*Uložit*.

Vytvořili jsme stránku se standardním ASP.NET ovládacího prvku TextBox a Button.

Dále musíme rozšířit ovládací prvek TextBox s disabledbutton extender:

1. Výběrem možnosti **Přidat úlohu zařízení pro zařízení** otevřete dialogové okno Průvodce pro rozstavovač (viz obrázek 5). Všimněte si, že dialogové okno obsahuje naše vlastní DisabledButton extender.
2. Vyberte zařízení DisabledButton extender a klepněte na tlačítko **OK.**

[![Dialogové okno Průvodce rozšiřovačem](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image19.png)

**Obrázek 05**: Dialogové okno Průvodce pro rozkládání[(Klepnutím zobrazíte obrázek v plné velikosti)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image21.png)

Nakonec můžeme nastavit vlastnosti disabledbutton extender. Vlastnosti zařízení DisabledButton extender můžete upravit úpravou vlastností ovládacího prvku TextBox:

1. V návrháři vyberte textové pole.
2. V okně Vlastnosti rozbalte uzel Zařízení pro rozšíření (viz obrázek 6).
3. Přiřaďte hodnotu *Uložit* vlastnostdisabledText a hodnotu *btnSave* vlastnosti TargetButtonID.

[![Nastavení vlastností zařízení extender](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image22.png)

**Obrázek 06**: Nastavení vlastností zařízení extender([Klepnutím zobrazíte obrázek v plné velikosti)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image24.png)

Při spuštění stránky (stisknutím f5) button ovládací prvek je zpočátku zakázáno. Jakmile začnete zadávat text do textového pole, ovládací prvek Button je povolen (viz obrázek 7).

[![Zařízení DisabledButton v akci](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image25.png)

**Obrázek 07**: Zařízení pro rozšíření DisabledButton v[akci(Obrázek v plné velikosti)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image27.png)

## <a name="summary"></a>Souhrn

Cílem tohoto kurzu bylo vysvětlit, jak můžete rozšířit sadu nástrojů AJAX Control Toolkit s vlastními ovládacími prvky extenderu. V tomto kurzu jsme vytvořili jednoduchý rozšiřující ovládací prvek DisabledButton. Tento extender jsme implementovali vytvořením třídy DisabledButtonExtender, javascriptového chování DisabledButtonBehavior a třídy DisabledButtonDesigner. Podobnou sadu kroků budete dodržovat při každém vytvoření vlastního rozšiřovače ovládacího prvku.

> [!div class="step-by-step"]
> [Předchozí](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)
