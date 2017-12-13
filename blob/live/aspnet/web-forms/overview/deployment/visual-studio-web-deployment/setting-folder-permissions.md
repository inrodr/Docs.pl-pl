---
uid: web-forms/overview/deployment/visual-studio-web-deployment/setting-folder-permissions
title: "Wdrażanie sieci Web ASP.NET przy użyciu programu Visual Studio: Ustawianie uprawnień folderu | Dokumentacja firmy Microsoft"
author: tdykstra
description: "Ta seria samouczek pokazuje, jak wdrożyć platformy ASP.NET (publikowanie) aplikacji do aplikacji sieci Web usługi aplikacji Azure lub innego dostawcy hostingu sieci web przez używane..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: 9715a121-fa55-4f1b-a5d2-fb3f6cd8be8f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/setting-folder-permissions
msc.type: authoredcontent
ms.openlocfilehash: 19bef5ff97fd5b79135df8ca9bd6bd316594cc5e
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/10/2017
---
<a name="aspnet-web-deployment-using-visual-studio-setting-folder-permissions"></a><span data-ttu-id="10281-103">Wdrażanie sieci Web ASP.NET przy użyciu programu Visual Studio: ustawienie uprawnień do folderu</span><span class="sxs-lookup"><span data-stu-id="10281-103">ASP.NET Web Deployment using Visual Studio: Setting Folder Permissions</span></span>
====================
<span data-ttu-id="10281-104">przez [Dykstra niestandardowy](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="10281-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="10281-105">Pobierz początkowego projektu</span><span class="sxs-lookup"><span data-stu-id="10281-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="10281-106">Ta seria samouczek pokazuje, jak wdrożyć platformy ASP.NET (publikowanie) aplikacji do aplikacji sieci Web usługi aplikacji Azure lub innego dostawcy hostingu sieci web za pomocą programu Visual Studio 2012 lub Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="10281-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="10281-107">Aby uzyskać informacje dotyczące serii, zobacz [pierwszy samouczek z tej serii](introduction.md).</span><span class="sxs-lookup"><span data-stu-id="10281-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="10281-108">Omówienie</span><span class="sxs-lookup"><span data-stu-id="10281-108">Overview</span></span>

<span data-ttu-id="10281-109">W tym samouczku, należy ustawić uprawnienia folderu do *Elmah* folder w sieci web, wdrożonych lokacji, dzięki czemu aplikacja może tworzyć pliki dziennika w tym folderze.</span><span class="sxs-lookup"><span data-stu-id="10281-109">In this tutorial, you set folder permissions for the *Elmah* folder in the deployed web site so that the application can create log files in that folder.</span></span>

<span data-ttu-id="10281-110">Podczas testowania aplikacji sieci web w programie Visual Studio przy użyciu serwera wdrożeniowego programu Visual Studio (Cassini) lub usługi IIS Express, aplikacja zostanie uruchomiona w ramach Twojej tożsamości.</span><span class="sxs-lookup"><span data-stu-id="10281-110">When you test a web application in Visual Studio using the Visual Studio Development Server (Cassini) or IIS Express, the application runs under your identity.</span></span> <span data-ttu-id="10281-111">Prawdopodobnie są uprawnienia administratora na komputerze deweloperskim i mieć pełne uprawnienia do podejmować żadnych działań, plików w folderze.</span><span class="sxs-lookup"><span data-stu-id="10281-111">You are most likely an administrator on your development computer and have full authority to do anything to any file in any folder.</span></span> <span data-ttu-id="10281-112">Ale po uruchomieniu aplikacji w środowisku usług IIS, działa z tożsamością zdefiniowane dla puli aplikacji, przypisane do lokacji.</span><span class="sxs-lookup"><span data-stu-id="10281-112">But when an application runs under IIS, it runs under the identity defined for the application pool that the site is assigned to.</span></span> <span data-ttu-id="10281-113">Jest to zazwyczaj konto zdefiniowane przez system, który ma ograniczone uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="10281-113">This is typically a system-defined account that has limited permissions.</span></span> <span data-ttu-id="10281-114">Domyślnie przeczytał i uprawnienia do wykonywania dla aplikacji sieci web plików i folderów, ale nie ma dostępu do zapisu.</span><span class="sxs-lookup"><span data-stu-id="10281-114">By default it has read and execute permissions on your web application's files and folders, but it doesn't have write access.</span></span>

<span data-ttu-id="10281-115">Staje się on problemu tworzy aplikacji lub aktualizacji plików, co jest typowe w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="10281-115">This becomes an issue if your application creates or updates files, which is a common need in web applications.</span></span> <span data-ttu-id="10281-116">W aplikacji Contoso University Elmah tworzy pliki XML z *Elmah* folderu w celu zapisania informacji o błędach.</span><span class="sxs-lookup"><span data-stu-id="10281-116">In the Contoso University application, Elmah creates XML files in the *Elmah* folder in order to save details about errors.</span></span> <span data-ttu-id="10281-117">Nawet jeśli nie używasz przypominać Elmah, witryny zezwolić użytkownikom na przekazywanie plików lub innych zadań, które zapisu danych do folderu w witrynie sieci.</span><span class="sxs-lookup"><span data-stu-id="10281-117">Even if you don't use something like Elmah, your site might let users upload files or perform other tasks that write data to a folder in your site.</span></span>

<span data-ttu-id="10281-118">Przypomnienie: Jeśli coś nie działa podczas wykonywania kroków samouczka wyświetlony komunikat o błędzie, należy sprawdzić [Rozwiązywanie problemów z strony](troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="10281-118">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="test-error-logging-and-reporting"></a><span data-ttu-id="10281-119">Rejestrowanie błędów testu i raportowanie</span><span class="sxs-lookup"><span data-stu-id="10281-119">Test error logging and reporting</span></span>

<span data-ttu-id="10281-120">Aby zobaczyć, jak aplikacja nie działa prawidłowo w usługach IIS (chociaż jak testach w programie Visual Studio), może spowodować błąd, który zwykle rejestrowany przez Elmah, a następnie otwórz dziennik błędów Elmah, aby wyświetlić szczegóły.</span><span class="sxs-lookup"><span data-stu-id="10281-120">To see how the application doesn't work correctly in IIS (although it did when you tested it in Visual Studio), you can cause an error that would normally be logged by Elmah, and then open the Elmah error log to see the details.</span></span> <span data-ttu-id="10281-121">Jeśli Elmah nie może utworzyć pliku XML i zapisać szczegóły błędu, zostanie wyświetlony raport o błędach puste.</span><span class="sxs-lookup"><span data-stu-id="10281-121">If Elmah was unable to create an XML file and store the error details, you see an empty error report.</span></span>

<span data-ttu-id="10281-122">Otwórz przeglądarkę i przejdź do `http://localhost/ContosoUniversity`, a następnie żądają nieprawidłowy adres URL, takie jak *Studentsxxx.aspx*.</span><span class="sxs-lookup"><span data-stu-id="10281-122">Open a browser and go to `http://localhost/ContosoUniversity`, and then request an invalid URL like *Studentsxxx.aspx*.</span></span> <span data-ttu-id="10281-123">Zostanie wyświetlona strona błędu generowanych przez system, zamiast *GenericErrorPage.aspx* strony, ponieważ `customErrors` ustawienia w pliku Web.config jest "RemoteOnly" i są uruchomione usługi IIS lokalnie:</span><span class="sxs-lookup"><span data-stu-id="10281-123">You see a system-generated error page instead of the *GenericErrorPage.aspx* page because the `customErrors` setting in the Web.config file is "RemoteOnly" and you are running IIS locally:</span></span>

![Strona błędu 404 protokołu HTTP](setting-folder-permissions/_static/image1.png)

<span data-ttu-id="10281-125">Teraz uruchom *Elmah.axd* Aby wyświetlić raport o błędzie.</span><span class="sxs-lookup"><span data-stu-id="10281-125">Now run *Elmah.axd* to see the error report.</span></span> <span data-ttu-id="10281-126">Po zalogowaniu się przy użyciu poświadczeń konta administratora (&quot;admin&quot; i &quot;devpwd&quot;), zobacz stronę błędu pusty dziennika, ponieważ Elmah nie może utworzyć pliku XML w *Elmah*folderu:</span><span class="sxs-lookup"><span data-stu-id="10281-126">After you log in with the administrator account credentials (&quot;admin&quot; and &quot;devpwd&quot;), you see an empty error log page because Elmah was unable to create an XML file in the *Elmah* folder:</span></span>

![Błąd dziennika pusta](setting-folder-permissions/_static/image2.png)

## <a name="set-write-permission-on-the-elmah-folder"></a><span data-ttu-id="10281-128">Ustaw uprawnienia do zapisu w folderze Elmah</span><span class="sxs-lookup"><span data-stu-id="10281-128">Set write permission on the Elmah folder</span></span>

<span data-ttu-id="10281-129">Możesz ręcznie ustawić uprawnienia do folderu lub można utworzyć automatycznego część procesu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="10281-129">You can set folder permissions manually or you can make it an automatic part of the deployment process.</span></span> <span data-ttu-id="10281-130">Dzięki automatycznej wymaga złożonego kodu MSBuild, a ponieważ masz w tym celu należy wdrożyć po raz pierwszy, następujące kroki jak to zrobić ręcznie.</span><span class="sxs-lookup"><span data-stu-id="10281-130">Making it automatic requires complex MSBuild code, and since you only have to do this the first time you deploy, the following steps how to do it manually.</span></span> <span data-ttu-id="10281-131">(Aby uzyskać informacje o sposobie tworzenia ta część procesu wdrażania, zobacz [ustawienie uprawnień folderu publikowania w sieci Web](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx) na blogu Sayed Hashimi.)</span><span class="sxs-lookup"><span data-stu-id="10281-131">(For information about how to make this part of the deployment process, see [Setting Folder Permissions on Web Publish](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx) on Sayed Hashimi's blog.)</span></span>

1. <span data-ttu-id="10281-132">W **Eksploratora plików**, przejdź do *C:\inetpub\wwwroot\ContosoUniversity*.</span><span class="sxs-lookup"><span data-stu-id="10281-132">In **File Explorer**, navigate to *C:\inetpub\wwwroot\ContosoUniversity*.</span></span> <span data-ttu-id="10281-133">Kliknij prawym przyciskiem myszy *Elmah* folderu, wybierz opcję **właściwości**, a następnie wybierz **zabezpieczeń** kartę.</span><span class="sxs-lookup"><span data-stu-id="10281-133">Right-click the *Elmah* folder, select **Properties**, and then select the **Security** tab.</span></span>
2. <span data-ttu-id="10281-134">Kliknij przycisk **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="10281-134">Click **Edit**.</span></span>
3. <span data-ttu-id="10281-135">W **uprawnienia dla Elmah** okno dialogowe, wybierz opcję **domyślna pula aplikacji**, a następnie wybierz **zapisu** pole wyboru w **Zezwalaj** kolumny.</span><span class="sxs-lookup"><span data-stu-id="10281-135">In the **Permissions for Elmah** dialog box, select **DefaultAppPool**, and then select the **Write** check box in the **Allow** column.</span></span>

    ![Uprawnienia do folderu ELMAH](setting-folder-permissions/_static/image3.png)

    <span data-ttu-id="10281-137">(Jeśli nie widzisz **DefaultAppPool** w **nazwy grup lub użytkowników** listy, prawdopodobnie użyto innej metody niż określona w tym samouczku można skonfigurować usługi IIS i platformy ASP.NET 4 na komputerze.</span><span class="sxs-lookup"><span data-stu-id="10281-137">(If you don't see **DefaultAppPool** in the **Group or user names** list, you probably used some other method than the one specified in this tutorial to set up IIS and ASP.NET 4 on your computer.</span></span> <span data-ttu-id="10281-138">W takim przypadku dowiedzieć się, jakie tożsamości jest używana przez pulę aplikacji przypisany do aplikacji Contoso University i przydziel uprawnienie zapisu do tej tożsamości.</span><span class="sxs-lookup"><span data-stu-id="10281-138">In that case, find out what identity is used by the application pool assigned to the Contoso University application, and grant write permission to that identity.</span></span> <span data-ttu-id="10281-139">Zobacz linki dotyczące tożsamości puli aplikacji na końcu tego samouczka). Kliknij przycisk **OK** w obu polach okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="10281-139">See the links about application pool identities at the end of this tutorial.) Click **OK** in both dialog boxes.</span></span>

## <a name="retest-error-logging-and-reporting"></a><span data-ttu-id="10281-140">Sprawdź jeszcze raz rejestrowania błędów i raportowanie</span><span class="sxs-lookup"><span data-stu-id="10281-140">Retest error logging and reporting</span></span>

<span data-ttu-id="10281-141">Testowanie powodując błąd ponownie w taki sam sposób (żądanie nieprawidłowy adres URL) i uruchom **dziennik błędów** strony.</span><span class="sxs-lookup"><span data-stu-id="10281-141">Test by causing an error again in the same way (request a bad URL) and run the **Error Log** page.</span></span> <span data-ttu-id="10281-142">Teraz ten błąd pojawia się na stronie.</span><span class="sxs-lookup"><span data-stu-id="10281-142">This time the error appears on the page.</span></span>

![Strona dziennika błędów ELMAH](setting-folder-permissions/_static/image4.png)

## <a name="summary"></a><span data-ttu-id="10281-144">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="10281-144">Summary</span></span>

<span data-ttu-id="10281-145">Ukończono wszystkich zadań, które są niezbędne, aby uzyskać Contoso University działa poprawnie w usługach IIS na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="10281-145">You have now completed all of the tasks necessary to get Contoso University working correctly in IIS on your local computer.</span></span> <span data-ttu-id="10281-146">W następnym samouczku udostępnienia lokacji publicznie przez wdrożenie jej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="10281-146">In the next tutorial, you will make the site publicly available by deploying it to Azure.</span></span>

## <a name="more-information"></a><span data-ttu-id="10281-147">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="10281-147">More information</span></span>

<span data-ttu-id="10281-148">W tym przykładzie przyczyny, dlaczego nie można zapisać plików dziennika Elmah było dość oczywiste.</span><span class="sxs-lookup"><span data-stu-id="10281-148">In this example, the reason why Elmah was unable to save log files was fairly obvious.</span></span> <span data-ttu-id="10281-149">Śledzenie usług IIS można użyć w przypadku gdy przyczyną tego problemu nie jest tak oczywiste; zobacz [Rozwiązywanie problemów z żądania za pomocą śledzenia nieudanych w usługach IIS 7](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis) w witrynie IIS.net.</span><span class="sxs-lookup"><span data-stu-id="10281-149">You can use IIS tracing in cases where the cause of the problem is not so obvious; see [Troubleshooting Failed Requests Using Tracing in IIS 7](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis) on the IIS.net site.</span></span>

<span data-ttu-id="10281-150">Aby uzyskać więcej informacji dotyczących sposobu udzielania uprawnień do tożsamości puli aplikacji, zobacz [tożsamości puli aplikacji](https://www.iis.net/learn/manage/configuring-security/application-pool-identities) i [Zabezpieczanie zawartości w usługach IIS za pomocą list ACL systemu plików](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls) w witrynie IIS.net.</span><span class="sxs-lookup"><span data-stu-id="10281-150">For more information about how to grant permissions to application pool identities, see [Application Pool Identities](https://www.iis.net/learn/manage/configuring-security/application-pool-identities) and [Secure Content in IIS Through File System ACLs](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls) on the IIS.net site.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="10281-151">[Poprzednie](deploying-to-iis.md)
[dalej](deploying-to-production.md)</span><span class="sxs-lookup"><span data-stu-id="10281-151">[Previous](deploying-to-iis.md)
[Next](deploying-to-production.md)</span></span>