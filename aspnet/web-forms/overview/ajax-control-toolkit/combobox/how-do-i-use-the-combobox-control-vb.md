---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-vb
title: Použití ovládacího prvku ComboBox (VB) | Dokumentace Microsoftu
author: microsoft
description: Pole se seznamem je ovládací prvek ASP.NET AJAX, který kombinuje flexibilitu textové pole se seznamem možností, ze kterých mohou uživatelé vybrat.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: e887e7b2-a6e7-4a28-a134-ba334494badb
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 2e33c7cfae7eed3c0b38b66dad779ce7dcd77b54
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59399681"
---
# <a name="how-do-i-use-the-combobox-control-vb"></a><span data-ttu-id="4aed7-104">Použití ovládacího prvku ComboBox</span><span class="sxs-lookup"><span data-stu-id="4aed7-104">How do I use the ComboBox Control?</span></span> <span data-ttu-id="4aed7-105">(VB)</span><span class="sxs-lookup"><span data-stu-id="4aed7-105">(VB)</span></span>

<span data-ttu-id="4aed7-106">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="4aed7-106">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="4aed7-107">Pole se seznamem je ovládací prvek ASP.NET AJAX, který kombinuje flexibilitu textové pole se seznamem možností, ze kterých mohou uživatelé vybrat.</span><span class="sxs-lookup"><span data-stu-id="4aed7-107">ComboBox is an ASP.NET AJAX control that combines the flexibility of a TextBox with a list of options from which users can choose.</span></span>


<span data-ttu-id="4aed7-108">Cílem tohoto kurzu je vysvětlit ovládacího prvku Toolkit ComboBox ovládacího prvku AJAX.</span><span class="sxs-lookup"><span data-stu-id="4aed7-108">The goal of this tutorial is to explain the AJAX Control Toolkit ComboBox control.</span></span> <span data-ttu-id="4aed7-109">Pole se seznamem funguje jako kombinace standardní ovládací prvek DropDownList s ASP.NET a ovládací prvek textového pole.</span><span class="sxs-lookup"><span data-stu-id="4aed7-109">The ComboBox works like a combination between a standard ASP.NET DropDownList control and a TextBox control.</span></span> <span data-ttu-id="4aed7-110">Můžete vybrat z existující seznam položek, nebo zadejte novou položku.</span><span class="sxs-lookup"><span data-stu-id="4aed7-110">You can either select from a pre-existing list of items or enter a new item.</span></span>

<span data-ttu-id="4aed7-111">Pole se seznamem se podobá – extender ovládacího prvku automatické dokončování, ale ovládací prvky se používají v různých scénářích.</span><span class="sxs-lookup"><span data-stu-id="4aed7-111">The ComboBox is similar to the AutoComplete control extender, but the controls are used in different scenarios.</span></span> <span data-ttu-id="4aed7-112">Zařízení extender automatické dokončování dotazů webovou službu, která najít odpovídající položky.</span><span class="sxs-lookup"><span data-stu-id="4aed7-112">The AutoComplete extender queries a web service to get matching entries.</span></span> <span data-ttu-id="4aed7-113">ComboBox – ovládací prvek naproti tomu je inicializována s sadu položek.</span><span class="sxs-lookup"><span data-stu-id="4aed7-113">The ComboBox control, in contrast, is initialized with a set of items.</span></span> <span data-ttu-id="4aed7-114">Umožňuje zařízení extender automatické dokončování pomocí smysl při práci s rozsáhlou sadou dat (miliony částí auta) při používání ovládacího prvku ComboBox dává smysl při práci s malou sadu dat (desítky car části).</span><span class="sxs-lookup"><span data-stu-id="4aed7-114">Using the AutoComplete extender makes sense when you are working with a large set of data (millions of car parts) while using the ComboBox control makes sense when working with a small set of data (dozens of car parts).</span></span>

## <a name="selecting-from-a-static-list-of-items"></a><span data-ttu-id="4aed7-115">Výběr ze statické seznam položek</span><span class="sxs-lookup"><span data-stu-id="4aed7-115">Selecting from a Static List of Items</span></span>

