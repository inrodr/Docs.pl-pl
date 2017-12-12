---
title: "Niestandardowe elementy formatujące w interfejsów API sieci web platformy ASP.NET Core MVC"
author: tdykstra
description: "Informacje o sposobie tworzenia i używania niestandardowych elementy formatujące do interfejsów API w ASP.NET Core sieci web."
keywords: "Niestandardowe elementy formatujące interfejsu api sieci web platformy ASP.NET Core"
ms.author: tdykstra
manager: wpickett
ms.date: 02/08/2017
ms.topic: article
ms.assetid: 1fb6fdc2-e199-4469-9012-b909d1913422
ms.technology: aspnet
ms.prod: asp.net-core
uid: mvc/models/custom-formatters
ms.openlocfilehash: 5e665abe10fd7444c3fd5f20cfeca3ef0a5f79d3
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/10/2017
---
# <a name="custom-formatters-in-aspnet-core-mvc-web-apis"></a><span data-ttu-id="754b1-104">Niestandardowe elementy formatujące w interfejsów API sieci web platformy ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="754b1-104">Custom formatters in ASP.NET Core MVC web APIs</span></span>

<span data-ttu-id="754b1-105">przez [Dykstra niestandardowy](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="754b1-105">By [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="754b1-106">Podstawowe ASP.NET MVC ma wbudowaną obsługę wymiany danych w interfejsów API sieci web za pomocą formatu JSON, XML lub zwykły tekst.</span><span class="sxs-lookup"><span data-stu-id="754b1-106">ASP.NET Core MVC has built-in support for data exchange in web APIs by using JSON, XML, or plain text formats.</span></span> <span data-ttu-id="754b1-107">W tym artykule pokazano, jak dodać obsługę dodatkowych formatach tworząc niestandardowe elementy formatujące.</span><span class="sxs-lookup"><span data-stu-id="754b1-107">This article shows how to add support for additional formats by creating custom formatters.</span></span>

<span data-ttu-id="754b1-108">[Wyświetlanie lub pobieranie próbki z usługi GitHub](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/advanced/custom-formatters/sample).</span><span class="sxs-lookup"><span data-stu-id="754b1-108">[View or download sample from GitHub](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/advanced/custom-formatters/sample).</span></span>

## <a name="when-to-use-custom-formatters"></a><span data-ttu-id="754b1-109">Kiedy używać niestandardowej elementy formatujące</span><span class="sxs-lookup"><span data-stu-id="754b1-109">When to use custom formatters</span></span>

<span data-ttu-id="754b1-110">Niestandardowy element formatujący należy użyć [zawartości negocjacji](xref:mvc/models/formatting) procesu do obsługi typu zawartości, która nie jest obsługiwana przez wbudowane elementy formatujące (JSON, XML i zwykły tekst).</span><span class="sxs-lookup"><span data-stu-id="754b1-110">Use a custom formatter when you want the [content negotiation](xref:mvc/models/formatting) process to support a content type that isn't supported by the built-in formatters (JSON, XML, and plain text).</span></span>

<span data-ttu-id="754b1-111">Na przykład, jeśli niektórzy klienci dla interfejsu API sieci web mogą obsługiwać [Protobuf](https://github.com/google/protobuf) format, warto użyć Protobuf z tymi klientami, ponieważ jest bardziej wydajne.</span><span class="sxs-lookup"><span data-stu-id="754b1-111">For example, if some of the clients for your web API can handle the [Protobuf](https://github.com/google/protobuf) format, you might want to use Protobuf with those clients because it's more efficient.</span></span>  <span data-ttu-id="754b1-112">Można też interfejs API sieci web do wysyłania nazwy i adresy [vCard](https://wikipedia.org/wiki/VCard) formatu, często używane format wymiany danych kontaktowych.</span><span class="sxs-lookup"><span data-stu-id="754b1-112">Or you might want your web API to send contact names and addresses in [vCard](https://wikipedia.org/wiki/VCard) format, a commonly used format for exchanging contact data.</span></span> <span data-ttu-id="754b1-113">Przykładowa aplikacja podaną w tym artykule implementuje element formatujący vCard proste.</span><span class="sxs-lookup"><span data-stu-id="754b1-113">The sample app provided with this article implements a simple vCard formatter.</span></span>

## <a name="overview-of-how-to-use-a-custom-formatter"></a><span data-ttu-id="754b1-114">Przegląd sposobu użycia niestandardowego elementu formatującego</span><span class="sxs-lookup"><span data-stu-id="754b1-114">Overview of how to use a custom formatter</span></span>

<span data-ttu-id="754b1-115">Poniżej przedstawiono procedurę tworzenia i używania niestandardowego elementu formatującego:</span><span class="sxs-lookup"><span data-stu-id="754b1-115">Here are the steps to create and use a custom formatter:</span></span>

* <span data-ttu-id="754b1-116">Utwórz klasę program formatujący danych wyjściowych, aby serializować dane do wysłania do klienta.</span><span class="sxs-lookup"><span data-stu-id="754b1-116">Create an output formatter class if you want to serialize data to send to the client.</span></span>
* <span data-ttu-id="754b1-117">Utwórz klasę wejściowy element formatujący, aby deserializować danych otrzymanych od klienta.</span><span class="sxs-lookup"><span data-stu-id="754b1-117">Create an input formatter class if you want to deserialize data received from the client.</span></span> 
* <span data-ttu-id="754b1-118">Dodawanie wystąpień użytkownika elementy formatujące do `InputFormatters` i `OutputFormatters` kolekcji w [MvcOptions](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.mvcoptions).</span><span class="sxs-lookup"><span data-stu-id="754b1-118">Add instances of your formatters to the `InputFormatters` and `OutputFormatters` collections in [MvcOptions](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.mvcoptions).</span></span>

<span data-ttu-id="754b1-119">Poniższe sekcje zawierają wskazówki i przykłady kodu dla każdego z tych kroków.</span><span class="sxs-lookup"><span data-stu-id="754b1-119">The following sections provide guidance and code examples for each of these steps.</span></span>

## <a name="how-to-create-a-custom-formatter-class"></a><span data-ttu-id="754b1-120">Tworzenie klasy niestandardowej programu formatującego</span><span class="sxs-lookup"><span data-stu-id="754b1-120">How to create a custom formatter class</span></span>

<span data-ttu-id="754b1-121">Aby utworzyć element formatujący:</span><span class="sxs-lookup"><span data-stu-id="754b1-121">To create a formatter:</span></span>

* <span data-ttu-id="754b1-122">Klasa wyprowadzona z odpowiedniej klasy podstawowej.</span><span class="sxs-lookup"><span data-stu-id="754b1-122">Derive the class from the appropriate base class.</span></span>
* <span data-ttu-id="754b1-123">Podaj prawidłowy nośnik typy i kodowania w konstruktorze.</span><span class="sxs-lookup"><span data-stu-id="754b1-123">Specify valid media types and encodings in the constructor.</span></span>
* <span data-ttu-id="754b1-124">Zastąpienie `CanReadType` / `CanWriteType` metody</span><span class="sxs-lookup"><span data-stu-id="754b1-124">Override `CanReadType`/`CanWriteType` methods</span></span>
* <span data-ttu-id="754b1-125">Zastąpienie `ReadRequestBodyAsync` / `WriteResponseBodyAsync` metody</span><span class="sxs-lookup"><span data-stu-id="754b1-125">Override `ReadRequestBodyAsync`/`WriteResponseBodyAsync` methods</span></span>
  
### <a name="derive-from-the-appropriate-base-class"></a><span data-ttu-id="754b1-126">Pochodzi od odpowiedniej klasy podstawowej</span><span class="sxs-lookup"><span data-stu-id="754b1-126">Derive from the appropriate base class</span></span>

<span data-ttu-id="754b1-127">Dla typów nośników tekstu (na przykład vCard), pochodzi z [TextInputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.textinputformatter) lub [TextOutputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.textoutputformatter) klasy podstawowej.</span><span class="sxs-lookup"><span data-stu-id="754b1-127">For text media types (for example, vCard), derive from the [TextInputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.textinputformatter) or [TextOutputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.textoutputformatter) base class.</span></span>

[!code-csharp[Main](custom-formatters/sample/Formatters/VcardOutputFormatter.cs?name=classdef)]

<span data-ttu-id="754b1-128">Dla typu binary, pochodzi z [InputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.inputformatter) lub [OutputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.outputformatter) klasy podstawowej.</span><span class="sxs-lookup"><span data-stu-id="754b1-128">For binary types, derive from the [InputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.inputformatter) or [OutputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.outputformatter) base class.</span></span>

### <a name="specify-valid-media-types-and-encodings"></a><span data-ttu-id="754b1-129">Określ prawidłowy nośnik typy i kodowania</span><span class="sxs-lookup"><span data-stu-id="754b1-129">Specify valid media types and encodings</span></span>

<span data-ttu-id="754b1-130">W konstruktorze, Określ prawidłowy nośnik typy i kodowania przez dodanie do `SupportedMediaTypes` i `SupportedEncodings` kolekcji.</span><span class="sxs-lookup"><span data-stu-id="754b1-130">In the constructor, specify valid media types and encodings by adding to the `SupportedMediaTypes` and `SupportedEncodings` collections.</span></span>

[!code-csharp[Main](custom-formatters/sample/Formatters/VcardOutputFormatter.cs?name=ctor&highlight=3,5-6)]

> [!NOTE]  
> <span data-ttu-id="754b1-131">Nie można wykonać iniekcji zależności konstruktora klasy elementu formatującego.</span><span class="sxs-lookup"><span data-stu-id="754b1-131">You can't do constructor dependency injection in a formatter class.</span></span> <span data-ttu-id="754b1-132">Na przykład nie można pobrać Rejestrator przez dodanie parametru rejestratora konstruktora.</span><span class="sxs-lookup"><span data-stu-id="754b1-132">For example, you can't get a logger by adding a logger parameter to the constructor.</span></span> <span data-ttu-id="754b1-133">Aby uzyskać dostęp do usługi, należy użyć obiektu context, który zostanie przekazany do metody.</span><span class="sxs-lookup"><span data-stu-id="754b1-133">To access services, you have to use the context object that gets passed in to your methods.</span></span> <span data-ttu-id="754b1-134">Przykładowy kod [poniżej](#read-write) pokazano, jak to zrobić.</span><span class="sxs-lookup"><span data-stu-id="754b1-134">A code example [below](#read-write) shows how to do this.</span></span>

### <a name="override-canreadtypecanwritetype"></a><span data-ttu-id="754b1-135">Zastąpienie CanReadType/CanWriteType</span><span class="sxs-lookup"><span data-stu-id="754b1-135">Override CanReadType/CanWriteType</span></span> 

<span data-ttu-id="754b1-136">Określ typ może deserializować do lub serializacji z przez zastąpienie `CanReadType` lub `CanWriteType` metody.</span><span class="sxs-lookup"><span data-stu-id="754b1-136">Specify the type you can deserialize into or serialize from by overriding the `CanReadType` or `CanWriteType` methods.</span></span> <span data-ttu-id="754b1-137">Na przykład tylko można utworzyć pliku vCard tekst z `Contact` typu i na odwrót.</span><span class="sxs-lookup"><span data-stu-id="754b1-137">For example, you might only be able to create vCard text from a `Contact` type and vice versa.</span></span>

[!code-csharp[Main](custom-formatters/sample/Formatters/VcardOutputFormatter.cs?name=canwritetype)]

#### <a name="the-canwriteresult-method"></a><span data-ttu-id="754b1-138">Metoda CanWriteResult</span><span class="sxs-lookup"><span data-stu-id="754b1-138">The CanWriteResult method</span></span>

<span data-ttu-id="754b1-139">W niektórych scenariuszach należy zastąpić `CanWriteResult` zamiast `CanWriteType`.</span><span class="sxs-lookup"><span data-stu-id="754b1-139">In some scenarios you have to override `CanWriteResult` instead of `CanWriteType`.</span></span> <span data-ttu-id="754b1-140">Użyj `CanWriteResult` jeśli są spełnione następujące warunki:</span><span class="sxs-lookup"><span data-stu-id="754b1-140">Use `CanWriteResult` if the following conditions are true:</span></span>

  * <span data-ttu-id="754b1-141">Stosowana metoda akcji zwraca klasę modelu.</span><span class="sxs-lookup"><span data-stu-id="754b1-141">Your action method returns a model class.</span></span>
  * <span data-ttu-id="754b1-142">Brak klasy pochodne, które może być zwracany w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="754b1-142">There are derived classes which might be returned at runtime.</span></span>
  * <span data-ttu-id="754b1-143">Należy znać w czasie wykonywania, z którego pochodzi klasy został zwrócony przez akcję.</span><span class="sxs-lookup"><span data-stu-id="754b1-143">You need to know at runtime which derived class was returned by the action.</span></span>  

<span data-ttu-id="754b1-144">Na przykład załóżmy, że podpis metody akcji zwraca `Person` typu, ale może zwrócić `Student` lub `Instructor` typu pochodzącego od `Person`.</span><span class="sxs-lookup"><span data-stu-id="754b1-144">For example, suppose your action method signature returns a `Person` type, but it may return a `Student` or `Instructor` type that derives from `Person`.</span></span> <span data-ttu-id="754b1-145">Jeśli chcesz, aby Twoje elementu formatującego do obsługi tylko `Student` obiektów, sprawdź typ [obiektu](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.outputformattercanwritecontext#Microsoft_AspNetCore_Mvc_Formatters_OutputFormatterCanWriteContext_Object) w obiekt kontekstu do `CanWriteResult` — metoda.</span><span class="sxs-lookup"><span data-stu-id="754b1-145">If you want your formatter to handle only `Student` objects, check the type of [Object](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.outputformattercanwritecontext#Microsoft_AspNetCore_Mvc_Formatters_OutputFormatterCanWriteContext_Object) in the context object provided to the `CanWriteResult` method.</span></span> <span data-ttu-id="754b1-146">Należy pamiętać, że nie jest konieczne użycie `CanWriteResult` gdy metoda akcji zwraca `IActionResult`; w takim przypadku `CanWriteType` metody odbiera typ środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="754b1-146">Note that it's not necessary to use `CanWriteResult` when the action method returns `IActionResult`; in that case, the `CanWriteType` method receives the runtime type.</span></span>

<a id="read-write"></a>
### <a name="override-readrequestbodyasyncwriteresponsebodyasync"></a><span data-ttu-id="754b1-147">Zastąpienie ReadRequestBodyAsync/WriteResponseBodyAsync</span><span class="sxs-lookup"><span data-stu-id="754b1-147">Override ReadRequestBodyAsync/WriteResponseBodyAsync</span></span> 

<span data-ttu-id="754b1-148">Wykonują rzeczywistą pracę podczas deserializacji lub serializacji w `ReadRequestBodyAsync` lub `WriteResponseBodyAsync`.</span><span class="sxs-lookup"><span data-stu-id="754b1-148">You do the actual work of deserializing or serializing in `ReadRequestBodyAsync` or `WriteResponseBodyAsync`.</span></span>  <span data-ttu-id="754b1-149">Wyróżnione wiersze w następującym przykładzie pokazano, jak można pobrać usługi z kontenera iniekcji zależności (nie można pobrać je z parametrami konstruktora).</span><span class="sxs-lookup"><span data-stu-id="754b1-149">The highlighted lines in the following example show how to get services from the dependency injection container (you can't get them from constructor parameters).</span></span>

[!code-csharp[Main](custom-formatters/sample/Formatters/VcardOutputFormatter.cs?name=writeresponse&highlight=3-4)]

## <a name="how-to-configure-mvc-to-use-a-custom-formatter"></a><span data-ttu-id="754b1-150">Jak skonfigurować MVC, aby użyć niestandardowego elementu formatującego</span><span class="sxs-lookup"><span data-stu-id="754b1-150">How to configure MVC to use a custom formatter</span></span>
 
<span data-ttu-id="754b1-151">Aby użyć niestandardowego elementu formatującego, dodać wystąpienia klasy elementu formatującego do `InputFormatters` lub `OutputFormatters` kolekcji.</span><span class="sxs-lookup"><span data-stu-id="754b1-151">To use a custom formatter, add an instance of the formatter class to the `InputFormatters` or `OutputFormatters` collection.</span></span>

[!code-csharp[Main](custom-formatters/sample/Startup.cs?name=mvcoptions&highlight=3-4)]

<span data-ttu-id="754b1-152">Elementy formatujące są oceniane w kolejności, w jakiej wstawić je.</span><span class="sxs-lookup"><span data-stu-id="754b1-152">Formatters are evaluated in the order you insert them.</span></span> <span data-ttu-id="754b1-153">Pierwsza z nich ma pierwszeństwo.</span><span class="sxs-lookup"><span data-stu-id="754b1-153">The first one takes precedence.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="754b1-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="754b1-154">Next steps</span></span>

<span data-ttu-id="754b1-155">Zobacz [Przykładowa aplikacja](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/advanced/custom-formatters/sample), który implementuje proste vCard dane wejściowe i elementy formatujące danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="754b1-155">See the [sample application](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/advanced/custom-formatters/sample), which implements simple vCard input and output formatters.</span></span>  <span data-ttu-id="754b1-156">Aplikacja czyta i zapisuje vCard, który wygląda jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="754b1-156">The application reads and writes vCards that look like the following example:</span></span>

```
BEGIN:VCARD
VERSION:2.1
N:Davolio;Nancy
FN:Nancy Davolio
UID:20293482-9240-4d68-b475-325df4a83728
END:VCARD
```

<span data-ttu-id="754b1-157">Aby wyświetlić vCard dane wyjściowe, uruchom aplikację i Wyślij żądanie Get z Akceptuj nagłówka "tekstu/vcard" do `http://localhost:63313/api/contacts/` (jeśli jest uruchomiony w programie Visual Studio) lub `http://localhost:5000/api/contacts/` (jeśli jest uruchomione z wiersza polecenia).</span><span class="sxs-lookup"><span data-stu-id="754b1-157">To see vCard output, run the application and send a Get request with Accept header "text/vcard" to `http://localhost:63313/api/contacts/` (when running from Visual Studio) or `http://localhost:5000/api/contacts/` (when running from the command line).</span></span>

<span data-ttu-id="754b1-158">Aby dodać vCard do kolekcji w pamięci, kontaktów, Wyślij żądanie Post do tego samego adresu URL, z nagłówka Content-Type "tekstu/vcard" i vCard z tekstem, sformatowany tak jak w powyższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="754b1-158">To add a vCard to the in-memory collection of contacts, send a Post request to the same URL, with Content-Type header "text/vcard" and with vCard text in the body, formatted like the example above.</span></span>