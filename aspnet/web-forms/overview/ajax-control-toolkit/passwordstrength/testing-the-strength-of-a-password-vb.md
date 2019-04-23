---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
title: Testování síly hesla (VB) | Dokumentace Microsoftu
author: wenz
description: Hesla jsou skoro kdekoli, vyžaduje, aby opožděné uživatelé mívají sklony zvolte jednoduchá hesla, které se podařilo. PasswordStrength ovládacího prvku ASP. N...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 9215a37f-3133-4887-8ed2-3689f3a53551
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
msc.type: authoredcontent
ms.openlocfilehash: fb185c4147d516ab28d632b3e874b6f1d46f6576
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59408417"
---
# <a name="testing-the-strength-of-a-password-vb"></a><span data-ttu-id="98f67-104">Testování síly hesla (VB)</span><span class="sxs-lookup"><span data-stu-id="98f67-104">Testing the Strength of a Password (VB)</span></span>

<span data-ttu-id="98f67-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="98f67-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="98f67-106">[Stáhněte si kód](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.vb.zip) nebo [stahovat PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="98f67-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0VB.pdf)</span></span>

> <span data-ttu-id="98f67-107">Hesla jsou skoro kdekoli, vyžaduje, aby opožděné uživatelé mívají sklony zvolte jednoduchá hesla, které se podařilo.</span><span class="sxs-lookup"><span data-stu-id="98f67-107">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="98f67-108">PasswordStrength ovládacího prvku ASP.NET AJAX Control Toolkit můžete zkontrolovat, jak kvalitní je heslo.</span><span class="sxs-lookup"><span data-stu-id="98f67-108">The PasswordStrength control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>


## <a name="overview"></a><span data-ttu-id="98f67-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="98f67-109">Overview</span></span>

<span data-ttu-id="98f67-110">Hesla jsou skoro kdekoli, vyžaduje, aby opožděné uživatelé mívají sklony zvolte jednoduchá hesla, které se podařilo.</span><span class="sxs-lookup"><span data-stu-id="98f67-110">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="98f67-111">`PasswordStrength` Ovládacího prvku ASP.NET AJAX Control Toolkit můžete zkontrolovat, jak kvalitní je heslo.</span><span class="sxs-lookup"><span data-stu-id="98f67-111">The `PasswordStrength` control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>

## <a name="steps"></a><span data-ttu-id="98f67-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="98f67-112">Steps</span></span>

<span data-ttu-id="98f67-113">`PasswordStrength` Ovládací prvek textové pole rozšiřuje a zkontroluje, zda je heslo v něm dostatečné.</span><span class="sxs-lookup"><span data-stu-id="98f67-113">The `PasswordStrength` control extends a text box and checks whether the password in it is good enough.</span></span> <span data-ttu-id="98f67-114">Nabízí celou řadu možností pomocí atributů Tady jsou některé z nich:</span><span class="sxs-lookup"><span data-stu-id="98f67-114">It offers a wealth of options via attributes; here are just some of them:</span></span>

- <span data-ttu-id="98f67-115">`MinimumNumericCharacters` minimální počet číslic v hesle</span><span class="sxs-lookup"><span data-stu-id="98f67-115">`MinimumNumericCharacters` minimum number of numeric characters required in the password</span></span>
- <span data-ttu-id="98f67-116">`MinimumSymbolCharacters` minimální počet znaků symbolu (ne písmena a číslice) v hesle</span><span class="sxs-lookup"><span data-stu-id="98f67-116">`MinimumSymbolCharacters` minimum number of symbol characters (not letters and digits) required in the password</span></span>
- <span data-ttu-id="98f67-117">`PreferredPasswordLength` Minimální délka hesla</span><span class="sxs-lookup"><span data-stu-id="98f67-117">`PreferredPasswordLength` minimum length of the password</span></span>
- <span data-ttu-id="98f67-118">`RequiresUpperAndLowerCaseCharacters` Určuje, zda heslo musí používat velká a malá písmena</span><span class="sxs-lookup"><span data-stu-id="98f67-118">`RequiresUpperAndLowerCaseCharacters` whether the password needs to use both uppercase and lowercase characters</span></span>

<span data-ttu-id="98f67-119">`StrengthIndicatorType` Poskytuje informace o představení sílu hesla, jako text (hodnota `"Text"`) nebo jako typ indikátoru průběhu (hodnota `"BarIndicator"`).</span><span class="sxs-lookup"><span data-stu-id="98f67-119">The `StrengthIndicatorType` provides the information how to present the strength of the password, as text (value `"Text"`) or as a kind of progress bar (value `"BarIndicator"`).</span></span> <span data-ttu-id="98f67-120">V `DisplayPosition` atribut, můžete nakonfigurovat ve kterém se zobrazí informace.</span><span class="sxs-lookup"><span data-stu-id="98f67-120">In the `DisplayPosition` attribute, you configure where the information appears.</span></span> <span data-ttu-id="98f67-121">Tady je úplný příklad, včetně technologie ASP.NET AJAX `ScriptManager` ovládací prvek, `PasswordStrength` ovládacího prvku a samozřejmě textového pole, ve kterém může uživatel zadat heslo.</span><span class="sxs-lookup"><span data-stu-id="98f67-121">Here is a complete example, including the ASP.NET AJAX `ScriptManager` control, the `PasswordStrength` control and of course a text box where the user may enter a password.</span></span> <span data-ttu-id="98f67-122">Druhé pole je představu, běžného textového pole a pole hesla tak, aby se zobrazí při vývoji co píšete.</span><span class="sxs-lookup"><span data-stu-id="98f67-122">For the sake of demonstration, the latter form field is a regular text field and not a password field so that you can see during development what you are typing.</span></span>

[!code-aspx[Main](testing-the-strength-of-a-password-vb/samples/sample1.aspx)]

<span data-ttu-id="98f67-123">Spuštění stránky a okamžitě zadejte: Poté, co jste zadali, malá písmena, velká písmena, číslice a symboly, heslo se bude považovat za jako nedělitelné.</span><span class="sxs-lookup"><span data-stu-id="98f67-123">Run the page and type away: Only after you have entered lowercase letters, uppercase letters, digits and symbols, the password is deemed as unbreakable .</span></span>


<span data-ttu-id="98f67-124">[![Nyní je (úplně) dobré heslo](testing-the-strength-of-a-password-vb/_static/image2.png)](testing-the-strength-of-a-password-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="98f67-124">[![Now the password is (quite) good](testing-the-strength-of-a-password-vb/_static/image2.png)](testing-the-strength-of-a-password-vb/_static/image1.png)</span></span>

<span data-ttu-id="98f67-125">Nyní je heslo (úplně) dobré ([kliknutím ji zobrazíte obrázek v plné velikosti](testing-the-strength-of-a-password-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="98f67-125">Now the password is (quite) good ([Click to view full-size image](testing-the-strength-of-a-password-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="98f67-126">Předchozí</span><span class="sxs-lookup"><span data-stu-id="98f67-126">Previous</span></span>](testing-the-strength-of-a-password-cs.md)