<span data-ttu-id="4aed7-116">Umožní s začínat jednoduchý příklad použití ovládacího prvku pole se seznamem.</span><span class="sxs-lookup"><span data-stu-id="4aed7-116">Let�s start with a simple sample of using the ComboBox control.</span></span> <span data-ttu-id="4aed7-117">Představte si, že chcete zobrazit statický seznam položek v rozevíracím seznamu.</span><span class="sxs-lookup"><span data-stu-id="4aed7-117">Imagine that you want to display a static list of items in a dropdown list.</span></span> <span data-ttu-id="4aed7-118">Ale budete chtít zůstat otevřeno, možnost, že seznam není úplný.</span><span class="sxs-lookup"><span data-stu-id="4aed7-118">However, you want to leave open the possibility that the list is not complete.</span></span> <span data-ttu-id="4aed7-119">Budete chtít umožnit uživateli zadat vlastní hodnoty do seznamu.</span><span class="sxs-lookup"><span data-stu-id="4aed7-119">You want to allow a user to enter a custom value into the list.</span></span>

<span data-ttu-id="4aed7-120">Jsme ll vytvoření nové stránky webových formulářů ASP.NET a pomocí ovládacího prvku pole se seznamem na stránce.</span><span class="sxs-lookup"><span data-stu-id="4aed7-120">We�ll create a new ASP.NET Web Forms page and use the ComboBox control in the page.</span></span> <span data-ttu-id="4aed7-121">Do projektu přidejte novou stránku ASP.NET a přepněte do zobrazení návrhu.</span><span class="sxs-lookup"><span data-stu-id="4aed7-121">Add the new ASP.NET page to your project and switch to Design view.</span></span>

<span data-ttu-id="4aed7-122">Pokud chcete pomocí ovládacího prvku pole se seznamem na stránce musíte přidat ovládací prvek ScriptManager na stránce.</span><span class="sxs-lookup"><span data-stu-id="4aed7-122">If you want to use the ComboBox control in the page then you must add a ScriptManager control to the page.</span></span> <span data-ttu-id="4aed7-123">Přetáhněte ovládací prvek ScriptManager from beneath na kartě Rozšíření AJAX na plochu návrháře.</span><span class="sxs-lookup"><span data-stu-id="4aed7-123">Drag the ScriptManager control from beneath the AJAX Extensions tab onto the Designer surface.</span></span> <span data-ttu-id="4aed7-124">Měli byste přidat ovládací prvek ScriptManager v horní části stránky. můžete ho přidat bezprostředně pod levou serverové &lt;formuláře&gt; značky.</span><span class="sxs-lookup"><span data-stu-id="4aed7-124">You should add the ScriptManager control at the top of the page; you can add it immediately below the opening server-side &lt;form&gt; tag.</span></span>

<span data-ttu-id="4aed7-125">V dalším kroku přetáhněte ovládací prvek pole se seznamem na stránku.</span><span class="sxs-lookup"><span data-stu-id="4aed7-125">Next, drag the ComboBox control onto the page.</span></span> <span data-ttu-id="4aed7-126">ComboBox – ovládací prvek můžete najít v panelu nástrojů s jinými sadou nástrojů AJAX Control Toolkit ovládacích prvků a extenderů (viz obrázek 1).</span><span class="sxs-lookup"><span data-stu-id="4aed7-126">You can find the ComboBox control in the Toolbox with the other AJAX Control Toolkit controls and control extenders (see figure1).</span></span>


[![S<span data-ttu-id="4aed7-127">uchá formulář pro vytvoření vizitky]</span><span class="sxs-lookup"><span data-stu-id="4aed7-127">imple form for creating a business card]</span></span>(how-do-i-use-the-combobox-control-vb/_static/image1.jpg)](how-do-i-use-the-combobox-control-vb/_static/image1.png)

