---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
title: "Tworzenie liczbowe w górę/dół formantu z zaplecze usługi sieci Web (VB) | Dokumentacja firmy Microsoft"
author: wenz
description: "Zamiast czekać na użytkownika, wpisz wartość w pole wyboru, liczbowe góra/dół formantu (znajdującego się w systemach Windows i innych systemów operacyjnych) może okazać się c w więcej..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: afa59dfa-fef1-43d3-8fdd-aea3be36ed3c
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
msc.type: authoredcontent
ms.openlocfilehash: 5ceefd6c18761c2abe3f3a4298d340642a0951d6
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/10/2017
---
<a name="creating-a-numeric-updown-control-with-a-web-service-backend-vb"></a><span data-ttu-id="9a5db-103">Tworzenie liczbowe formantu góra/dół z zaplecze usługi sieci Web (VB)</span><span class="sxs-lookup"><span data-stu-id="9a5db-103">Creating a Numeric Up/Down Control with a Web Service Backend (VB)</span></span>
====================
<span data-ttu-id="9a5db-104">przez [Wenz Chrześcijańskie](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="9a5db-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="9a5db-105">[Pobierz kod](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.vb.zip) lub [pobierania plików PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="9a5db-105">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1VB.pdf)</span></span>

> <span data-ttu-id="9a5db-106">Zamiast czekać na użytkownika, wpisz wartość w pole wyboru, liczbowe w górę/dół formantu (znajdującego się w systemach Windows i innymi systemami operacyjnymi) może okazać się za bardziej wygodne.</span><span class="sxs-lookup"><span data-stu-id="9a5db-106">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="9a5db-107">Domyślnie numericupdown — formant zawsze zwiększa lub zmniejsza wartość 1, ale okaże się większą elastyczność i usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="9a5db-107">By default, the NumericUpDown control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>


## <a name="overview"></a><span data-ttu-id="9a5db-108">Omówienie</span><span class="sxs-lookup"><span data-stu-id="9a5db-108">Overview</span></span>

<span data-ttu-id="9a5db-109">Zamiast czekać na użytkownika, wpisz wartość w pole wyboru, liczbowe w górę/dół formantu (znajdującego się w systemach Windows i innymi systemami operacyjnymi) może okazać się za bardziej wygodne.</span><span class="sxs-lookup"><span data-stu-id="9a5db-109">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="9a5db-110">Domyślnie `NumericUpDown` formant zawsze zwiększa lub zmniejsza wartość 1, ale okaże się większą elastyczność i usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="9a5db-110">By default, the `NumericUpDown` control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>

## <a name="steps"></a><span data-ttu-id="9a5db-111">Kroki</span><span class="sxs-lookup"><span data-stu-id="9a5db-111">Steps</span></span>

<span data-ttu-id="9a5db-112">Zawiera zestawie narzędzi programu ASP.NET AJAX kontroli `NumericUpDown` rozszerzeń, które automatycznie dodaje dwa przyciski do pola tekstowego: jeden dla zwiększenie jego wartości, jeden dla zmniejszenie go.</span><span class="sxs-lookup"><span data-stu-id="9a5db-112">The ASP.NET AJAX Control Toolkit contains the `NumericUpDown` extender which automatically adds two buttons to a text box: One for increasing its value, one for decreasing it.</span></span> <span data-ttu-id="9a5db-113">Jednak formant obsługuje również wywołania usługi sieci web (lub wywołanie metody strony).</span><span class="sxs-lookup"><span data-stu-id="9a5db-113">However the control also supports a web service call (or page method call).</span></span> <span data-ttu-id="9a5db-114">Zawsze, gdy w górę lub w dół przycisk zostanie kliknięty, JavaScript, kod łączy się z serwerem sieci web i wykonuje metodę istnieje.</span><span class="sxs-lookup"><span data-stu-id="9a5db-114">Whenever the up or down button is clicked, the JavaScript code connects to the web server and executes a method there.</span></span> <span data-ttu-id="9a5db-115">Podpis metody jest następujące:</span><span class="sxs-lookup"><span data-stu-id="9a5db-115">The method signature is the following one:</span></span>

[!code-vb[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample1.vb)]

<span data-ttu-id="9a5db-116">`current` Argument jest bieżąca wartość w polu tekstowym; `tag` atrybut jest dodatkowy kontekst danych, które można ustawić jako właściwość `NumericUpDown` rozszerzeń (ale nie jest wymagane).</span><span class="sxs-lookup"><span data-stu-id="9a5db-116">The `current` argument is the current value in the text box; the `tag` attribute is additional context data that can be set as a property of the `NumericUpDown` extender (but is not required).</span></span>

<span data-ttu-id="9a5db-117">Dla tego przykładu liczbowe w górę/dół formantu tylko Zezwalaj wartości, które są potęgami liczby dwa: 1, 2, 4, 8, 16, 32, 64 i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="9a5db-117">For this sample, the numeric up/down control shall only allow values that are powers of two: 1, 2, 4, 8, 16, 32, 64, and so on.</span></span> <span data-ttu-id="9a5db-118">W związku z tym metoda wykonywać, gdy użytkownik chce zwiększyć wartość musi dokładnie stara wartość; inne metody Podziel wartość przez dwa.</span><span class="sxs-lookup"><span data-stu-id="9a5db-118">Therefore, the method executed when the user wants to increase the value must double the old value; the other method must divide value by two.</span></span> <span data-ttu-id="9a5db-119">Dlatego jest tutaj usługę sieci web zakończenie:</span><span class="sxs-lookup"><span data-stu-id="9a5db-119">So here is the complete web service:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample2.aspx)]

