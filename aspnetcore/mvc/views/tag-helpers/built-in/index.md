---
title: ASP.NET Core integrované pomocné rutiny značek
author: pkellner
description: 'Zjistěte, jak ASP.NET Core integrovaných pomocných rutin značek zvýší vaši produktivitu.'
ms.author: riande
ms.custom: mvc
ms.date: 10/10/2018
uid: mvc/views/tag-helpers/builtin-th/Index
---

# <a name="aspnet-core-built-in-tag-helpers"></a><span data-ttu-id="dde25-103">ASP.NET Core integrované pomocné rutiny značek</span><span class="sxs-lookup"><span data-stu-id="dde25-103">ASP.NET Core built-in Tag Helpers</span></span>

<span data-ttu-id="dde25-104">Podle [Peter Kellner](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="dde25-104">By [Peter Kellner](http://peterkellner.net)</span></span>

<span data-ttu-id="dde25-105">Přehled pomocných rutin značek, naleznete v tématu <xref:mvc/views/tag-helpers/intro>.</span><span class="sxs-lookup"><span data-stu-id="dde25-105">For an overview of Tag Helpers, see <xref:mvc/views/tag-helpers/intro>.</span></span>

> [!NOTE]
> <span data-ttu-id="dde25-106">Existují vestavěné pomocných rutin značek, které nebyly popsány v dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="dde25-106">There are built-in Tag Helpers which aren't described in the documentation.</span></span> <span data-ttu-id="dde25-107">Tyto pomocné rutiny značek se používají interně pomocí [Razor](xref:mvc/views/razor) modul zobrazení.</span><span class="sxs-lookup"><span data-stu-id="dde25-107">These Tag Helpers are used internally by the [Razor](xref:mvc/views/razor) view engine.</span></span> <span data-ttu-id="dde25-108">Jedná se o pomocné rutiny značky pro `~` znaku (tilda), které rozšíří kořenová cesta webové stránky.</span><span class="sxs-lookup"><span data-stu-id="dde25-108">This includes a Tag Helper for the `~` (tilde) character, which expands to the root path of the website.</span></span>

## <a name="built-in-aspnet-core-tag-helpers"></a><span data-ttu-id="dde25-109">ASP.NET Core integrované pomocné rutiny značek</span><span class="sxs-lookup"><span data-stu-id="dde25-109">Built-in ASP.NET Core Tag Helpers</span></span>

<span data-ttu-id="dde25-110">**[Ukotvení pomocné rutiny značky](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="dde25-110">**[Anchor Tag Helper](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper)**</span></span>

<span data-ttu-id="dde25-111">**[Pomocné rutiny značky do mezipaměti](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="dde25-111">**[Cache Tag Helper](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)**</span></span>

<span data-ttu-id="dde25-112">**[Pomocná rutina značek v distribuované mezipaměti](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="dde25-112">**[Distributed Cache Tag Helper](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)**</span></span>

<span data-ttu-id="dde25-113">**[Pomocná rutina značky prostředí](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="dde25-113">**[Environment Tag Helper](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)**</span></span>

[comment]: **[FormActionTagHelper](xref:mvc/views/tag-helpers/builtin-th/form-action-tag-helper)**

<span data-ttu-id="dde25-114">**[Pomocná rutina značky formuláře](xref:mvc/views/working-with-forms#the-form-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="dde25-114">**[Form Tag Helper](xref:mvc/views/working-with-forms#the-form-tag-helper)**</span></span>

<span data-ttu-id="dde25-115">**[Pomocná rutina značky obrázku](xref:mvc/views/tag-helpers/builtin-th/image-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="dde25-115">**[Image Tag Helper](xref:mvc/views/tag-helpers/builtin-th/image-tag-helper)**</span></span>

<span data-ttu-id="dde25-116">**[Vstup pomocné rutiny značky](xref:mvc/views/working-with-forms#the-input-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="dde25-116">**[Input Tag Helper](xref:mvc/views/working-with-forms#the-input-tag-helper)**</span></span>

<span data-ttu-id="dde25-117">**[Pomocná rutina značek v popisku](xref:mvc/views/working-with-forms#the-label-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="dde25-117">**[Label Tag Helper](xref:mvc/views/working-with-forms#the-label-tag-helper)**</span></span>

[comment]: **[LinkTagHelper](xref:mvc/views/tag-helpers/builtin-th/link-tag-helper)**

[comment]: **[OptionTagHelper](xref:mvc/views/tag-helpers/builtin-th/option-tag-helper)**

[comment]: **[ScriptTagHelper](xref:mvc/views/tag-helpers/builtin-th/script-tag-helper)**

<span data-ttu-id="dde25-118">**[Pomocná rutina částečné značky](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="dde25-118">**[Partial Tag Helper](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper)**</span></span>

<span data-ttu-id="dde25-119">**[Vyberte pomocné rutiny značky](xref:mvc/views/working-with-forms#the-select-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="dde25-119">**[Select Tag Helper](xref:mvc/views/working-with-forms#the-select-tag-helper)**</span></span>

<span data-ttu-id="dde25-120">**[Pomocná rutina značky TextArea](xref:mvc/views/working-with-forms#the-textarea-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="dde25-120">**[Textarea Tag Helper](xref:mvc/views/working-with-forms#the-textarea-tag-helper)**</span></span>

<span data-ttu-id="dde25-121">**[Pomocná rutina značek v ověřovací zpráva](xref:mvc/views/working-with-forms#the-validation-message-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="dde25-121">**[Validation Message Tag Helper](xref:mvc/views/working-with-forms#the-validation-message-tag-helper)**</span></span>

<span data-ttu-id="dde25-122">**[Pomocná rutina pro ověření Summary – značka](xref:mvc/views/working-with-forms#the-validation-summary-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="dde25-122">**[Validation Summary Tag Helper](xref:mvc/views/working-with-forms#the-validation-summary-tag-helper)**</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dde25-123">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="dde25-123">Additional resources</span></span>

* <xref:mvc/views/tag-helpers/intro>
* <xref:mvc/views/tag-helpers/th-components>