<span data-ttu-id="4aed7-128">**Obrázek 01**: ComboBox – ovládací prvek výběru z panelu nástrojů ([kliknutím ji zobrazíte obrázek v plné velikosti](how-do-i-use-the-combobox-control-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="4aed7-128">**Figure 01**: Selecting the ComboBox control from the toolbox ([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image2.png))</span></span>


<span data-ttu-id="4aed7-129">Jsme ll pomocí ovládacího prvku pole se seznamem pro zobrazení statický seznam voleb.</span><span class="sxs-lookup"><span data-stu-id="4aed7-129">We�ll use the ComboBox control to display a static list of choices.</span></span> <span data-ttu-id="4aed7-130">Uživatel můžete vybrat určitou úroveň spiciness pro jejich potravin ze seznamu tři možnosti: Mírné, střední a aktivní (viz obrázek 2).</span><span class="sxs-lookup"><span data-stu-id="4aed7-130">The user can select a particular level of spiciness for their food from a list of three choices: Mild, Medium, and Hot (see Figure 2).</span></span>


[![S<span data-ttu-id="4aed7-131">jak zvolit ze statické seznam položek]</span><span class="sxs-lookup"><span data-stu-id="4aed7-131">electing from a static list of items]</span></span>(how-do-i-use-the-combobox-control-vb/_static/image2.jpg)](how-do-i-use-the-combobox-control-vb/_static/image3.png)

<span data-ttu-id="4aed7-132">**Obrázek 02**: Výběr ze statické seznam položek ([kliknutím ji zobrazíte obrázek v plné velikosti](how-do-i-use-the-combobox-control-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="4aed7-132">**Figure 02**: Selecting from a static list of items([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image4.png))</span></span>


<span data-ttu-id="4aed7-133">Existují dva způsoby, že tyto možnosti můžete přidat do ovládacího prvku pole se seznamem.</span><span class="sxs-lookup"><span data-stu-id="4aed7-133">There are two ways that you can add these choices to the ComboBox control.</span></span> <span data-ttu-id="4aed7-134">Nejprve vyberte možnost upravit možnosti úkolu, když myší najedete myší na ovládací prvek v návrhovém zobrazení a otevřete Editor položek (viz obrázek 3).</span><span class="sxs-lookup"><span data-stu-id="4aed7-134">First, you select the Edit Options task option when hovering your mouse over the control in Design view and open the Item Editor (see Figure 3).</span></span>


[![E<span data-ttu-id="4aed7-135">položky pole se seznamem ATO funkce]</span><span class="sxs-lookup"><span data-stu-id="4aed7-135">diting ComboBox items]</span></span>(how-do-i-use-the-combobox-control-vb/_static/image3.jpg)](how-do-i-use-the-combobox-control-vb/_static/image5.png)

<span data-ttu-id="4aed7-136">**Obrázek 03**: Úprava pole se seznamem položek ([kliknutím ji zobrazíte obrázek v plné velikosti](how-do-i-use-the-combobox-control-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="4aed7-136">**Figure 03**: Editing ComboBox items([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image6.png))</span></span>


<span data-ttu-id="4aed7-137">Druhou možností je přidat seznam položek mezi otevírací a zavírací &lt;asp: pole se seznamem&gt; značky v zobrazení zdroje.</span><span class="sxs-lookup"><span data-stu-id="4aed7-137">The second option is to add the list of items in between the opening and closing &lt;asp:ComboBox&gt; tags in Source view.</span></span> <span data-ttu-id="4aed7-138">Na stránce v informacích 1 obsahuje aktualizované pole se seznamem, který má seznam položek.</span><span class="sxs-lookup"><span data-stu-id="4aed7-138">The page in Listing 1 contains the updated ComboBox that has the list of items.</span></span>

**<span data-ttu-id="4aed7-139">Výpis 1 - Static.aspx</span><span class="sxs-lookup"><span data-stu-id="4aed7-139">Listing 1 - Static.aspx</span></span>**

[!code-aspx[Main](how-do-i-use-the-combobox-control-vb/samples/sample1.aspx)]

<span data-ttu-id="4aed7-140">Při otevření stránky v informacích 1, můžete vybrat jednu z již existujících možností z pole se seznamem.</span><span class="sxs-lookup"><span data-stu-id="4aed7-140">When you open the page in Listing 1, you can select one of the pre-existing options from the ComboBox.</span></span> <span data-ttu-id="4aed7-141">Jinými slovy pole se seznamem funguje stejně jako ovládací prvek DropDownList.</span><span class="sxs-lookup"><span data-stu-id="4aed7-141">In other words, the ComboBox works just like a DropDownList control.</span></span>

<span data-ttu-id="4aed7-142">Nicméně máte také možnost zadat novou volbu (třeba Super Spicy), který není v seznamu existujících.</span><span class="sxs-lookup"><span data-stu-id="4aed7-142">However, you also have the option of entering a new choice (for example, Super Spicy) that is not in the existing list.</span></span> <span data-ttu-id="4aed7-143">Ano pole se seznamem funguje také jako ovládací prvek textového pole.</span><span class="sxs-lookup"><span data-stu-id="4aed7-143">So, the ComboBox also works like a TextBox control.</span></span>

<span data-ttu-id="4aed7-144">Bez ohledu na to, jestli si vybrat existující položky nebo můžete zadat vlastní položky při odeslání formuláře, podle vašeho výběru se zobrazí v ovládacím prvku popisek.</span><span class="sxs-lookup"><span data-stu-id="4aed7-144">Regardless of whether you pick a pre-existing item or you enter a custom item, when you submit the form, your choice appears in the label control.</span></span> <span data-ttu-id="4aed7-145">Po odeslání formuláře btnSubmit\_kliknutím obslužná rutina spustí a aktualizuje popisek (viz obrázek 4).</span><span class="sxs-lookup"><span data-stu-id="4aed7-145">When you submit the form, the btnSubmit\_Click handler executes and updates the label (see Figure 4).</span></span>


[![D<span data-ttu-id="4aed7-146">Vybraná položka isplaying]</span><span class="sxs-lookup"><span data-stu-id="4aed7-146">isplaying the selected item]</span></span>(how-do-i-use-the-combobox-control-vb/_static/image4.jpg)](how-do-i-use-the-combobox-control-vb/_static/image7.png)

<span data-ttu-id="4aed7-147">**Obrázek 04**: Zobrazení vybrané položky ([kliknutím ji zobrazíte obrázek v plné velikosti](how-do-i-use-the-combobox-control-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="4aed7-147">**Figure 04**: Displaying the selected item([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image8.png))</span></span>


<span data-ttu-id="4aed7-148">Pole se seznamem podporuje stejné vlastnosti jako ovládací prvek DropDownList pro načtení vybrané položky po odeslání formuláře:</span><span class="sxs-lookup"><span data-stu-id="4aed7-148">The ComboBox supports the same properties as the DropDownList control for retrieving the selected item after a form is submitted:</span></span>

- <span data-ttu-id="4aed7-149">SelectedItem.Text – zobrazí hodnoty vlastnosti Text vybrané položky.</span><span class="sxs-lookup"><span data-stu-id="4aed7-149">SelectedItem.Text - Displays the value of the Text property of the selected item.</span></span>
- <span data-ttu-id="4aed7-150">SelectedItem.Value – zobrazí hodnoty vlastnosti hodnotu vybrané položky nebo zobrazuje text zadaný do pole se seznamem.</span><span class="sxs-lookup"><span data-stu-id="4aed7-150">SelectedItem.Value - Displays the value of the Value property of the selected item or displays the text typed into the ComboBox.</span></span>
- <span data-ttu-id="4aed7-151">SelectedValue – stejný jako SelectedItem.Value s tím rozdílem, že tato vlastnost umožňuje určit výchozí (počáteční) vybranou položku.</span><span class="sxs-lookup"><span data-stu-id="4aed7-151">SelectedValue - Same as SelectedItem.Value except that this property enables you to specify the default (initial) selected item.</span></span>

<span data-ttu-id="4aed7-152">Pokud zadáte vlastní možnost do pole se seznamem pak podle vlastního výběru přiřazená SelectedItem.Text i SelectedItem.Value vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="4aed7-152">If you type a custom choice into the ComboBox then the custom choice is assigned to both the SelectedItem.Text and SelectedItem.Value properties.</span></span>

## <a name="selecting-the-list-of-items-from-the-database"></a><span data-ttu-id="4aed7-153">Výběr v seznamu položek z databáze</span><span class="sxs-lookup"><span data-stu-id="4aed7-153">Selecting the List of Items from the Database</span></span>

<span data-ttu-id="4aed7-154">Seznam položek, které zobrazí pole se seznamem můžete načíst z databáze.</span><span class="sxs-lookup"><span data-stu-id="4aed7-154">You can retrieve the list of items that the ComboBox displays from a database.</span></span> <span data-ttu-id="4aed7-155">Například lze svázat pole se seznamem ovládacím prvkem SqlDataSource, ovládací prvek ObjectDataSource, zdroje dat LinqDataSource nebo EntityDataSource.</span><span class="sxs-lookup"><span data-stu-id="4aed7-155">For example, you can bind the ComboBox to a SqlDataSource control, an ObjectDataSource control, a LinqDataSource, or an EntityDataSource.</span></span>

<span data-ttu-id="4aed7-156">Představte si, že chcete zobrazit seznam filmy v pole se seznamem.</span><span class="sxs-lookup"><span data-stu-id="4aed7-156">Imagine that you want to display a list of movies in a ComboBox.</span></span> <span data-ttu-id="4aed7-157">Chcete načíst seznam videa z databázové tabulky videa.</span><span class="sxs-lookup"><span data-stu-id="4aed7-157">You want to retrieve the list of movies from the Movies database table.</span></span> <span data-ttu-id="4aed7-158">Postupujte podle těchto kroků:</span><span class="sxs-lookup"><span data-stu-id="4aed7-158">Follow these steps:</span></span>

1. <span data-ttu-id="4aed7-159">Vytvoření stránky s názvem Movies.aspx</span><span class="sxs-lookup"><span data-stu-id="4aed7-159">Create a page named Movies.aspx</span></span>
2. <span data-ttu-id="4aed7-160">Přidání ovládacího prvku ScriptManager na stránce přetažením ScriptManager získáte na kartě Rozšíření AJAX na panelu nástrojů na stránku.</span><span class="sxs-lookup"><span data-stu-id="4aed7-160">Add a ScriptManager control to the page by dragging the ScriptManager from under the AJAX Extensions tab in the Toolbox onto the page.</span></span>
3. <span data-ttu-id="4aed7-161">Přidání ovládacího prvku pole se seznamem na stránku tak, že přetáhnete pole se seznamem na stránku.</span><span class="sxs-lookup"><span data-stu-id="4aed7-161">Add a ComboBox control to the page by dragging the ComboBox onto the page.</span></span>
4. <span data-ttu-id="4aed7-162">V návrhovém zobrazení přesunutí ukazatele myši nad ovládací prvek pole se seznamem a vyberte **zvolit zdroj dat** úloh možnost (viz obrázek 5).</span><span class="sxs-lookup"><span data-stu-id="4aed7-162">In Design view, hover your mouse over the ComboBox control and select the **Choose Data Source** task option (see Figure 5).</span></span> <span data-ttu-id="4aed7-163">Průvodce konfigurací zdroje dat není spuštěn.</span><span class="sxs-lookup"><span data-stu-id="4aed7-163">The Data Source Configuration Wizard is launched.</span></span>
5. <span data-ttu-id="4aed7-164">V **vyberte zdroj dat** kroku, vyberte &lt;nový zdroj dat&gt; možnost.</span><span class="sxs-lookup"><span data-stu-id="4aed7-164">In the **Choose a Data Source** step, select the &lt;New data source�&gt; option.</span></span>
6. <span data-ttu-id="4aed7-165">V **zvolte typ zdroje dat** kroku, vyberte databázi.</span><span class="sxs-lookup"><span data-stu-id="4aed7-165">In the **Choose a Data Source Type** step, select Database.</span></span>
7. <span data-ttu-id="4aed7-166">V **vyberte datové připojení** kroku, vyberte svou databázi (například MoviesDB.mdf).</span><span class="sxs-lookup"><span data-stu-id="4aed7-166">In the **Choose Your Data Connection** step, select your database (for example, MoviesDB.mdf).</span></span>
8. <span data-ttu-id="4aed7-167">V **uložit připojovací řetězec do konfiguračního souboru aplikace** kroku, vyberte možnost Uložit připojovací řetězec.</span><span class="sxs-lookup"><span data-stu-id="4aed7-167">In the **Save the Connection String to the Application Configuration File** step, select the option to save your connection string.</span></span>
9. <span data-ttu-id="4aed7-168">V **konfigurovat příkaz Select** kroku, vyberte v tabulce databáze filmů a vybrat všechny sloupce.</span><span class="sxs-lookup"><span data-stu-id="4aed7-168">In the **Configure the Select Statement** step, select the Movies database table and select all of the columns.</span></span>
10. <span data-ttu-id="4aed7-169">V **testovat dotaz** krok, kliknutím na tlačítko Dokončit.</span><span class="sxs-lookup"><span data-stu-id="4aed7-169">In the **Test Query** step, click the Finish button.</span></span>
11. <span data-ttu-id="4aed7-170">Zpátky **zvolit zdroj dat** kroku, vyberte sloupec název pro pole k zobrazení a ve sloupci Id pro data polí (viz obrázek).</span><span class="sxs-lookup"><span data-stu-id="4aed7-170">Back in the **Choose Data Source** step, select the Title column for the field to display and the Id column for the data field (see Figure).</span></span>
12. <span data-ttu-id="4aed7-171">Klikněte na tlačítko OK ukončete průvodce.</span><span class="sxs-lookup"><span data-stu-id="4aed7-171">Click the OK button to close the wizard.</span></span>


[![C<span data-ttu-id="4aed7-172">zdroj dat hoosing]</span><span class="sxs-lookup"><span data-stu-id="4aed7-172">hoosing a data source]</span></span>(how-do-i-use-the-combobox-control-vb/_static/image5.jpg)](how-do-i-use-the-combobox-control-vb/_static/image9.png)

<span data-ttu-id="4aed7-173">**Obrázek 05**: Výběr zdroje dat ([kliknutím ji zobrazíte obrázek v plné velikosti](how-do-i-use-the-combobox-control-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="4aed7-173">**Figure 05**: Choosing a data source([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image10.png))</span></span>


[![C<span data-ttu-id="4aed7-174">Hodnota pole a hoosing text dat]</span><span class="sxs-lookup"><span data-stu-id="4aed7-174">hoosing the data text and value fields]</span></span>(how-do-i-use-the-combobox-control-vb/_static/image6.jpg)](how-do-i-use-the-combobox-control-vb/_static/image11.png)

<span data-ttu-id="4aed7-175">**Obrázek 06**: Výběr datových polí hodnoty a text ([kliknutím ji zobrazíte obrázek v plné velikosti](how-do-i-use-the-combobox-control-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="4aed7-175">**Figure 06**: Choosing the data text and value fields([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image12.png))</span></span>


<span data-ttu-id="4aed7-176">Po dokončení výše uvedených kroků, pole se seznamem je svázána s ovládacím prvkem SqlDataSource, představující videa z databázové tabulky filmy.</span><span class="sxs-lookup"><span data-stu-id="4aed7-176">After you complete the steps above, the ComboBox is bound to a SqlDataSource control that represents the movies from the Movies database table.</span></span> <span data-ttu-id="4aed7-177">Zdroj pro stránku vypadá výpis 2 (mám vyčištění formátování trochu).</span><span class="sxs-lookup"><span data-stu-id="4aed7-177">The source for the page looks like Listing 2 (I cleaned up the formatting a little bit).</span></span>

**<span data-ttu-id="4aed7-178">Výpis 2 - Movies.aspx</span><span class="sxs-lookup"><span data-stu-id="4aed7-178">Listing 2 - Movies.aspx</span></span>**

[!code-aspx[Main](how-do-i-use-the-combobox-control-vb/samples/sample2.aspx)]

<span data-ttu-id="4aed7-179">Všimněte si, že ovládací prvek pole se seznamem má vlastnost DataSourceID, která odkazuje na ovládacím prvkem SqlDataSource.</span><span class="sxs-lookup"><span data-stu-id="4aed7-179">Notice that the ComboBox control has a DataSourceID property that points to the SqlDataSource control.</span></span> <span data-ttu-id="4aed7-180">Když otevřete stránku v prohlížeči se zobrazí seznam videa z databáze (viz obrázek 7).</span><span class="sxs-lookup"><span data-stu-id="4aed7-180">When you open the page in a browser, the list of movies from the database is displayed (see Figure 7).</span></span> <span data-ttu-id="4aed7-181">Můžete vybrat video ze seznamu nebo zadejte nový film zadáním videa do pole se seznamem.</span><span class="sxs-lookup"><span data-stu-id="4aed7-181">You can either a pick a movie from the list or enter a new movie by typing the movie into the ComboBox.</span></span>


[![D<span data-ttu-id="4aed7-182">seznam filmy isplaying]</span><span class="sxs-lookup"><span data-stu-id="4aed7-182">isplaying a list of movies]</span></span>(how-do-i-use-the-combobox-control-vb/_static/image7.jpg)](how-do-i-use-the-combobox-control-vb/_static/image13.png)

<span data-ttu-id="4aed7-183">**Obrázek 07**: Zobrazení seznamu filmy ([kliknutím ji zobrazíte obrázek v plné velikosti](how-do-i-use-the-combobox-control-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="4aed7-183">**Figure 07**: Displaying a list of movies([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image14.png))</span></span>


## <a name="setting-the-dropdownstyle"></a><span data-ttu-id="4aed7-184">Nastavení DropDownStyle</span><span class="sxs-lookup"><span data-stu-id="4aed7-184">Setting the DropDownStyle</span></span>

<span data-ttu-id="4aed7-185">Pokud chcete změnit chování pole se seznamem můžete použít vlastnost DropDownStyle – pole se seznamem.</span><span class="sxs-lookup"><span data-stu-id="4aed7-185">You can use the ComboBox DropDownStyle property to change the behavior of the ComboBox.</span></span> <span data-ttu-id="4aed7-186">Tato vlastnost přijímá není možné hodnoty:</span><span class="sxs-lookup"><span data-stu-id="4aed7-186">This property accepts there possible values:</span></span>

- <span data-ttu-id="4aed7-187">Rozevírací seznam – (výchozí hodnota) zobrazí The – pole se seznamem rozevírací seznam, když kliknete na šipku a vy můžete zadat vlastní hodnotu.</span><span class="sxs-lookup"><span data-stu-id="4aed7-187">DropDown - (default value) The ComboBox displays a dropdown list when you click the arrow and you can enter a custom value.</span></span>
- <span data-ttu-id="4aed7-188">Jednoduché – pole se seznamem se automaticky zobrazí rozevírací seznam a můžete zadat vlastní hodnoty.</span><span class="sxs-lookup"><span data-stu-id="4aed7-188">Simple - The ComboBox displays a dropdown list automatically and you can enter a custom value.</span></span>
- <span data-ttu-id="4aed7-189">DropDownList – pole se seznamem funguje stejně jako ovládací prvek DropDownList.</span><span class="sxs-lookup"><span data-stu-id="4aed7-189">DropDownList - The ComboBox works just like a DropDownList control.</span></span>

<span data-ttu-id="4aed7-190">Rozdíly mezi rozevírací seznam a jednoduché je, když se zobrazí seznam položek.</span><span class="sxs-lookup"><span data-stu-id="4aed7-190">The different between DropDown and Simple is when the list of items is displayed.</span></span> <span data-ttu-id="4aed7-191">V případě jednoduchého zobrazí se seznam okamžitě při přesunutí fokusu do pole se seznamem.</span><span class="sxs-lookup"><span data-stu-id="4aed7-191">In the case of Simple, the list is displayed immediately when you move focus to the ComboBox.</span></span> <span data-ttu-id="4aed7-192">V případě rozevírací seznam musíte kliknout na šipku zobrazte seznam položek.</span><span class="sxs-lookup"><span data-stu-id="4aed7-192">In the case of DropDown, you must click the arrow to see the list of items.</span></span>

<span data-ttu-id="4aed7-193">Hodnota DropDownList způsobí, že ovládací prvek ComboBox pracovat stejně jako standardní ovládací prvek DropDownList.</span><span class="sxs-lookup"><span data-stu-id="4aed7-193">The DropDownList value causes the ComboBox control to work just like a standard DropDownList control.</span></span> <span data-ttu-id="4aed7-194">Ale je tady důležitý rozdíl.</span><span class="sxs-lookup"><span data-stu-id="4aed7-194">However, there is an important difference here.</span></span> <span data-ttu-id="4aed7-195">Starší verze aplikace Internet Explorer zobrazit ovládací prvek DropDownList s nekonečnou z-index, proto se ovládací prvek zobrazí před libovolný ovládací prvek umístěn před jeho.</span><span class="sxs-lookup"><span data-stu-id="4aed7-195">Older versions of Internet Explorer display a DropDownList control with an infinite z-index so the control will appear in front of any control placed in front of it.</span></span> <span data-ttu-id="4aed7-196">Vzhledem k tomu, že pole se seznamem vykreslí HTML &lt;div&gt; značek namísto HTML &lt;vyberte&gt; značky, pole se seznamem správně respektuje pořadí z-ordering.</span><span class="sxs-lookup"><span data-stu-id="4aed7-196">Because the ComboBox renders an HTML &lt;div&gt; tag instead of an HTML &lt;select&gt; tag, the ComboBox correctly respects z-ordering.</span></span>

## <a name="setting-the-autocompletemode"></a><span data-ttu-id="4aed7-197">Nastavení vlastnost AutoCompleteMode</span><span class="sxs-lookup"><span data-stu-id="4aed7-197">Setting the AutoCompleteMode</span></span>

<span data-ttu-id="4aed7-198">Chcete-li určit, co se stane, když uživatel zadá text do pole se seznamem použijete vlastnost AutoCompleteMode – pole se seznamem vlastností.</span><span class="sxs-lookup"><span data-stu-id="4aed7-198">You use the ComboBox AutoCompleteMode property to specify what happens when someone types text into the ComboBox.</span></span> <span data-ttu-id="4aed7-199">Tato vlastnost přijímá následující možné hodnoty:</span><span class="sxs-lookup"><span data-stu-id="4aed7-199">This property accepts the following possible values:</span></span>

- <span data-ttu-id="4aed7-200">None – (výchozí hodnota), která pole se seznamem neposkytuje žádné chování automatického dokončení.</span><span class="sxs-lookup"><span data-stu-id="4aed7-200">None - (default value) The ComboBox does not provide any auto-complete behavior.</span></span>
- <span data-ttu-id="4aed7-201">Navrhnout – pole se seznamem se zobrazí v seznamu a zvýrazní odpovídající položku v seznamu (viz obrázek 8).</span><span class="sxs-lookup"><span data-stu-id="4aed7-201">Suggest - The ComboBox displays the list and it highlights the matching item in the list (see Figure 8).</span></span>
- <span data-ttu-id="4aed7-202">Append – pole se seznamem nezobrazuje v seznamu a přidá odpovídající položky ze seznamu do co jste zadali (viz obrázek 9).</span><span class="sxs-lookup"><span data-stu-id="4aed7-202">Append - The ComboBox does not display the list and it appends the matching item from the list onto what you have typed (see Figure 9).</span></span>
- <span data-ttu-id="4aed7-203">SuggestAppend – pole se seznamem se zobrazí v seznamu a přidá odpovídající položky ze seznamu do co jste zadali (viz obrázek 10).</span><span class="sxs-lookup"><span data-stu-id="4aed7-203">SuggestAppend - The ComboBox both displays the list and appends the matching item from the list onto what you have typed (see Figure 10).</span></span>


[![T<span data-ttu-id="4aed7-204">má pole se seznamem umožňuje návrh]</span><span class="sxs-lookup"><span data-stu-id="4aed7-204">he ComboBox makes a suggestion]</span></span>(how-do-i-use-the-combobox-control-vb/_static/image8.jpg)](how-do-i-use-the-combobox-control-vb/_static/image15.png)

<span data-ttu-id="4aed7-205">**Obrázek 08**: Pole se seznamem umožňuje návrh ([kliknutím ji zobrazíte obrázek v plné velikosti](how-do-i-use-the-combobox-control-vb/_static/image16.png))</span><span class="sxs-lookup"><span data-stu-id="4aed7-205">**Figure 08**: The ComboBox makes a suggestion([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image16.png))</span></span>


[![C<span data-ttu-id="4aed7-206">omboBox připojí odpovídající text]</span><span class="sxs-lookup"><span data-stu-id="4aed7-206">omboBox appends matching text]</span></span>(how-do-i-use-the-combobox-control-vb/_static/image9.jpg)](how-do-i-use-the-combobox-control-vb/_static/image17.png)

<span data-ttu-id="4aed7-207">**Obrázek 09**: Pole se seznamem připojí odpovídající text ([kliknutím ji zobrazíte obrázek v plné velikosti](how-do-i-use-the-combobox-control-vb/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="4aed7-207">**Figure 09**: ComboBox appends matching text([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image18.png))</span></span>


[![T<span data-ttu-id="4aed7-208">má pole se seznamem navrhuje a připojí]</span><span class="sxs-lookup"><span data-stu-id="4aed7-208">he ComboBox suggests and appends]</span></span>(how-do-i-use-the-combobox-control-vb/_static/image10.jpg)](how-do-i-use-the-combobox-control-vb/_static/image19.png)

<span data-ttu-id="4aed7-209">**Obrázek 10**: Pole se seznamem navrhuje a připojí ([kliknutím ji zobrazíte obrázek v plné velikosti](how-do-i-use-the-combobox-control-vb/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="4aed7-209">**Figure 10**: The ComboBox suggests and appends([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image20.png))</span></span>


## <a name="summary"></a><span data-ttu-id="4aed7-210">Souhrn</span><span class="sxs-lookup"><span data-stu-id="4aed7-210">Summary</span></span>

<span data-ttu-id="4aed7-211">V tomto kurzu jste zjistili, jak zobrazit pevnou sadu položek pomocí ovládacího prvku ComboBox.</span><span class="sxs-lookup"><span data-stu-id="4aed7-211">In this tutorial, you learned how to use the ComboBox control to display a fixed set of items.</span></span> <span data-ttu-id="4aed7-212">Jsme vázaného ovládacího prvku pole se seznamem, jak na statickou sadu položek a do databázové tabulky.</span><span class="sxs-lookup"><span data-stu-id="4aed7-212">We bound the ComboBox control both to a static set of items and to a database table.</span></span> <span data-ttu-id="4aed7-213">Nakonec jste zjistili, jak upravit nastavením jeho vlastnosti DropDownStyle a vlastnost AutoCompleteMode chování pole se seznamem.</span><span class="sxs-lookup"><span data-stu-id="4aed7-213">Finally, you learned how to modify the behavior of the ComboBox by setting its DropDownStyle and AutoCompleteMode properties.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="4aed7-214">Předchozí</span><span class="sxs-lookup"><span data-stu-id="4aed7-214">Previous</span></span>](how-do-i-use-the-combobox-control-cs.md)
