---
uid: web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-cs
title: Wyzwolenie animacji w inny formant (C#) | Dokumentacja firmy Microsoft
author: wenz
description: "Formantu animacji w zestawie narzędzi programu ASP.NET AJAX formantu nie jest po prostu formantu, ale całego framework do Dodawanie animacji do formantu. Ogólnie rzecz biorąc, uruchamianie..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: e5d99c2b-d8ee-413c-80d5-c120cffb0a4c
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 8d243eebc42b66f1e86b38a1b7531e527144ea7e
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/10/2017
---
<a name="triggering-an-animation-in-another-control-c"></a><span data-ttu-id="90c2a-104">Wyzwolenie animacji w inny formant (C#)</span><span class="sxs-lookup"><span data-stu-id="90c2a-104">Triggering an Animation in another Control (C#)</span></span>
====================
<span data-ttu-id="90c2a-105">przez [Wenz Chrześcijańskie](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="90c2a-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="90c2a-106">[Pobierz kod](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.cs.zip) lub [pobierania plików PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="90c2a-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8CS.pdf)</span></span>

> <span data-ttu-id="90c2a-107">Formantu animacji w zestawie narzędzi programu ASP.NET AJAX formantu nie jest po prostu formantu, ale całego framework do Dodawanie animacji do formantu.</span><span class="sxs-lookup"><span data-stu-id="90c2a-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="90c2a-108">Ogólnie rzecz biorąc uruchomienie animacji zostanie wywołany przez użytkownika za pomocą formantu tego samego.</span><span class="sxs-lookup"><span data-stu-id="90c2a-108">Generally, launching an animation is triggered by user interaction with the same control.</span></span> <span data-ttu-id="90c2a-109">Jest jednak również możliwość interakcji z formantami, a następnie animacji inny formant.</span><span class="sxs-lookup"><span data-stu-id="90c2a-109">It is however also possible to interact with one control and then animation another control.</span></span>


## <a name="overview"></a><span data-ttu-id="90c2a-110">Omówienie</span><span class="sxs-lookup"><span data-stu-id="90c2a-110">Overview</span></span>

<span data-ttu-id="90c2a-111">Formantu animacji w zestawie narzędzi programu ASP.NET AJAX formantu nie jest po prostu formantu, ale całego framework do Dodawanie animacji do formantu.</span><span class="sxs-lookup"><span data-stu-id="90c2a-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="90c2a-112">Ogólnie rzecz biorąc uruchomienie animacji zostanie wywołany przez użytkownika za pomocą formantu tego samego.</span><span class="sxs-lookup"><span data-stu-id="90c2a-112">Generally, launching an animation is triggered by user interaction with the same control.</span></span> <span data-ttu-id="90c2a-113">Jest jednak również możliwość interakcji z formantami, a następnie animacji inny formant.</span><span class="sxs-lookup"><span data-stu-id="90c2a-113">It is however also possible to interact with one control and then animation another control.</span></span>

## <a name="steps"></a><span data-ttu-id="90c2a-114">Kroki</span><span class="sxs-lookup"><span data-stu-id="90c2a-114">Steps</span></span>

<span data-ttu-id="90c2a-115">Po pierwsze, obejmują `ScriptManager` na stronie; następnie biblioteki ASP.NET AJAX został załadowany, dzięki czemu można użyć kontroli zestawu narzędzi:</span><span class="sxs-lookup"><span data-stu-id="90c2a-115">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample1.aspx)]

<span data-ttu-id="90c2a-116">Animacja zostanie zastosowana do panelu tekstu, która wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="90c2a-116">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample2.aspx)]

<span data-ttu-id="90c2a-117">Skojarzone klasy CSS panelu Zdefiniuj kolor tła nieuprzywilejowany i również ustawić stałą szerokość panelu:</span><span class="sxs-lookup"><span data-stu-id="90c2a-117">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](triggering-an-animation-in-another-control-cs/samples/sample3.css)]

<span data-ttu-id="90c2a-118">Aby rozpocząć animacji panelu, przycisk HTML jest używany.</span><span class="sxs-lookup"><span data-stu-id="90c2a-118">In order to start animating the panel, an HTML button is used.</span></span> <span data-ttu-id="90c2a-119">Należy pamiętać, że `<input type="button" />` jest uprzywilejowanym za pośrednictwem `<asp:Button />` ponieważ nie chcemy odświeżania strony po kliknięciu tego przycisku.</span><span class="sxs-lookup"><span data-stu-id="90c2a-119">Note that `<input type="button" />` is favoured over `<asp:Button />` since we do not want a postback when the user clicks on that button.</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample4.aspx)]

