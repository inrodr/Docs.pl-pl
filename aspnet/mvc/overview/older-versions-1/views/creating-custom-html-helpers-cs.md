---
uid: aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: "Tworzenie niestandardowych HTML wątków (C#) | Dokumentacja firmy Microsoft"
author: microsoft
description: "Celem tego samouczka jest aby zademonstrować, jak utworzyć niestandardowe pomocników HTML używanej w ramach widoków MVC. Dzięki wykorzystaniu pomocnika kodu HTML..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/07/2008
ms.topic: article
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: a0b6d67eb7aab51ba2b422fab0788e34255f2c8c
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/10/2017
---
<a name="creating-custom-html-helpers-c"></a><span data-ttu-id="ccd56-104">Tworzenie niestandardowych HTML wątków (C#)</span><span class="sxs-lookup"><span data-stu-id="ccd56-104">Creating Custom HTML Helpers (C#)</span></span>
====================
<span data-ttu-id="ccd56-105">przez [firmy Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="ccd56-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="ccd56-106">Pobierz plik PDF</span><span class="sxs-lookup"><span data-stu-id="ccd56-106">Download PDF</span></span>](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> <span data-ttu-id="ccd56-107">Celem tego samouczka jest aby zademonstrować, jak utworzyć niestandardowe pomocników HTML używanej w ramach widoków MVC.</span><span class="sxs-lookup"><span data-stu-id="ccd56-107">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="ccd56-108">Dzięki wykorzystaniu pomocników HTML, można zmniejszyć ilość wpisywania niewygodny tagów HTML, że należy wykonać, aby utworzyć standardowej strony HTML.</span><span class="sxs-lookup"><span data-stu-id="ccd56-108">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>


<span data-ttu-id="ccd56-109">Celem tego samouczka jest aby zademonstrować, jak utworzyć niestandardowe pomocników HTML używanej w ramach widoków MVC.</span><span class="sxs-lookup"><span data-stu-id="ccd56-109">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="ccd56-110">Dzięki wykorzystaniu pomocników HTML, można zmniejszyć ilość wpisywania niewygodny tagów HTML, że należy wykonać, aby utworzyć standardowej strony HTML.</span><span class="sxs-lookup"><span data-stu-id="ccd56-110">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="ccd56-111">W pierwszej części tego samouczka I opisano niektóre z istniejących pomocników HTML dołączonego platformę ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="ccd56-111">In the first part of this tutorial, I describe some of the existing HTML Helpers included with the ASP.NET MVC framework.</span></span> <span data-ttu-id="ccd56-112">Następnie I opisano dwie metody tworzenia niestandardowych pomocników HTML: opisano sposób tworzenia niestandardowych pomocników HTML, tworząc metody statycznej i tworząc — metoda rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="ccd56-112">Next, I describe two methods of creating custom HTML Helpers: I explain how to create custom HTML Helpers by creating a static method and by creating an extension method.</span></span>

## <a name="understanding-html-helpers"></a><span data-ttu-id="ccd56-113">Opis pomocników HTML</span><span class="sxs-lookup"><span data-stu-id="ccd56-113">Understanding HTML Helpers</span></span>

<span data-ttu-id="ccd56-114">Pomocnik kodu HTML jest po prostu metodę, która zwraca wartość typu ciąg.</span><span class="sxs-lookup"><span data-stu-id="ccd56-114">An HTML Helper is just a method that returns a string.</span></span> <span data-ttu-id="ccd56-115">Ten ciąg może reprezentować dowolnego typu zawartości, którą chcesz.</span><span class="sxs-lookup"><span data-stu-id="ccd56-115">The string can represent any type of content that you want.</span></span> <span data-ttu-id="ccd56-116">Na przykład można użyć pomocników HTML do renderowania standardowych znaczników HTML, takich jak HTML `<input>` i `<img>` tagów.</span><span class="sxs-lookup"><span data-stu-id="ccd56-116">For example, you can use HTML Helpers to render standard HTML tags like HTML `<input>` and `<img>` tags.</span></span> <span data-ttu-id="ccd56-117">Możesz również użyć pomocników HTML do renderowania zawartości bardziej złożonych, takie jak paska karty lub tabeli HTML danych bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ccd56-117">You also can use HTML Helpers to render more complex content such as a tab strip or an HTML table of database data.</span></span>

<span data-ttu-id="ccd56-118">Platforma ASP.NET MVC zawiera następujący zestaw standardowych pomocników HTML (nie jest to pełna lista):</span><span class="sxs-lookup"><span data-stu-id="ccd56-118">The ASP.NET MVC framework includes the following set of standard HTML Helpers (this is not a complete list):</span></span>

- <span data-ttu-id="ccd56-119">Html.ActionLink()</span><span class="sxs-lookup"><span data-stu-id="ccd56-119">Html.ActionLink()</span></span>
- <span data-ttu-id="ccd56-120">Html.BeginForm()</span><span class="sxs-lookup"><span data-stu-id="ccd56-120">Html.BeginForm()</span></span>
- <span data-ttu-id="ccd56-121">Html.CheckBox()</span><span class="sxs-lookup"><span data-stu-id="ccd56-121">Html.CheckBox()</span></span>
- <span data-ttu-id="ccd56-122">Html.DropDownList()</span><span class="sxs-lookup"><span data-stu-id="ccd56-122">Html.DropDownList()</span></span>
- <span data-ttu-id="ccd56-123">Html.EndForm()</span><span class="sxs-lookup"><span data-stu-id="ccd56-123">Html.EndForm()</span></span>
- <span data-ttu-id="ccd56-124">Html.Hidden()</span><span class="sxs-lookup"><span data-stu-id="ccd56-124">Html.Hidden()</span></span>
- <span data-ttu-id="ccd56-125">Html.ListBox()</span><span class="sxs-lookup"><span data-stu-id="ccd56-125">Html.ListBox()</span></span>
- <span data-ttu-id="ccd56-126">Html.Password()</span><span class="sxs-lookup"><span data-stu-id="ccd56-126">Html.Password()</span></span>
- <span data-ttu-id="ccd56-127">Html.RadioButton()</span><span class="sxs-lookup"><span data-stu-id="ccd56-127">Html.RadioButton()</span></span>
- <span data-ttu-id="ccd56-128">Html.TextArea()</span><span class="sxs-lookup"><span data-stu-id="ccd56-128">Html.TextArea()</span></span>
- <span data-ttu-id="ccd56-129">Html.TextBox()</span><span class="sxs-lookup"><span data-stu-id="ccd56-129">Html.TextBox()</span></span>

<span data-ttu-id="ccd56-130">Rozważmy na przykład formularz wyświetlania 1.</span><span class="sxs-lookup"><span data-stu-id="ccd56-130">For example, consider the form in Listing 1.</span></span> <span data-ttu-id="ccd56-131">Ten formularz jest renderowany przy użyciu dwóch standardowe pomocników HTML (zobacz rysunek 1).</span><span class="sxs-lookup"><span data-stu-id="ccd56-131">This form is rendered with the help of two of the standard HTML Helpers (see Figure 1).</span></span> <span data-ttu-id="ccd56-132">Ten formularz używa `Html.BeginForm()` i `Html.TextBox()` metody pomocnicze do renderowania prostego formularza HTML.</span><span class="sxs-lookup"><span data-stu-id="ccd56-132">This form uses the `Html.BeginForm()` and `Html.TextBox()` Helper methods to render a simple HTML form.</span></span>


<span data-ttu-id="ccd56-133">[![Strona jest odwzorowywany z pomocników HTML](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ccd56-133">[![Page rendered with HTML Helpers](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span></span>

<span data-ttu-id="ccd56-134">**Rysunek 01**: strona odwzorowywany z pomocników HTML ([kliknij, aby wyświetlić obraz w pełnym rozmiarze](creating-custom-html-helpers-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="ccd56-134">**Figure 01**: Page rendered with HTML Helpers ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image3.png))</span></span>


<span data-ttu-id="ccd56-135">**1 — Lista`Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="ccd56-135">**Listing 1 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

<span data-ttu-id="ccd56-136">Metoda pomocnicza Html.BeginForm() służy do tworzenia HTML otwierający i zamykający `<form>` tagów.</span><span class="sxs-lookup"><span data-stu-id="ccd56-136">The Html.BeginForm() Helper method is used to create the opening and closing HTML `<form>` tags.</span></span> <span data-ttu-id="ccd56-137">Zwróć uwagę, że `Html.BeginForm()` metoda jest wywoływana w za pomocą instrukcji.</span><span class="sxs-lookup"><span data-stu-id="ccd56-137">Notice that the `Html.BeginForm()` method is called within a using statement.</span></span> <span data-ttu-id="ccd56-138">Za pomocą instrukcji upewnia się, że `<form>` tag zostanie zamknięty na końcu przy użyciu bloku.</span><span class="sxs-lookup"><span data-stu-id="ccd56-138">The using statement ensures that the `<form>` tag gets closed at the end of the using block.</span></span>

<span data-ttu-id="ccd56-139">Jeśli wolisz, zamiast tworzyć przy użyciu bloku, należy wywołać metodę pomocnika Html.EndForm(), aby zamknąć `<form>` tagu.</span><span class="sxs-lookup"><span data-stu-id="ccd56-139">If you prefer, instead of creating a using block, you can call the Html.EndForm() Helper method to close the `<form>` tag.</span></span> <span data-ttu-id="ccd56-140">Użyj innego podejścia do tworzenia, otwierania i zamykania `<form>` tag, który wydaje się najbardziej intuicyjny.</span><span class="sxs-lookup"><span data-stu-id="ccd56-140">Use whichever approach to creating an opening and closing `<form>` tag that seems most intuitive to you.</span></span>

<span data-ttu-id="ccd56-141">`Html.TextBox()` Metody pomocnicze są używane w wyświetlania 1 do renderowania elementów HTML `<input>` tagów.</span><span class="sxs-lookup"><span data-stu-id="ccd56-141">The `Html.TextBox()` Helper methods are used in Listing 1 to render HTML `<input>` tags.</span></span> <span data-ttu-id="ccd56-142">W przypadku wybrania Wyświetl źródło w przeglądarce, a następnie wyświetlić źródło HTML w wyświetlania 2.</span><span class="sxs-lookup"><span data-stu-id="ccd56-142">If you select view source in your browser then you see the HTML source in Listing 2.</span></span> <span data-ttu-id="ccd56-143">Zwróć uwagę, że źródło zawiera standardowych znaczników HTML.</span><span class="sxs-lookup"><span data-stu-id="ccd56-143">Notice that the source contains standard HTML tags.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ccd56-144">Zwróć uwagę, że `Html.TextBox()`-HTML pomocnika jest odwzorowywany z `<%= %>` znaczniki zamiast `<% %>` tagów.</span><span class="sxs-lookup"><span data-stu-id="ccd56-144">notice that the `Html.TextBox()`-HTML Helper is rendered with `<%= %>` tags instead of `<% %>` tags.</span></span> <span data-ttu-id="ccd56-145">Jeśli nie zawiera znaku równości, następnie nic nie pobiera renderowane w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="ccd56-145">If you don't include the equal sign, then nothing gets rendered to the browser.</span></span>

<span data-ttu-id="ccd56-146">Platforma ASP.NET MVC zawiera niewielki zestaw pomocników.</span><span class="sxs-lookup"><span data-stu-id="ccd56-146">The ASP.NET MVC framework contains a small set of helpers.</span></span> <span data-ttu-id="ccd56-147">Prawdopodobnie należy rozszerzyć struktura MVC z niestandardowych pomocników HTML.</span><span class="sxs-lookup"><span data-stu-id="ccd56-147">Most likely, you will need to extend the MVC framework with custom HTML Helpers.</span></span> <span data-ttu-id="ccd56-148">W pozostałej części tego samouczka dowiesz się dwie metody tworzenia niestandardowych pomocników HTML.</span><span class="sxs-lookup"><span data-stu-id="ccd56-148">In the remainder of this tutorial, you learn two methods of creating custom HTML Helpers.</span></span>

<span data-ttu-id="ccd56-149">**2 — Lista`Index.aspx Source`**</span><span class="sxs-lookup"><span data-stu-id="ccd56-149">**Listing 2 – `Index.aspx Source`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a><span data-ttu-id="ccd56-150">Tworzenie pomocników HTML za pomocą metod statycznych</span><span class="sxs-lookup"><span data-stu-id="ccd56-150">Creating HTML Helpers with Static Methods</span></span>

<span data-ttu-id="ccd56-151">Najprostszym sposobem tworzenia nowego pomocnika kodu HTML jest Tworzenie statycznej metody, która zwraca wartość typu ciąg.</span><span class="sxs-lookup"><span data-stu-id="ccd56-151">The easiest way to create a new HTML Helper is to create a static method that returns a string.</span></span> <span data-ttu-id="ccd56-152">Załóżmy na przykład użytkownik chce utworzyć nowe pomocnika kodu HTML, który renderuje HTML `<label>` tagu.</span><span class="sxs-lookup"><span data-stu-id="ccd56-152">Imagine, for example, that you decide to create a new HTML Helper that renders an HTML `<label>` tag.</span></span> <span data-ttu-id="ccd56-153">Klasa w 2 wyświetlania służy do renderowania `<label>` .</span><span class="sxs-lookup"><span data-stu-id="ccd56-153">You can use the class in Listing 2 to render a `<label>` .</span></span>

<span data-ttu-id="ccd56-154">**2 — Lista`Helpers\LabelHelper.cs`**</span><span class="sxs-lookup"><span data-stu-id="ccd56-154">**Listing 2 – `Helpers\LabelHelper.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

<span data-ttu-id="ccd56-155">Nie ma nic specjalne informacje o klasie wyświetlania 2.</span><span class="sxs-lookup"><span data-stu-id="ccd56-155">There is nothing special about the class in Listing 2.</span></span> <span data-ttu-id="ccd56-156">`Label()` Metoda po prostu zwraca ciąg.</span><span class="sxs-lookup"><span data-stu-id="ccd56-156">The `Label()` method simply returns a string.</span></span>

<span data-ttu-id="ccd56-157">Używa zmodyfikowany widok indeksu w 3 wyświetlania `LabelHelper` do renderowania elementów HTML `<label>` tagów.</span><span class="sxs-lookup"><span data-stu-id="ccd56-157">The modified Index view in Listing 3 uses the `LabelHelper` to render HTML `<label>` tags.</span></span> <span data-ttu-id="ccd56-158">Należy zauważyć, że zawiera on `<%@ imports %>` dyrektywy, który importuje `Application1.Helpers` przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="ccd56-158">Notice that the view includes an `<%@ imports %>` directive that imports the `Application1.Helpers` namespace.</span></span>

<span data-ttu-id="ccd56-159">**2 — Lista`Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="ccd56-159">**Listing 2 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a><span data-ttu-id="ccd56-160">Tworzenie pomocników HTML za pomocą metody rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="ccd56-160">Creating HTML Helpers with Extension Methods</span></span>

<span data-ttu-id="ccd56-161">Jeśli chcesz utworzyć pomocników HTML, które działają podobnie jak standardowy pomocników HTML dołączony platformy ASP.NET MVC, a następnie musisz utworzyć metody rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="ccd56-161">If you want to create HTML Helpers that work just like the standard HTML Helpers included in the ASP.NET MVC framework then you need to create extension methods.</span></span> <span data-ttu-id="ccd56-162">Metody rozszerzenia umożliwiają dodanie nowych metod do istniejącej klasy.</span><span class="sxs-lookup"><span data-stu-id="ccd56-162">Extension methods enable you to add new methods to an existing class.</span></span> <span data-ttu-id="ccd56-163">Podczas tworzenia metody pomocnika kodu HTML, możesz dodać nowe metody klasy HtmlHelper reprezentowany przez właściwości Html widoku.</span><span class="sxs-lookup"><span data-stu-id="ccd56-163">When creating an HTML Helper method, you add new methods to the HtmlHelper class represented by a view's Html property.</span></span>

<span data-ttu-id="ccd56-164">Klasa w 3 wyświetlania dodaje metodę rozszerzenia, aby `HtmlHelper` klasy o nazwie `Label()`.</span><span class="sxs-lookup"><span data-stu-id="ccd56-164">The class in Listing 3 adds an extension method to the `HtmlHelper` class named `Label()`.</span></span> <span data-ttu-id="ccd56-165">Istnieje kilka rzeczy, które powinny uwagi dotyczące tej klasy.</span><span class="sxs-lookup"><span data-stu-id="ccd56-165">There are a couple of things that you should notice about this class.</span></span> <span data-ttu-id="ccd56-166">Należy zauważyć, że klasa jest klasie statycznej.</span><span class="sxs-lookup"><span data-stu-id="ccd56-166">First, notice that the class is a static class.</span></span> <span data-ttu-id="ccd56-167">Zdefiniuj metodę rozszerzenia o klasie statycznej.</span><span class="sxs-lookup"><span data-stu-id="ccd56-167">You must define an extension method with a static class.</span></span>

<span data-ttu-id="ccd56-168">Po drugie, zwróć uwagę, że pierwszy parametr `Label()` metody jest poprzedzony słowa kluczowego `this`.</span><span class="sxs-lookup"><span data-stu-id="ccd56-168">Second, notice that the first parameter of the `Label()` method is preceded by the keyword `this`.</span></span> <span data-ttu-id="ccd56-169">Pierwszy parametr metody rozszerzenia wskazuje klasę, która rozszerza — metoda rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="ccd56-169">The first parameter of an extension method indicates the class that the extension method extends.</span></span>

<span data-ttu-id="ccd56-170">**3 — lista`Helpers\LabelExtensions.cs`**</span><span class="sxs-lookup"><span data-stu-id="ccd56-170">**Listing 3 – `Helpers\LabelExtensions.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

<span data-ttu-id="ccd56-171">Po utworzeniu metodę rozszerzenia i pomyślnie skompilować aplikację, metody rozszerzenia pojawia się w programie Visual Studio Intellisense podobnie jak wszystkie inne metody klasy (patrz rysunek 2).</span><span class="sxs-lookup"><span data-stu-id="ccd56-171">After you create an extension method, and build your application successfully, the extension method appears in Visual Studio Intellisense like all of the other methods of a class (see Figure 2).</span></span> <span data-ttu-id="ccd56-172">Jedyna różnica polega na rozszerzenia metod są wyświetlane przy użyciu specjalnego symbolu obok nich (ikonę strzałki w dół).</span><span class="sxs-lookup"><span data-stu-id="ccd56-172">The only difference is that extension methods appear with a special symbol next to them (an icon of a downward arrow).</span></span>


<span data-ttu-id="ccd56-173">[![Przy użyciu metody rozszerzenia Html.Label()](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="ccd56-173">[![Using the Html.Label() extension method](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span></span>

<span data-ttu-id="ccd56-174">**Rysunek 02**: przy użyciu metody rozszerzenia Html.Label() ([kliknij, aby wyświetlić obraz w pełnym rozmiarze](creating-custom-html-helpers-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="ccd56-174">**Figure 02**: Using the Html.Label() extension method  ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image6.png))</span></span>


<span data-ttu-id="ccd56-175">Zmodyfikowany widok indeksu listę 4 używa metody rozszerzenia Html.Label() do renderowania, wszystkie jego `<label>` tagów.</span><span class="sxs-lookup"><span data-stu-id="ccd56-175">The modified Index view in Listing 4 uses the Html.Label() extension method to render all of its `<label>` tags.</span></span>

<span data-ttu-id="ccd56-176">**Wyświetlanie listy 4.`Views\Home\Index3.aspx`**</span><span class="sxs-lookup"><span data-stu-id="ccd56-176">**Listing 4 – `Views\Home\Index3.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a><span data-ttu-id="ccd56-177">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="ccd56-177">Summary</span></span>

<span data-ttu-id="ccd56-178">W tym samouczku przedstawiono dwie metody tworzenia niestandardowych pomocników HTML.</span><span class="sxs-lookup"><span data-stu-id="ccd56-178">In this tutorial, you learned two methods of creating custom HTML Helpers.</span></span> <span data-ttu-id="ccd56-179">Po pierwsze, przedstawiono sposób tworzenia niestandardowego `Label()` pomocnika kodu HTML, tworząc statycznej metody, która zwraca wartość typu ciąg.</span><span class="sxs-lookup"><span data-stu-id="ccd56-179">First, you learned how to create a custom `Label()` HTML Helper by creating a static method that returns a string.</span></span> <span data-ttu-id="ccd56-180">Następnie przedstawiono sposób tworzenia niestandardowego `Label()` metody pomocnika kodu HTML, tworząc metody rozszerzenia na `HtmlHelper` klasy.</span><span class="sxs-lookup"><span data-stu-id="ccd56-180">Next, you learned how to create a custom `Label()` HTML Helper method by creating an extension method on the `HtmlHelper` class.</span></span>

<span data-ttu-id="ccd56-181">W tym samouczku I koncentruje się na tworzeniu bardzo prosta metoda pomocnika kodu HTML.</span><span class="sxs-lookup"><span data-stu-id="ccd56-181">In this tutorial, I focused on building an extremely simple HTML Helper method.</span></span> <span data-ttu-id="ccd56-182">Należy pamiętać, że pomocnika kodu HTML, może być jako skomplikowane, można dowolnie.</span><span class="sxs-lookup"><span data-stu-id="ccd56-182">Realize that an HTML Helper can be as complicated as you want.</span></span> <span data-ttu-id="ccd56-183">Można tworzyć pomocników HTML, który renderowania zawartości zaawansowanych, takich jak widok drzewa, menu lub tabele bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ccd56-183">You can build HTML Helpers that render rich content such as tree views, menus, or tables of database data.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="ccd56-184">[Poprzednie](asp-net-mvc-views-overview-cs.md)
[dalej](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span><span class="sxs-lookup"><span data-stu-id="ccd56-184">[Previous](asp-net-mvc-views-overview-cs.md)
[Next](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span></span>