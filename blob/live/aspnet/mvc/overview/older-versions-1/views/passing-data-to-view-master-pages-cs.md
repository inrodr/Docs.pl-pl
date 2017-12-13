---
uid: mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-cs
title: Przekazywanie danych do strony wzorcowej widoku (C#) | Dokumentacja firmy Microsoft
author: microsoft
description: "Celem tego samouczka jest wyjaśnienie, jak można przekazać dane z kontrolera do widoku strony wzorcowej. Omówione dwie strategie przekazywania danych do widoku m..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/16/2008
ms.topic: article
ms.assetid: 5fee879b-8bde-42a9-a434-60ba6b1cf747
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: b8bc8ce0690d2e45877be75011d8883facbc74a7
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/10/2017
---
<a name="passing-data-to-view-master-pages-c"></a><span data-ttu-id="75a21-104">Przekazywanie danych do strony wzorcowej widoku (C#)</span><span class="sxs-lookup"><span data-stu-id="75a21-104">Passing Data to View Master Pages (C#)</span></span>
====================
<span data-ttu-id="75a21-105">przez [firmy Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="75a21-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="75a21-106">Pobierz plik PDF</span><span class="sxs-lookup"><span data-stu-id="75a21-106">Download PDF</span></span>](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_13_CS.pdf)

> <span data-ttu-id="75a21-107">Celem tego samouczka jest wyjaśnienie, jak można przekazać dane z kontrolera do widoku strony wzorcowej.</span><span class="sxs-lookup"><span data-stu-id="75a21-107">The goal of this tutorial is to explain how you can pass data from a controller to a view master page.</span></span> <span data-ttu-id="75a21-108">Omówione dwie strategie przekazywania danych do strony wzorcowej widoku.</span><span class="sxs-lookup"><span data-stu-id="75a21-108">We examine two strategies for passing data to a view master page.</span></span> <span data-ttu-id="75a21-109">Najpierw omówimy łatwe rozwiązania, który daje w aplikacji, która jest trudne w utrzymaniu.</span><span class="sxs-lookup"><span data-stu-id="75a21-109">First, we discuss an easy solution that results in an application that is difficult to maintain.</span></span> <span data-ttu-id="75a21-110">Następnie omówione dużo lepszym rozwiązaniem, które wymaga nieco więcej pracy początkowej, ale powoduje utrzymaniu znacznie więcej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="75a21-110">Next, we examine a much better solution that requires a little more initial work but results in a much more maintainable application.</span></span>


## <a name="passing-data-to-view-master-pages"></a><span data-ttu-id="75a21-111">Przekazywanie danych do strony wzorcowej widoku</span><span class="sxs-lookup"><span data-stu-id="75a21-111">Passing Data to View Master Pages</span></span>

<span data-ttu-id="75a21-112">Celem tego samouczka jest wyjaśnienie, jak można przekazać dane z kontrolera do widoku strony wzorcowej.</span><span class="sxs-lookup"><span data-stu-id="75a21-112">The goal of this tutorial is to explain how you can pass data from a controller to a view master page.</span></span> <span data-ttu-id="75a21-113">Omówione dwie strategie przekazywania danych do strony wzorcowej widoku.</span><span class="sxs-lookup"><span data-stu-id="75a21-113">We examine two strategies for passing data to a view master page.</span></span> <span data-ttu-id="75a21-114">Najpierw omówimy łatwe rozwiązania, który daje w aplikacji, która jest trudne w utrzymaniu.</span><span class="sxs-lookup"><span data-stu-id="75a21-114">First, we discuss an easy solution that results in an application that is difficult to maintain.</span></span> <span data-ttu-id="75a21-115">Następnie omówione dużo lepszym rozwiązaniem, które wymaga nieco więcej pracy początkowej, ale powoduje utrzymaniu znacznie więcej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="75a21-115">Next, we examine a much better solution that requires a little more initial work but results in a much more maintainable application.</span></span>

### <a name="the-problem"></a><span data-ttu-id="75a21-116">Problem</span><span class="sxs-lookup"><span data-stu-id="75a21-116">The Problem</span></span>

<span data-ttu-id="75a21-117">Załóżmy, że tworzysz filmu aplikacji bazy danych i mają być wyświetlane na liście kategorii filmu na każdej stronie w aplikacji (zobacz rysunek 1).</span><span class="sxs-lookup"><span data-stu-id="75a21-117">Imagine that you are building a movie database application and you want to display the list of movie categories on every page in your application (see Figure 1).</span></span> <span data-ttu-id="75a21-118">Załóżmy, ponadto, czy lista kategorii film jest przechowywana w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="75a21-118">Imagine, furthermore, that the list of movie categories is stored in a database table.</span></span> <span data-ttu-id="75a21-119">W takim przypadku powinna mieć do pobrania kategorii z bazy danych i renderowania listy kategorii filmu w widoku strony wzorcowej.</span><span class="sxs-lookup"><span data-stu-id="75a21-119">In that case, it would make sense to retrieve the categories from the database and render the list of movie categories within a view master page.</span></span>


<span data-ttu-id="75a21-120">[![Wyświetlanie kategorii filmu w widoku strony wzorcowej](passing-data-to-view-master-pages-cs/_static/image2.png)](passing-data-to-view-master-pages-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="75a21-120">[![Displaying movie categories in a view master page](passing-data-to-view-master-pages-cs/_static/image2.png)](passing-data-to-view-master-pages-cs/_static/image1.png)</span></span>

<span data-ttu-id="75a21-121">**Rysunek 01**: wyświetlanie kategorii filmu w widoku strony wzorcowej ([kliknij, aby wyświetlić obraz w pełnym rozmiarze](passing-data-to-view-master-pages-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="75a21-121">**Figure 01**: Displaying movie categories in a view master page ([Click to view full-size image](passing-data-to-view-master-pages-cs/_static/image3.png))</span></span>


<span data-ttu-id="75a21-122">Oto problem.</span><span class="sxs-lookup"><span data-stu-id="75a21-122">Here's the problem.</span></span> <span data-ttu-id="75a21-123">Sposób pobierania listy kategorii filmu z strony wzorcowej?</span><span class="sxs-lookup"><span data-stu-id="75a21-123">How do you retrieve the list of movie categories in the master page?</span></span> <span data-ttu-id="75a21-124">Jest kuszące bezpośrednio wywołać metody klasach modeli na stronie głównej.</span><span class="sxs-lookup"><span data-stu-id="75a21-124">It is tempting to call methods of your model classes in the master page directly.</span></span> <span data-ttu-id="75a21-125">Innymi słowy jest kuszące, aby uwzględnić kod do pobierania danych z prawej stronie głównej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="75a21-125">In other words, it is tempting to include the code for retrieving the data from the database right in your master page.</span></span> <span data-ttu-id="75a21-126">Jednak pomijanie kontrolerów MVC dostęp do bazy danych naruszyłoby czyste rozdzielenie dotyczy jest jednym z podstawowych zalet tworzenia aplikacji MVC.</span><span class="sxs-lookup"><span data-stu-id="75a21-126">However, bypassing your MVC controllers to access the database would violate the clean separation of concerns that is one of the primary benefits of building an MVC application.</span></span>

<span data-ttu-id="75a21-127">W aplikacji MVC ma wszystkie interakcje między widoków MVC i modelu MVC, które mają być obsługiwane przez kontrolerów MVC.</span><span class="sxs-lookup"><span data-stu-id="75a21-127">In an MVC application, you want all interaction between your MVC views and your MVC model to be handled by your MVC controllers.</span></span> <span data-ttu-id="75a21-128">Powoduje to separacji w utrzymaniu, dostosowywalne i testować aplikacji.</span><span class="sxs-lookup"><span data-stu-id="75a21-128">This separation of concerns results in a more maintainable, adaptable, and testable application.</span></span>

<span data-ttu-id="75a21-129">W aplikacji MVC wszystkie dane przekazywane do widoku — w tym widoku strony wzorcowej — powinny być przekazywane do widoku przez akcji kontrolera.</span><span class="sxs-lookup"><span data-stu-id="75a21-129">In an MVC application, all data passed to a view – including a view master page – should be passed to a view by a controller action.</span></span> <span data-ttu-id="75a21-130">Ponadto dane powinien zostać przekazany dzięki wykorzystaniu danych widoku.</span><span class="sxs-lookup"><span data-stu-id="75a21-130">Furthermore, the data should be passed by taking advantage of view data.</span></span> <span data-ttu-id="75a21-131">W pozostałej części tego samouczka I Sprawdź na dwa sposoby przekazywania danych widoku do strony wzorcowej widoku.</span><span class="sxs-lookup"><span data-stu-id="75a21-131">In the remainder of this tutorial, I examine two methods of passing view data to a view master page.</span></span>

### <a name="the-simple-solution"></a><span data-ttu-id="75a21-132">Prostym rozwiązaniem</span><span class="sxs-lookup"><span data-stu-id="75a21-132">The Simple Solution</span></span>

<span data-ttu-id="75a21-133">Zacznijmy z Najprostszym rozwiązaniem w celu przekazywania danych widoku z kontrolera do widoku strony wzorcowej.</span><span class="sxs-lookup"><span data-stu-id="75a21-133">Let's start with the simplest solution to passing view data from a controller to a view master page.</span></span> <span data-ttu-id="75a21-134">Najprostszym rozwiązaniem jest przekazywanie danych widoku dla strony wzorcowej każdej akcji kontrolera.</span><span class="sxs-lookup"><span data-stu-id="75a21-134">The simplest solution is to pass the view data for the master page in each and every controller action.</span></span>

<span data-ttu-id="75a21-135">Należy wziąć pod uwagę kontrolera 1 wyświetlania.</span><span class="sxs-lookup"><span data-stu-id="75a21-135">Consider the controller in Listing 1.</span></span> <span data-ttu-id="75a21-136">Udostępnia ona dwie akcje o nazwie `Index()` i `Details()`.</span><span class="sxs-lookup"><span data-stu-id="75a21-136">It exposes two actions named `Index()` and `Details()`.</span></span> <span data-ttu-id="75a21-137">`Index()` Metoda akcji zwraca co film filmy tabeli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="75a21-137">The `Index()` action method returns every movie in the Movies database table.</span></span> <span data-ttu-id="75a21-138">`Details()` Metoda akcji zwraca co filmu w filmu określonej kategorii.</span><span class="sxs-lookup"><span data-stu-id="75a21-138">The `Details()` action method returns every movie in a particular movie category.</span></span>

<span data-ttu-id="75a21-139">**1 — Lista`Controllers\HomeController.cs`**</span><span class="sxs-lookup"><span data-stu-id="75a21-139">**Listing 1 – `Controllers\HomeController.cs`**</span></span>

[!code-csharp[Main](passing-data-to-view-master-pages-cs/samples/sample1.cs)]

<span data-ttu-id="75a21-140">Należy zauważyć, że zarówno indeks() i akcje Details() dodać dwóch elementów do wyświetlania danych.</span><span class="sxs-lookup"><span data-stu-id="75a21-140">Notice that both the Index() and the Details() actions add two items to view data.</span></span> <span data-ttu-id="75a21-141">Akcja indeks() dodaje dwa klucze: kategorie i filmy.</span><span class="sxs-lookup"><span data-stu-id="75a21-141">The Index() action adds two keys: categories and movies.</span></span> <span data-ttu-id="75a21-142">Klucz kategorie reprezentuje listę filmu kategorie wyświetlane w widoku strony wzorcowej.</span><span class="sxs-lookup"><span data-stu-id="75a21-142">The categories key represents the list of movie categories displayed by the view master page.</span></span> <span data-ttu-id="75a21-143">Klucz filmy reprezentuje listę filmów wyświetlanych przez indeks strony widoku.</span><span class="sxs-lookup"><span data-stu-id="75a21-143">The movies key represents the list of movies displayed by the Index view page.</span></span>

<span data-ttu-id="75a21-144">Akcja Details() dodaje również dwa klucze o nazwie kategorii i filmy.</span><span class="sxs-lookup"><span data-stu-id="75a21-144">The Details() action also adds two keys named categories and movies.</span></span> <span data-ttu-id="75a21-145">Klucz kategorie jeszcze raz reprezentuje listę filmu kategorie wyświetlane w widoku strony wzorcowej.</span><span class="sxs-lookup"><span data-stu-id="75a21-145">The categories key, once again, represents the list of movie categories displayed by the view master page.</span></span> <span data-ttu-id="75a21-146">Klucz filmy reprezentuje listę filmów w określonej kategorii wyświetlanych przez strony widoku szczegółów (patrz rysunek 2).</span><span class="sxs-lookup"><span data-stu-id="75a21-146">The movies key represents the list of movies in a particular category displayed by the Details view page (see Figure 2).</span></span>


<span data-ttu-id="75a21-147">[![W widoku szczegółów](passing-data-to-view-master-pages-cs/_static/image5.png)](passing-data-to-view-master-pages-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="75a21-147">[![The Details view](passing-data-to-view-master-pages-cs/_static/image5.png)](passing-data-to-view-master-pages-cs/_static/image4.png)</span></span>

<span data-ttu-id="75a21-148">**Rysunek 02**: widok szczegółów ([kliknij, aby wyświetlić obraz w pełnym rozmiarze](passing-data-to-view-master-pages-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="75a21-148">**Figure 02**: The Details view ([Click to view full-size image](passing-data-to-view-master-pages-cs/_static/image6.png))</span></span>


<span data-ttu-id="75a21-149">Widok indeks znajduje się w wyświetlania 2.</span><span class="sxs-lookup"><span data-stu-id="75a21-149">The Index view is contained in Listing 2.</span></span> <span data-ttu-id="75a21-150">Iteruje po prostu Lista filmów reprezentowany przez element filmów w widoku danych.</span><span class="sxs-lookup"><span data-stu-id="75a21-150">It simply iterates through the list of movies represented by the movies item in view data.</span></span>

<span data-ttu-id="75a21-151">**2 — Lista`Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="75a21-151">**Listing 2 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](passing-data-to-view-master-pages-cs/samples/sample2.aspx)]

<span data-ttu-id="75a21-152">Strony wzorcowej widoku znajduje się w 3 wyświetlania.</span><span class="sxs-lookup"><span data-stu-id="75a21-152">The view master page is contained in Listing 3.</span></span> <span data-ttu-id="75a21-153">Widok strony wzorcowej iteracje i renderuje wszystkie kategorie filmu reprezentowany przez element kategorii z danymi widoku.</span><span class="sxs-lookup"><span data-stu-id="75a21-153">The view master page iterates and renders all of the movie categories represented by the categories item from view data.</span></span>

<span data-ttu-id="75a21-154">**3 — lista`Views\Shared\Site.master`**</span><span class="sxs-lookup"><span data-stu-id="75a21-154">**Listing 3 – `Views\Shared\Site.master`**</span></span>

[!code-aspx[Main](passing-data-to-view-master-pages-cs/samples/sample3.aspx)]

<span data-ttu-id="75a21-155">Wszystkie dane są przekazywane do widoku oraz widoku strony wzorcowej za pośrednictwem widoku danych.</span><span class="sxs-lookup"><span data-stu-id="75a21-155">All data is passed to the view and the view master page through view data.</span></span> <span data-ttu-id="75a21-156">To jest prawidłowy sposób, aby przekazać dane do strony wzorcowej.</span><span class="sxs-lookup"><span data-stu-id="75a21-156">That is the correct way to pass data to the master page.</span></span>

<span data-ttu-id="75a21-157">Tak co to jest problem z tego rozwiązania?</span><span class="sxs-lookup"><span data-stu-id="75a21-157">So, what's wrong with this solution?</span></span> <span data-ttu-id="75a21-158">Problem polega na tym, że to rozwiązanie narusza zasady suchej (nie powtarzaj siebie).</span><span class="sxs-lookup"><span data-stu-id="75a21-158">The problem is that this solution violates the DRY (Don't Repeat Yourself) principle.</span></span> <span data-ttu-id="75a21-159">Każdy akcji kontrolera należy dodać tej samej listy kategorii film, aby wyświetlić dane.</span><span class="sxs-lookup"><span data-stu-id="75a21-159">Each and every controller action must add the very same list of movie categories to view data.</span></span> <span data-ttu-id="75a21-160">Mające zduplikowany kod w aplikacji utrudnia aplikacji znacznie Obsługa dostosowania i modyfikować.</span><span class="sxs-lookup"><span data-stu-id="75a21-160">Having duplicate code in your application makes your application much more difficult to maintain, adapt, and modify.</span></span>

### <a name="the-good-solution"></a><span data-ttu-id="75a21-161">Dobre rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="75a21-161">The Good Solution</span></span>

<span data-ttu-id="75a21-162">W tej sekcji omówione alternatywnych i lepsze, rozwiązanie do przekazywania danych z akcji kontrolera do widoku strony wzorcowej.</span><span class="sxs-lookup"><span data-stu-id="75a21-162">In this section, we examine an alternative, and better, solution to passing data from a controller action to a view master page.</span></span> <span data-ttu-id="75a21-163">Zamiast opcji dodawania kategorii filmu dla strony wzorcowej w każdej akcji kontrolera, możemy dodać filmu kategorie do widoku danych tylko raz.</span><span class="sxs-lookup"><span data-stu-id="75a21-163">Instead of adding the movie categories for the master page in each and every controller action, we add the movie categories to the view data only once.</span></span> <span data-ttu-id="75a21-164">Wszystkie dane widoku, używany przez strony wzorcowej widoku jest dodawany do kontrolera aplikacji.</span><span class="sxs-lookup"><span data-stu-id="75a21-164">All view data used by the view master page is added in an Application controller.</span></span>

<span data-ttu-id="75a21-165">Klasa ApplicationController znajduje się w listę 4.</span><span class="sxs-lookup"><span data-stu-id="75a21-165">The ApplicationController class is contained in Listing 4.</span></span>

<span data-ttu-id="75a21-166">**Wyświetlanie listy 4.`Controllers\ApplicationController.cs`**</span><span class="sxs-lookup"><span data-stu-id="75a21-166">**Listing 4 – `Controllers\ApplicationController.cs`**</span></span>

[!code-csharp[Main](passing-data-to-view-master-pages-cs/samples/sample4.cs)]

<span data-ttu-id="75a21-167">Istnieją trzy elementy, które powinny uwagi dotyczące kontrolera aplikacji na wyświetlanie 4.</span><span class="sxs-lookup"><span data-stu-id="75a21-167">There are three things that you should notice about the Application controller in Listing 4.</span></span> <span data-ttu-id="75a21-168">Najpierw należy zauważyć, że klasa dziedziczy z klasy podstawowej System.Web.Mvc.Controller.</span><span class="sxs-lookup"><span data-stu-id="75a21-168">First, notice that the class inherits from the base System.Web.Mvc.Controller class.</span></span> <span data-ttu-id="75a21-169">Kontroler aplikacji jest klasy kontrolera.</span><span class="sxs-lookup"><span data-stu-id="75a21-169">The Application controller is a controller class.</span></span>

<span data-ttu-id="75a21-170">Po drugie Zwróć uwagę, że klasa kontrolera aplikacji jest klasą abstrakcyjną.</span><span class="sxs-lookup"><span data-stu-id="75a21-170">Second, notice that the Application controller class is an abstract class.</span></span> <span data-ttu-id="75a21-171">Klasy abstrakcyjnej jest klasa, która musi być implementowana przez konkretną klasę.</span><span class="sxs-lookup"><span data-stu-id="75a21-171">An abstract class is a class that must be implemented by a concrete class.</span></span> <span data-ttu-id="75a21-172">Ponieważ kontrolera aplikacji jest klasą abstrakcyjną, nie można wywołać nie wszystkie metody zdefiniowanej w klasie bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="75a21-172">Because the Application controller is an abstract class, you cannot not invoke any methods defined in the class directly.</span></span> <span data-ttu-id="75a21-173">Jeśli będziesz próbować wywołać klasy aplikacji bezpośrednio następnie zostanie wyświetlony komunikat o błędzie nie można odnaleźć zasobu.</span><span class="sxs-lookup"><span data-stu-id="75a21-173">If you attempt to invoke the Application class directly then you'll get a Resource Cannot Be Found error message.</span></span>

<span data-ttu-id="75a21-174">Trzecie Zwróć uwagę, że kontroler aplikacji zawiera konstruktora, który dodaje listy kategorii film, aby wyświetlić dane.</span><span class="sxs-lookup"><span data-stu-id="75a21-174">Third, notice that the Application controller contains a constructor that adds the list of movie categories to view data.</span></span> <span data-ttu-id="75a21-175">Każda klasa kontrolera, który dziedziczy z kontrolera aplikacji automatycznie wywołuje konstruktor kontrolera aplikacji.</span><span class="sxs-lookup"><span data-stu-id="75a21-175">Every controller class that inherits from the Application controller calls the Application controller's constructor automatically.</span></span> <span data-ttu-id="75a21-176">Zawsze, gdy wywoływana żadnych działań na każdym kontrolerze, który dziedziczy z kontrolera aplikacji, kategorie film jest dołączony do danych widoku automatycznie.</span><span class="sxs-lookup"><span data-stu-id="75a21-176">Whenever you call any action on any controller that inherits from the Application controller, the movie categories is included in the view data automatically.</span></span>

<span data-ttu-id="75a21-177">Kontroler filmów w listę 5 dziedziczy kontrolera aplikacji.</span><span class="sxs-lookup"><span data-stu-id="75a21-177">The Movies controller in Listing 5 inherits from the Application controller.</span></span>

<span data-ttu-id="75a21-178">**Wyświetlanie listy 5 —`Controllers\MoviesController.cs`**</span><span class="sxs-lookup"><span data-stu-id="75a21-178">**Listing 5 – `Controllers\MoviesController.cs`**</span></span>

[!code-csharp[Main](passing-data-to-view-master-pages-cs/samples/sample5.cs)]

<span data-ttu-id="75a21-179">Kontroler filmów, podobnie jak kontrolera głównej opisanych w poprzedniej sekcji, udostępnia dwie metody akcji, o nazwie `Index()` i `Details()`.</span><span class="sxs-lookup"><span data-stu-id="75a21-179">The Movies controller, just like the Home controller discussed in the previous section, exposes two action methods named `Index()` and `Details()`.</span></span> <span data-ttu-id="75a21-180">Należy zauważyć, że na liście kategorii filmu wyświetlanych przez strony wzorcowej widoku nie jest dodawane do wyświetlania danych w jednym `Index()` lub `Details()` metody.</span><span class="sxs-lookup"><span data-stu-id="75a21-180">Notice that the list of movie categories displayed by the view master page is not added to view data in either the `Index()` or `Details()` method.</span></span> <span data-ttu-id="75a21-181">Ponieważ kontrolera filmy dziedziczy kontrolera aplikacji, lista kategorii film jest dodawana do wyświetlania danych automatycznie.</span><span class="sxs-lookup"><span data-stu-id="75a21-181">Because the Movies controller inherits from the Application controller, the list of movie categories is added to view data automatically.</span></span>

<span data-ttu-id="75a21-182">Zwróć uwagę, to rozwiązanie w celu dodanie danych widoku dla strony wzorcowej widoku nie narusza zasady suchej (nie powtarzaj siebie).</span><span class="sxs-lookup"><span data-stu-id="75a21-182">Notice that this solution to adding view data for a view master page does not violate the DRY (Don't Repeat Yourself) principle.</span></span> <span data-ttu-id="75a21-183">Kod do dodawania listy kategorii film, aby wyświetlić dane znajduje się w lokalizacji tylko jeden: Konstruktor kontrolera aplikacji.</span><span class="sxs-lookup"><span data-stu-id="75a21-183">The code for adding the list of movie categories to view data is contained in only one location: the constructor for the Application controller.</span></span>

### <a name="summary"></a><span data-ttu-id="75a21-184">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="75a21-184">Summary</span></span>

<span data-ttu-id="75a21-185">W tym samouczku omówiono dwa podejścia do przekazywania danych widoku z kontrolera do widoku strony wzorcowej.</span><span class="sxs-lookup"><span data-stu-id="75a21-185">In this tutorial, we discussed two approaches to passing view data from a controller to a view master page.</span></span> <span data-ttu-id="75a21-186">Po pierwsze firma Microsoft zbadać prostą, ale trudne w utrzymaniu podejście.</span><span class="sxs-lookup"><span data-stu-id="75a21-186">First, we examined a simple, but difficult to maintain approach.</span></span> <span data-ttu-id="75a21-187">W pierwszej sekcji omówiono sposób dodawania danych widoku dla strony wzorcowej widoku w każdej akcji każdego kontrolera w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="75a21-187">In the first section, we discussed how you can add view data for a view master page in each every controller action in your application.</span></span> <span data-ttu-id="75a21-188">Możemy stwierdzić, było nieprawidłowe podejście ponieważ narusza on zasady suchej (nie powtarzaj samodzielnie).</span><span class="sxs-lookup"><span data-stu-id="75a21-188">We concluded that this was a bad approach because it violates the DRY (Don't Repeat Yourself) principle.</span></span>

<span data-ttu-id="75a21-189">Następnie możemy się zbadana znacznie lepszą strategię dodawania danych do wyświetlania danych wymagane przez strony wzorcowej widoku.</span><span class="sxs-lookup"><span data-stu-id="75a21-189">Next, we examined a much better strategy for adding data required by a view master page to view data.</span></span> <span data-ttu-id="75a21-190">Zamiast opcji dodawania danych widoku w każdej akcji kontrolera, dodaliśmy danych widoku tylko raz w ramach kontrolera aplikacji.</span><span class="sxs-lookup"><span data-stu-id="75a21-190">Instead of adding the view data in each and every controller action, we added the view data only once within an Application controller.</span></span> <span data-ttu-id="75a21-191">W ten sposób można uniknąć zduplikowanych kodu podczas przekazywania danych do strony wzorcowej widoku w aplikacji platformy ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="75a21-191">That way, you can avoid duplicate code when passing data to a view master page in an ASP.NET MVC application.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="75a21-192">[Poprzednie](creating-page-layouts-with-view-master-pages-cs.md)
[dalej](asp-net-mvc-views-overview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="75a21-192">[Previous](creating-page-layouts-with-view-master-pages-cs.md)
[Next](asp-net-mvc-views-overview-vb.md)</span></span>