<span data-ttu-id="90c2a-120">Następnie należy dodać `AnimationExtender` ze stroną, zapewniając `ID`, `TargetControlID` atrybut i obowiązkowe `runat="server"`.</span><span class="sxs-lookup"><span data-stu-id="90c2a-120">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`.</span></span> <span data-ttu-id="90c2a-121">Ważne jest, aby ustawić `TargetControlID` identyfikator przycisku (element wyzwalania animacji), nie identyfikatorowi panelu (element animowanej)</span><span class="sxs-lookup"><span data-stu-id="90c2a-121">It is important to set `TargetControlID` to the ID of the button (the element triggering the animation), not to the ID of the panel (the element being animated)</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample5.aspx)]

<span data-ttu-id="90c2a-122">W ramach `<Animations>` węzła, animacje miejsce w zwykły sposób.</span><span class="sxs-lookup"><span data-stu-id="90c2a-122">Within the `<Animations>` node, place animations as usual.</span></span> <span data-ttu-id="90c2a-123">Aby je zmienić panelu, ustaw nie przycisk `AnimationTarget` atrybutu dla każdego elementu animacji w `AnimationExtender`.</span><span class="sxs-lookup"><span data-stu-id="90c2a-123">In order to make them change the panel, not the button, set the `AnimationTarget` attribute for every animation element within `AnimationExtender`.</span></span> <span data-ttu-id="90c2a-124">Wartość `AnimationTarget` oczywiście jest Identyfikatorem panelu.</span><span class="sxs-lookup"><span data-stu-id="90c2a-124">The value for `AnimationTarget` is the ID of the panel, of course.</span></span> <span data-ttu-id="90c2a-125">W ten sposób animacji się tak zdarzyć przy użyciu panelu, nie z przyciskiem wyzwalająca.</span><span class="sxs-lookup"><span data-stu-id="90c2a-125">That way, the animations happen with the panel, not with the triggering button.</span></span> <span data-ttu-id="90c2a-126">Oto `AnimationExtender` znaczników dla tego scenariusza:</span><span class="sxs-lookup"><span data-stu-id="90c2a-126">Here is the `AnimationExtender` markup for this scenario:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample6.aspx)]

<span data-ttu-id="90c2a-127">Należy zwrócić uwagę specjalne kolejność poszczególnych animacji.</span><span class="sxs-lookup"><span data-stu-id="90c2a-127">Note the special order in which the individual animations appear.</span></span> <span data-ttu-id="90c2a-128">Przede wszystkim przycisku pobiera dezaktywowane, po uruchomieniu animacji.</span><span class="sxs-lookup"><span data-stu-id="90c2a-128">First of all, the button gets deactivated once the animation runs.</span></span> <span data-ttu-id="90c2a-129">Ponieważ nie `AnimationTarget` atrybutu w `<EnableAction>` elementu, to animacji jest stosowana do formantu źródłowego: przycisku.</span><span class="sxs-lookup"><span data-stu-id="90c2a-129">Since there is no `AnimationTarget` attribute in the `<EnableAction>` element, this animation is applied to the originating control: the button.</span></span> <span data-ttu-id="90c2a-130">Animacja następne dwa kroki przeprowadza się parallelly (`<Parallel>` elementu).</span><span class="sxs-lookup"><span data-stu-id="90c2a-130">The next two animation steps shall be carried out parallelly (`<Parallel>` element).</span></span> <span data-ttu-id="90c2a-131">Mają ich `AnimationTarget` ustawić atrybuty `"Panel1"`, w związku z tym animacji panelu, a nie przycisk.</span><span class="sxs-lookup"><span data-stu-id="90c2a-131">Both have their `AnimationTarget` attributes set to `"Panel1"`, thus animating the panel, not the button.</span></span>


<span data-ttu-id="90c2a-132">[![Kliknięcie przycisku powoduje uruchomienie animacji panelu](triggering-an-animation-in-another-control-cs/_static/image2.png)](triggering-an-animation-in-another-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="90c2a-132">[![A mouse click on the button starts the panel animation](triggering-an-animation-in-another-control-cs/_static/image2.png)](triggering-an-animation-in-another-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="90c2a-133">Kliknięcie przycisku powoduje uruchomienie animacji panelu ([kliknij, aby wyświetlić obraz w pełnym rozmiarze](triggering-an-animation-in-another-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="90c2a-133">A mouse click on the button starts the panel animation ([Click to view full-size image](triggering-an-animation-in-another-control-cs/_static/image3.png))</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="90c2a-134">[Poprzednie](disabling-actions-during-animation-cs.md)
[dalej](modifying-animations-from-the-server-side-cs.md)</span><span class="sxs-lookup"><span data-stu-id="90c2a-134">[Previous](disabling-actions-during-animation-cs.md)
[Next](modifying-animations-from-the-server-side-cs.md)</span></span>