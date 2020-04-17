---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: Vytvoření aplikace MVC 3 s břitvou a nenápadným JavaScriptem | Dokumenty společnosti Microsoft
author: rick-anderson
description: Ukázková webová aplikace Seznamu uživatelů ukazuje, jak jednoduché je vytvářet ASP.NET aplikací MVC 3 pomocí modulu zobrazení Razor. Ukázková aplikace s...
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: c57e19f8eeca15e3676b3d490b08f69786d44f93
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542453"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a>Vytvoření aplikace MVC 3 se syntaxí Razor a nerušivým JavaScriptem

podle [společnosti Microsoft](https://github.com/microsoft)

> Ukázková webová aplikace Seznamu uživatelů ukazuje, jak jednoduché je vytvářet ASP.NET aplikací MVC 3 pomocí modulu zobrazení Razor. Ukázková aplikace ukazuje, jak používat nový modul zobrazení Razor s ASP.NET MVC verze 3 a Visual Studio 2010 k vytvoření fiktivního webu seznamu uživatelů, který obsahuje funkce, jako je vytváření, zobrazování, úpravy a odstranění uživatelů.
> 
> Tento kurz popisuje kroky, které byly podniknuty za účelem sestavení ukázky seznamu uživatelů ASP.NET aplikace MVC 3. Projekt sady Visual Studio se zdrojovým kódem jazyka C# a VB je k dispozici jako doprovodný k tomuto tématu: [Stáhnout](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114). Máte-li dotazy týkající se tohoto výukového programu, prosím, po nich na [fóru MVC](https://forums.asp.net/1146.aspx).

## <a name="overview"></a>Přehled

Aplikace, kterou budete vytvářet, je jednoduchý seznam uživatelů webové stránky. Uživatelé mohou zadávat, zobrazovat a aktualizovat informace o uživateli.

![Ukázkový web](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

Můžete si stáhnout VB a C# dokončený projekt [zde](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f).

## <a name="creating-the-web-application"></a>Vytvoření webové aplikace

Chcete-li kurz spustit, otevřete Visual Studio 2010 a vytvořte nový projekt pomocí ASP.NET *šablonu webové aplikace MVC 3.* Pojmenujte &quot;aplikaci Mvc3Razor&quot;.

[![Nový projekt MVC 3](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)

V dialogovém **okně Nový ASP.NET MVC 3 Project** vyberte Možnost **Internetová aplikace**, vyberte modul zobrazení Holicí strojek a klepněte na tlačítko **OK**.

![Nový ASP.NET dialogové okno Projektu MVC 3](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

V tomto kurzu nebudete používat ASP.NET poskytovatele členství, takže můžete odstranit všechny soubory spojené s přihlášením a členstvím. V **Průzkumníku řešení**odeberte následující soubory a adresáře:

- *Řadiče\AccountController*
- *Modely\Modely účtů*
- *Zobrazení\Sdílené\\_LogOnPartial*
- *Zobrazení\Účet* (a všechny soubory v tomto adresáři)

![Soln Exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

Upravte `<div>` `logindisplay` <em>&quot;</em>&quot; <em> \_soubor Layout.cshtml</em> a nahraďte značky uvnitř prvku s názvem Přihlášení zakázáno . Následující příklad ukazuje nové značky:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a>Přidání modelu

V **Průzkumníku řešení**klepněte pravým tlačítkem myši na složku *Modely,* vyberte **přidat**a potom klepněte na příkaz **Třída**.

![Třída Mdl nového uživatele](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

Pojmenujte `UserModel`třídu . Nahraďte obsah souboru *UserModel* následujícím kódem:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

Třída `UserModel` představuje uživatele. Každý člen třídy je anotován s [atributem Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) z oboru názvů [DataAnnotations.](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) Atributy v oboru názvů [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) poskytují automatické ověření na straně klienta a serveru pro webové aplikace.

Otevřete `HomeController` třídu `using` a přidejte direktivu, abyste měli přístup k třídám `UserModel` a: `Users`

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

Hned za `HomeController` deklaraci přidejte následující komentář `Users` a odkaz na třídu:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

Třída `Users` je zjednodušené úložiště dat v paměti, které budete používat v tomto kurzu. V reálné aplikaci byste použili databázi k ukládání informací o uživateli. Prvních několik řádků `HomeController` souboru je zobrazeno v následujícím příkladu:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

Vytvořte aplikaci tak, aby model uživatele bude k dispozici průvodce pomocí posla v dalším kroku.

## <a name="creating-the-default-view"></a>Vytvoření výchozího zobrazení

Dalším krokem je přidání metody akce a zobrazení pro zobrazení uživatelů.

Odstraňte existující *soubor Zobrazení\Domů\Index.* Vytvoříte nový soubor *indexu* pro zobrazení uživatelů.

Ve `HomeController` třídě nahraďte obsah `Index` metody následujícím kódem:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

Klepněte pravým `Index` tlačítkem myši do metody a potom klepněte na příkaz **Přidat zobrazení**.

![Přidat zobrazení](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

Vyberte možnost **Vytvořit zobrazení silného typu.** V **pole Zobrazit třídu dat**vyberte možnost **Mvc3Razor.Models.UserModel**. (Pokud nevidíte **Mvc3Razor.Models.UserModel** v poli **Zobrazit datové třídy,** je třeba vytvořit projekt.) Ujistěte se, že je modul zobrazení nastaven na **břitvu**. Nastavte **obsah zobrazení** na **seznam** a klepněte na tlačítko **Přidat**.

![Přidat zobrazení indexu](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

Nové zobrazení automaticky přilne uživatelskými daty, která `Index` byla předána zobrazení. Zkontrolujte nově generovaný soubor *Zobrazení\Home\Index.* Odkazy **Vytvořit nové**, **Upravit**, **Podrobnosti**a **Odstranit** nefungují, ale zbytek stránky je funkční. Spusťte stránku. Zobrazí se seznam uživatelů.

![Stránka rejstříku](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

Otevřete soubor *Index.cshtml* `ActionLink` a nahraďte značky **pro Úpravy**, **Podrobnosti**a **Odstranit** následujícím kódem:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

Uživatelské jméno se používá jako ID pro vyhledání vybraného záznamu v odkazech **Upravit**, **Podrobnosti**a **Odstranit.**

## <a name="creating-the-details-view"></a>Vytvoření zobrazení podrobností

Dalším krokem je přidání `Details` metody akce a zobrazení pro zobrazení podrobností o uživateli.

![Podrobnosti](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

Do domácího ovladače přidejte následující `Details` metodu:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

Klepněte pravým `Details` tlačítkem myši do metody a pak vyberte <strong>přidat zobrazení</strong>. Ověřte, zda pole <strong>Zobrazit datovou třídu</strong> obsahuje <strong>model Mvc3Razor.Models.UserModel</strong><em>.</em> Nastavte <strong>zobrazení obsahu</strong> na <strong>podrobnosti</strong> a klepněte na tlačítko <strong>Přidat</strong>.

![Přidání zobrazení podrobností](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

Spusťte aplikaci a vyberte odkaz podrobností. Automatické generování uživatelského zařízení zobrazuje každou vlastnost v modelu.

![Podrobnosti](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a>Vytvoření zobrazení úprav

Do domácího ovladače přidejte následující `Edit` metodu.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

Přidejte zobrazení jako v předchozích krocích, ale nastavte **obsah zobrazení** na **Upravit**.

![Přidat zobrazení pro úpravy](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

Spusťte aplikaci a upravte jméno a příjmení jednoho z uživatelů. Pokud porušíte omezení, `DataAnnotation` která byla `UserModel` použita pro třídu, při odeslání formuláře se zobrazí chyby ověření, které jsou vytvářeny kódem serveru. Pokud například změníte křestní &quot;&quot; jméno &quot;&quot;Ann na A , zobrazí se ve formuláři následující chyba:

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

V tomto kurzu považujete uživatelské jméno za primární klíč. Proto vlastnost uživatelského jména nelze změnit. V souboru *Edit.cshtml* nastavte `Html.BeginForm` uživatelské jméno jako skryté pole. To způsobí, že vlastnost, která má být předána v modelu. Následující fragment kódu ukazuje umístění `Hidden` příkazu:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

`TextBoxFor` Nahraďte `ValidationMessageFor` a značky pro `DisplayFor` uživatelské jméno voláním. Metoda `DisplayFor` zobrazí vlastnost jako prvek jen pro čtení. Následující příklad ukazuje dokončené značky. Původní `TextBoxFor` a `ValidationMessageFor` volání jsou komentoval se břitva start-komentář`@* *@`a end-komentář znaky ( )

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a>Povolení ověřování na straně klienta

Chcete-li povolit ověření na straně klienta v ASP.NET MVC 3, musíte nastavit dva příznaky a musíte zahrnout tři soubory JavaScriptu.

Otevřete soubor *Web.config* aplikace. Ověřte `that ClientValidationEnabled` a `UnobtrusiveJavaScriptEnabled` jsou nastaveny na hodnotu true v nastavení aplikace. Následující fragment z kořenového souboru *Web.config* zobrazuje správné nastavení:

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

Nastavení `UnobtrusiveJavaScriptEnabled` na hodnotu true umožňuje nenápadné ověřování klienta Ajax a nenápadný klient. Při použití nenápadné ověření, ověřovací pravidla se změní na atributy HTML5. Názvy atributů HTML5 se mohou skládat pouze z malých písmen, čísel a pomlček.

Nastavení `ClientValidationEnabled` na hodnotu true umožňuje ověření na straně klienta. Nastavením těchto klíčů v souboru *Web.config* aplikace povolíte ověření klienta a nenápadný JavaScript pro celou aplikaci. Tato nastavení můžete také povolit nebo zakázat v jednotlivých zobrazeních nebo v metodách kontroleru pomocí následujícího kódu:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

Do vykresleného zobrazení je také nutné zahrnout několik souborů JavaScriptu. Snadný způsob, jak zahrnout JavaScript do všech zobrazení, je přidat jej do souboru *Views\Shared\\_Layout.cshtml.* Nahraďte `<head>` prvek souboru * \_Layout.cshtml* následujícím kódem:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

První dva skripty jQuery jsou hostovány sítí CDN (Microsoft Ajax Content Delivery Network). Využitím microsoft ajax CDN, můžete výrazně zlepšit první přístupů výkon vašich aplikací.

Spusťte aplikaci a klepněte na odkaz pro úpravy. Zobrazení zdroje stránky v prohlížeči. Zdroj prohlížeče zobrazuje mnoho atributů `data-val` formuláře (pro ověření dat). Pokud je povoleno ověření klienta a nenápadný JavaScript, vstupní pole `data-val="true"` s pravidlem ověření klienta obsahují atribut pro aktivaci nenápadného ověření klienta. Například `City` pole v modelu bylo dekorováno atributem [Required,](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) což má za následek html zobrazený v následujícím příkladu:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

Pro každé pravidlo ověření klienta je přidán `data-val-rulename="message"`atribut, který má formulář . Pomocí `City` předchozího příkladu pole vygeneruje požadované `data-val-required` pravidlo ověření &quot;klienta atribut&quot;a zprávu Pole Město je povinné . Spusťte aplikaci, upravte jednoho `City` z uživatelů a zrušte zaškrtnutí pole. Při out mimo pole se zobrazí chybová zpráva ověření na straně klienta.

![Město požadováno](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

Podobně pro každý parametr v pravidle ověření klienta je přidán `data-val-rulename-paramname=paramvalue`atribut, který má formulář . Například `FirstName` vlastnost je anotována atributem [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) a určuje minimální délku 3 a maximální délku 8. Pojmenované ověřovací pravidlo `length` dat má `max` název parametru a hodnotu parametru 8. Následující text ukazuje kód HTML, `FirstName` který je generován pro pole při úpravě jednoho z uživatelů:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

Další informace o nenápadném ověření klienta naleznete v položce [Unobtrusive Client Validation in ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) v blogu Brada Wilsona.

> [!NOTE]
> V ASP.NET MVC 3 Beta, někdy budete muset odeslat formulář, aby bylo možné spustit ověření na straně klienta. To může být změněno pro konečnou verzi.

## <a name="creating-the-create-view"></a>Vytvoření zobrazení vytvoření

Dalším krokem je přidání `Create` metody a zobrazení akce, aby uživatel mohl vytvořit nového uživatele. Do domácího ovladače přidejte následující `Create` metodu:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

Přidejte zobrazení jako v předchozích krocích, ale nastavte **obsah zobrazení** na **Vytvořit**.

![Create View](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

Spusťte aplikaci, vyberte odkaz **Vytvořit** a přidejte nového uživatele. Metoda `Create` automaticky využívá ověřování na straně klienta a serveru. Pokuste se zadat uživatelské jméno, které &quot;obsahuje&quot;prázdné znaky, například Ben X . Při vybočování karty z pole uživatelského`White space is not allowed`jména se zobrazí chyba ověření na straně klienta ( ).

## <a name="add-the-delete-method"></a>Přidat metodu Delete

Chcete-li kurz dokončit, `Delete` přidejte do domácího ovladače následující metodu:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

Přidejte `Delete` zobrazení jako v předchozích krocích a **nastavíte možnost Odstranit obsah zobrazení** . **Delete**

![Odstranit zobrazení](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

Nyní máte jednoduchou, ale plně funkční aplikaci ASP.NET MVC 3 s ověřením.