<span data-ttu-id="9a5db-120">Na koniec Utwórz nową stronę ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9a5db-120">Finally, create a new ASP.NET page.</span></span> <span data-ttu-id="9a5db-121">Jak zwykle należy `ScriptManager` kontroli, `TextBox` kontroli i `NumericUpDownExtender` kontroli.</span><span class="sxs-lookup"><span data-stu-id="9a5db-121">As usual, you need a `ScriptManager` control, a `TextBox` control and a `NumericUpDownExtender` control.</span></span> <span data-ttu-id="9a5db-122">W przypadku drugiego nagłówka musisz podać informacje o usłudze sieci web:</span><span class="sxs-lookup"><span data-stu-id="9a5db-122">For the latter, you have to provide the web service information:</span></span>

- <span data-ttu-id="9a5db-123">`ServiceDownMethod`Nazwa w dół sieci web — metoda lub strona — Metoda</span><span class="sxs-lookup"><span data-stu-id="9a5db-123">`ServiceDownMethod` name of the down web method or page method</span></span>
- <span data-ttu-id="9a5db-124">`ServiceDownPath`Ścieżka do usługi sieci web z dół metody usługi; pominąć, jeśli używana jest metoda strony</span><span class="sxs-lookup"><span data-stu-id="9a5db-124">`ServiceDownPath` path to the web service with the down service method; omit if you are using a page method</span></span>
- <span data-ttu-id="9a5db-125">`ServiceUpMethod`Nazwa pracy sieci web — metoda lub strona — Metoda</span><span class="sxs-lookup"><span data-stu-id="9a5db-125">`ServiceUpMethod` name of the up web method or page method</span></span>
- <span data-ttu-id="9a5db-126">`ServiceUpPath`Ścieżka do usługi sieci web z się metody usługi; pominąć, jeśli używana jest metoda strony</span><span class="sxs-lookup"><span data-stu-id="9a5db-126">`ServiceUpPath` path to the web service with the up service method; omit if you are using a page method</span></span>

<span data-ttu-id="9a5db-127">W tym miejscu jest pełny kod znaczników dla strony:</span><span class="sxs-lookup"><span data-stu-id="9a5db-127">Here is the complete markup for the page:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample3.aspx)]

<span data-ttu-id="9a5db-128">Po uruchomieniu strony, zwróć uwagę, jak wartość w polu tekstowym zawsze podwaja podczas kliknij przycisk górny, a po kliknięciu przycisku niższe, jest dwukrotnie mniejsza.</span><span class="sxs-lookup"><span data-stu-id="9a5db-128">If you run the page, notice how the value in the text box always doubles when you click on the upper button, and is halved when you click on the lower button.</span></span>


<span data-ttu-id="9a5db-129">[![Są wyświetlane tylko cyfry, które są potęgami liczby 2](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9a5db-129">[![Only numbers that are a power of 2 appear](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image1.png)</span></span>

<span data-ttu-id="9a5db-130">Są wyświetlane tylko cyfry, które są potęgami liczby 2 ([kliknij, aby wyświetlić obraz w pełnym rozmiarze](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="9a5db-130">Only numbers that are a power of 2 appear ([Click to view full-size image](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image3.png))</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="9a5db-131">Poprzednie</span><span class="sxs-lookup"><span data-stu-id="9a5db-131">Previous</span></span>](creating-a-numeric-up-down-control-with-a-web-service-backend-cs.md)