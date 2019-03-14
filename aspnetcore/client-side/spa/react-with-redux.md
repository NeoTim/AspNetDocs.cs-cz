---
title: Šablona projektu React s Redux pomocí ASP.NET Core
author: SteveSandersonMS
description: Zjistěte, jak začít pracovat s ASP.NET Core jedné stránky aplikace (SPA) šablona projektu pro React s Reduxem a vytvořit aplikaci react.
monikerRange: '>= aspnetcore-2.1'
ms.author: scaddie
ms.custom: mvc
ms.date: 02/13/2019
uid: spa/react-with-redux
ms.openlocfilehash: ed2e9aea449ddb09fef049a391f40f57452786a8
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57067162"
---
# <a name="use-the-react-with-redux-project-template-with-aspnet-core"></a><span data-ttu-id="0bbc2-103">Šablona projektu React s Redux pomocí ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="0bbc2-103">Use the React-with-Redux project template with ASP.NET Core</span></span>

<span data-ttu-id="0bbc2-104">Aktualizovaná šablona projektu React s Reduxem poskytuje příhodný výchozí bod pro aplikace ASP.NET Core pomocí React, Reduxem, a [vytvořit aplikaci react](https://github.com/facebookincubator/create-react-app) konvence (CRA) k implementaci bohatě vybaveným a na straně klienta uživatelské rozhraní (UI).</span><span class="sxs-lookup"><span data-stu-id="0bbc2-104">The updated React-with-Redux project template provides a convenient starting point for ASP.NET Core apps using React, Redux, and [create-react-app](https://github.com/facebookincubator/create-react-app) (CRA) conventions to implement a rich, client-side user interface (UI).</span></span>

<span data-ttu-id="0bbc2-105">S výjimkou příkazu pro vytvoření projektu všechny informace o šabloně React s Redux je stejný jako šablona React.</span><span class="sxs-lookup"><span data-stu-id="0bbc2-105">With the exception of the project creation command, all information about the React-with-Redux template is the same as the React template.</span></span> <span data-ttu-id="0bbc2-106">Chcete-li vytvořit tento typ projektu, spusťte `dotnet new reactredux` místo `dotnet new react`.</span><span class="sxs-lookup"><span data-stu-id="0bbc2-106">To create this project type, run `dotnet new reactredux` instead of `dotnet new react`.</span></span> <span data-ttu-id="0bbc2-107">Další informace o funkcích, které jsou společné pro obě šablony založené na React najdete v tématu [React dokumentaci k šabloně](xref:spa/react).</span><span class="sxs-lookup"><span data-stu-id="0bbc2-107">For more information about the functionality common to both React-based templates, see [React template documentation](xref:spa/react).</span></span>

<span data-ttu-id="0bbc2-108">Informace o konfiguraci React s Redux dílčí aplikace ve službě IIS najdete v tématu [2.1 šablony ReactRedux: Nelze použít jednostránková aplikace ve službě IIS (aspnet/Šablonování &num;555)](https://github.com/aspnet/Templating/issues/555).</span><span class="sxs-lookup"><span data-stu-id="0bbc2-108">For information on configuring a React-with-Redux sub-application in IIS, see [ReactRedux Template 2.1: Unable to use SPA on IIS (aspnet/Templating &num;555)](https://github.com/aspnet/Templating/issues/555).</span></span>
