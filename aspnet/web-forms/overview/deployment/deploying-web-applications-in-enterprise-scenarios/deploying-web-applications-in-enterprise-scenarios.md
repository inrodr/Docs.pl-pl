---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios
title: "Wdrażanie aplikacji sieci Web w scenariuszach dla przedsiębiorstw przy użyciu programu Visual Studio 2010 | Dokumentacja firmy Microsoft"
author: jrjlee
description: "Ten zestaw samouczków opisano narzędzia i metod, które służy do wdrażania aplikacji sieci web w różnych scenariuszach dla przedsiębiorstwa. Wyjaśniono, jak najlepiej wykorzystać..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/03/2012
ms.topic: article
ms.assetid: 48cfe378-d62a-48c6-a4db-6be3cead6898
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios
msc.type: authoredcontent
ms.openlocfilehash: 99bab371dd34b30f3554843e49bbec7f57c3f96c
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/10/2017
---
<a name="deploying-web-applications-in-enterprise-scenarios-using-visual-studio-2010"></a><span data-ttu-id="051d3-104">Wdrażanie aplikacji sieci Web w scenariuszach dla przedsiębiorstw przy użyciu programu Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="051d3-104">Deploying Web Applications in Enterprise Scenarios using Visual Studio 2010</span></span>
====================
<span data-ttu-id="051d3-105">przez [Lewandowski Jason](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="051d3-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="051d3-106">Pobierz plik PDF</span><span class="sxs-lookup"><span data-stu-id="051d3-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="051d3-107">Ten zestaw samouczków opisano narzędzia i metod, które służy do wdrażania aplikacji sieci web w różnych scenariuszach dla przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="051d3-107">This set of tutorials describes tools and techniques you can use to deploy web applications in various enterprise scenarios.</span></span> <span data-ttu-id="051d3-108">Wyjaśniono, jak najlepiej korzystać z technologii, takich jak Visual Studio 2010, aparat kompilacji firmy Microsoft (MSBuild), Internet informacji Services (IIS) 7.5, narzędzia wdrażania usług IIS sieci Web (Web Deploy), Framework kolektywu serwerów sieci Web (WFF) i narzędzi, takich jak VSDBCMD.exe do uproszczenie i zarządzanie procesem wdrażania.</span><span class="sxs-lookup"><span data-stu-id="051d3-108">It explains how to make best use of technologies like Visual Studio 2010, the Microsoft Build Engine (MSBuild), Internet Information Services (IIS) 7.5, the IIS Web Deployment Tool (Web Deploy), the Web Farm Framework (WFF), and utilities like VSDBCMD.exe to simplify and manage the deployment process.</span></span> <span data-ttu-id="051d3-109">Zawiera omówienie pojęć i wskazówki zorientowane na zadania, który pomoże Ci:</span><span class="sxs-lookup"><span data-stu-id="051d3-109">It includes conceptual overviews and task-oriented guidance that will help you to:</span></span>
> 
> - <span data-ttu-id="051d3-110">Przejrzyj i ustanowienia wymagań związanych z wdrażaniem aplikacji sieci web skali przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="051d3-110">Review and establish the deployment requirements for an enterprise-scale web application.</span></span>
> - <span data-ttu-id="051d3-111">Skonfiguruj test, tymczasowych i produkcyjnych środowiska serwera sieci web do obsługi wdrożenia sieci web.</span><span class="sxs-lookup"><span data-stu-id="051d3-111">Configure test, staging, and production web server environments to support web deployment.</span></span>
> - <span data-ttu-id="051d3-112">Skonfiguruj procesów ciągłej integracji (CI) Team Foundation Server (TFS) do obsługi wdrażania automatycznego sieci web.</span><span class="sxs-lookup"><span data-stu-id="051d3-112">Configure Team Foundation Server (TFS) continuous integration (CI) processes to support automated web deployment.</span></span>
> - <span data-ttu-id="051d3-113">Wdrażanie aplikacji sieci web skali przedsiębiorstwa do innego serwera środowisk przy użyciu różnych wymagań i ograniczeń.</span><span class="sxs-lookup"><span data-stu-id="051d3-113">Deploy enterprise-scale web applications to different server environments with varying requirements and restrictions.</span></span>
> - <span data-ttu-id="051d3-114">Wdróż zmian w aplikacji sieci web, które działają w środowiskach inny serwer.</span><span class="sxs-lookup"><span data-stu-id="051d3-114">Deploy changes to web applications that are running in different server environments.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="051d3-115">Gdy te samouczki opisano użycie TFS jako serwer elementu konfiguracji, wskazówki łatwo jest dostosowane do dowolnego serwera CI.</span><span class="sxs-lookup"><span data-stu-id="051d3-115">While these tutorials describe the use of TFS as a CI server, the guidance is easily adapted to any CI server.</span></span> <span data-ttu-id="051d3-116">Nie trzeba szczegółowej znajomości TFS, aby poznać i korzystać z samouczków.</span><span class="sxs-lookup"><span data-stu-id="051d3-116">You don't need a detailed knowledge of TFS to understand and leverage the tutorials.</span></span>
> 
> 
> <span data-ttu-id="051d3-117">Włoska translacji tego samouczka, odwiedź stronę [http://www.lucamorelli.it](http://www.lucamorelli.it).</span><span class="sxs-lookup"><span data-stu-id="051d3-117">For an Italian translation of these tutorials, visit [http://www.lucamorelli.it](http://www.lucamorelli.it).</span></span>


## <a name="about-the-authors"></a><span data-ttu-id="051d3-118">O autorów</span><span class="sxs-lookup"><span data-stu-id="051d3-118">About the Authors</span></span>

<span data-ttu-id="051d3-119">JASON jest główną technologist z [wzorca zawartości](http://www.contentmaster.com/) gdzie on pracuje z produktów firmy Microsoft i technologie, szczególnie programu SharePoint i ASP.NET, przez kilka lat.</span><span class="sxs-lookup"><span data-stu-id="051d3-119">Jason Lee is a principal technologist with [Content Master](http://www.contentmaster.com/) where he has been working with Microsoft products and technologies, especially SharePoint and ASP.NET, for several years.</span></span> <span data-ttu-id="051d3-120">JASON zawiera Praca w przypadku komputerów i jest obecnie MCPD i MCTS certyfikowane.</span><span class="sxs-lookup"><span data-stu-id="051d3-120">Jason holds a PhD in computing and is currently MCPD and MCTS certified.</span></span> <span data-ttu-id="051d3-121">Możesz przeczytać Jason w blogu techniczne w [www.jrjlee.com](http://www.jrjlee.com/).</span><span class="sxs-lookup"><span data-stu-id="051d3-121">You can read Jason's technical blog at [www.jrjlee.com](http://www.jrjlee.com/).</span></span>

<span data-ttu-id="051d3-122">Curry Benjaminowi jest główną technologist z [wzorca zawartości](http://www.contentmaster.com/) który został zapisany oficjalnych dokumentów, dokumentacji zestawu SDK prezentacji programu PowerPoint i prowadzone i online szkoleń podczas jego zawodowych.</span><span class="sxs-lookup"><span data-stu-id="051d3-122">Benjamin Curry is a principal technologist with [Content Master](http://www.contentmaster.com/) who has written whitepapers, SDK documentation, PowerPoint presentations, and instructor-led and online training courses during his career.</span></span> <span data-ttu-id="051d3-123">Oryginalnego elementu członkowskiego zespołu programu ASP.NET, on współpracuje z technologii sieci web firmy Microsoft za pośrednictwem dekadę.</span><span class="sxs-lookup"><span data-stu-id="051d3-123">An original member of the ASP.NET documentation team, he has worked with Microsoft's web technologies for over a decade.</span></span>

## <a name="target-audience"></a><span data-ttu-id="051d3-124">Odbiorcy docelowi</span><span class="sxs-lookup"><span data-stu-id="051d3-124">Target Audience</span></span>

<span data-ttu-id="051d3-125">Jest to zestaw samouczków dla deweloperów aplikacji sieci web ASP.NET i architekci rozwiązań, korzystających z programu Visual Studio 2010 do tworzenia aplikacji sieci web w skali przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="051d3-125">This set of tutorials is for ASP.NET web application developers and solution architects who use Visual Studio 2010 to create enterprise-scale web applications.</span></span> <span data-ttu-id="051d3-126">Aby uzyskać najbardziej wartości z zawartości, należy wiedzieć, jak za pomocą programu Visual Studio 2010 i mieć podstawowe znajomość TFS, wraz z pogłębianie wiedzy na temat technologii platformy sieci web firmy Microsoft, takich jak ASP.NET MVC 3, Windows Communication Foundation (WCF), usługi IIS, SQL Serwer i projektów bazy danych programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="051d3-126">To get the most value from the content, you should be comfortable using Visual Studio 2010 and have a basic familiarity with TFS, together with an awareness of Microsoft web platform technologies like ASP.NET MVC 3, Windows Communication Foundation (WCF), IIS, SQL Server, and Visual Studio database projects.</span></span> <span data-ttu-id="051d3-127">Jednak nie trzeba znać technologie i narzędzia wdrażania lub trzeba wiedzieć, jak skonfigurować elementu konfiguracji systemów.</span><span class="sxs-lookup"><span data-stu-id="051d3-127">However, you do not need to be familiar with deployment tools and technologies or need to know how to set up CI systems.</span></span>

## <a name="requirements"></a><span data-ttu-id="051d3-128">Wymagania</span><span class="sxs-lookup"><span data-stu-id="051d3-128">Requirements</span></span>

<span data-ttu-id="051d3-129">Wykonaj wskazówki i wykonywać zadania, które opisują te samouczki, musisz zainstalować to oprogramowanie na komputerze deweloperskim:</span><span class="sxs-lookup"><span data-stu-id="051d3-129">To follow the walkthroughs and perform the tasks that these tutorials describe, you'll need to install this software on your development computer:</span></span>

- <span data-ttu-id="051d3-130">Visual Studio 2010 Premium lub Ultimate Edition z dodatkiem Service Pack 1</span><span class="sxs-lookup"><span data-stu-id="051d3-130">Visual Studio 2010 Premium or Ultimate Edition with Service Pack 1</span></span>
- <span data-ttu-id="051d3-131">.NET framework 4.0</span><span class="sxs-lookup"><span data-stu-id="051d3-131">.NET Framework 4.0</span></span>
- <span data-ttu-id="051d3-132">.NET framework 3.5 z dodatkiem Service Pack 1</span><span class="sxs-lookup"><span data-stu-id="051d3-132">.NET Framework 3.5 with Service Pack 1</span></span>
- <span data-ttu-id="051d3-133">ASP.NET MVC 3.0</span><span class="sxs-lookup"><span data-stu-id="051d3-133">ASP.NET MVC 3.0</span></span>
- <span data-ttu-id="051d3-134">Usługi IIS 7.5 Express</span><span class="sxs-lookup"><span data-stu-id="051d3-134">IIS 7.5 Express</span></span>
- <span data-ttu-id="051d3-135">Program SQL Server Express 2008 R2</span><span class="sxs-lookup"><span data-stu-id="051d3-135">SQL Server Express 2008 R2</span></span>

<span data-ttu-id="051d3-136">Do wykonania opisanych w całym te wskazówki dotyczące kroków wdrażania, musisz mieć dostęp do środowiska wdrażania aplikacji sieci Web przykładowej.</span><span class="sxs-lookup"><span data-stu-id="051d3-136">To perform the deployment steps described throughout these walkthroughs, you'll need to have access to sample Web application deployment environments.</span></span> <span data-ttu-id="051d3-137">Aby uzyskać najlepsze wyniki tych środowisk powinien odzwierciedlać wzorca wdrażania przedsiębiorstwa w organizacji.</span><span class="sxs-lookup"><span data-stu-id="051d3-137">For best results, these environments should reflect your organization's enterprise deployment pattern.</span></span> <span data-ttu-id="051d3-138">Następnie można zmodyfikować wskazówki zawarte w tej dokumentacji, aby uwzględnić w środowiskach wdrożenia oraz wymagań organizacji.</span><span class="sxs-lookup"><span data-stu-id="051d3-138">You can then modify the walkthroughs provided in this documentation to reflect the deployment environments and requirements of your own organization.</span></span>

## <a name="series-contents"></a><span data-ttu-id="051d3-139">Zawartość serii</span><span class="sxs-lookup"><span data-stu-id="051d3-139">Series Contents</span></span>

<span data-ttu-id="051d3-140">W tej sekcji wprowadzające składa się z dwóch tematy dodatkowe.</span><span class="sxs-lookup"><span data-stu-id="051d3-140">This introductory section consists of two further topics.</span></span> <span data-ttu-id="051d3-141">Te zaprojektowano niektórych szerszym kontekstem samouczki, które należy wykonać:</span><span class="sxs-lookup"><span data-stu-id="051d3-141">These are designed to provide some broader context for the tutorials that follow:</span></span>

- <span data-ttu-id="051d3-142">[Wdrożenia sieci Web w przedsiębiorstwie: Omówienie scenariusza](enterprise-web-deployment-scenario-overview.md).</span><span class="sxs-lookup"><span data-stu-id="051d3-142">[Enterprise Web Deployment: Scenario Overview](enterprise-web-deployment-scenario-overview.md).</span></span> <span data-ttu-id="051d3-143">W tym temacie opisano scenariusz, który stanowi podstawę dla każdego z samouczków w tej serii.</span><span class="sxs-lookup"><span data-stu-id="051d3-143">This topic describes the scenario that underpins each of the tutorials in this series.</span></span> <span data-ttu-id="051d3-144">Scenariusz koncentruje się na wymagania dotyczące zarządzania cyklem życia aplikacji (ALM) fikcyjnej firmy o nazwie firmy Fabrikam, Inc. miarę jej rozwoju aplikacji sieci web w skali przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="051d3-144">The scenario focuses on the Application Lifecycle Management (ALM) requirements of a fictional company named Fabrikam, Inc. as it develops an enterprise-scale web application.</span></span>
- <span data-ttu-id="051d3-145">[Zarządzanie cyklem życia aplikacji: Od projektowania do produkcji](application-lifecycle-management-from-development-to-production.md).</span><span class="sxs-lookup"><span data-stu-id="051d3-145">[Application Lifecycle Management: From Development to Production](application-lifecycle-management-from-development-to-production.md).</span></span> <span data-ttu-id="051d3-146">Ten temat zawiera omówienie wysokiego poziomu, end-to-end procesu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="051d3-146">This topic provides a high-level, end-to-end overview of a deployment process.</span></span> <span data-ttu-id="051d3-147">Go przedstawiono, jak firma Fabrikam przenosi skali przedsiębiorstwa aplikacja sieci web ASP.NET za pośrednictwem środowiska testowego, tymczasowych i produkcyjnych w ramach procesu projektowania ciągłe.</span><span class="sxs-lookup"><span data-stu-id="051d3-147">It illustrates how Fabrikam,Inc. moves an enterprise-scale ASP.NET web application through test, staging, and production environments as part of a continuous development process.</span></span>

<span data-ttu-id="051d3-148">Seria zawiera cztery zestawy samouczka.</span><span class="sxs-lookup"><span data-stu-id="051d3-148">The series includes four tutorial sets.</span></span> <span data-ttu-id="051d3-149">Każdy koncentruje się na różnych aspektów wdrożenia sieci web:</span><span class="sxs-lookup"><span data-stu-id="051d3-149">Each focuses on different aspects of web deployment:</span></span>

- <span data-ttu-id="051d3-150">[Narzędzie Web Deployment w przedsiębiorstwie](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md).</span><span class="sxs-lookup"><span data-stu-id="051d3-150">[Web Deployment in the Enterprise](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md).</span></span> <span data-ttu-id="051d3-151">Ten samouczek zawiera koncepcyjnej wprowadzenie do plików projektu MSBuild, potoku publikowania w sieci Web narzędzia Web Deploy i innych technologii pokrewnych.</span><span class="sxs-lookup"><span data-stu-id="051d3-151">This tutorial provides a conceptual introduction to MSBuild project files, the Web Publishing Pipeline, Web Deploy, and other related technologies.</span></span> <span data-ttu-id="051d3-152">Wyjaśniono sposób korzystania tych narzędzi wspólnie do zarządzania procesami złożone wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="051d3-152">It explains how you can use these tools together to manage complex deployment processes.</span></span>
- <span data-ttu-id="051d3-153">[Konfigurowanie środowisk serwera sieci Web wdrożenia](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="051d3-153">[Configuring Server Environments for Web Deployment](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md).</span></span> <span data-ttu-id="051d3-154">W tym samouczku opisano sposób konfigurowania serwerów systemu Windows do obsługi różnych scenariuszy wdrażania, w tym wdrażania pakietu sieci web do zdalnego przy użyciu usługi sieci Web wdrożenia agenta ("agent zdalnego") lub program obsługi wdrażania w sieci Web i wdrożenia zdalnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="051d3-154">This tutorial describes how to configure Windows servers to support various deployment scenarios, including remote web package deployment using the Web Deployment Agent Service (the "remote agent") or the Web Deploy Handler and remote database deployment.</span></span> <span data-ttu-id="051d3-155">Go znajdują się wskazówki dotyczące wybierania metody wdrażania właściwe dla własnego środowiska i opisuje sposób użycia WFF replikowanie wdrożonych aplikacji sieci web na wszystkich serwerach sieci web w farmie serwerów.</span><span class="sxs-lookup"><span data-stu-id="051d3-155">It provides guidance on choosing the appropriate deployment method for your own environment, and it describes how to use the WFF to replicate deployed web applications across all the web servers in a server farm.</span></span>
- <span data-ttu-id="051d3-156">[Konfigurowanie serwera Team Foundation Server Web Deployment](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="051d3-156">[Configuring Team Foundation Server for Web Deployment](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md).</span></span> <span data-ttu-id="051d3-157">W tym samouczku opisano sposób konfigurowania TFS w celu obsługi różnych scenariuszy wdrażania, łącznie z automatycznego wdrażania w trakcie procesu konfiguracji i ręcznie wyzwalane wdrożeń określonej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="051d3-157">This tutorial describes how to configure TFS to support various deployment scenarios, including automated deployment as part of a CI process and manually triggered deployments of specific builds.</span></span>
- <span data-ttu-id="051d3-158">[Zaawansowane wdrażanie w przedsiębiorstwie sieci Web](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="051d3-158">[Advanced Enterprise Web Deployment](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md).</span></span> <span data-ttu-id="051d3-159">Ten przewodnik opisuje sposób wykonywania różnych bardziej zaawansowanych zadań wdrażania, jak dostosowywanie wdrożenia bazy danych w wielu środowiskach, z wyjątkiem plików i folderów z wdrożenia i pobieranie aplikacji sieci web w trybie offline podczas procesu wdrażania .</span><span class="sxs-lookup"><span data-stu-id="051d3-159">This tutorial describes how to accomplish various more advanced deployment tasks, like customizing database deployments for multiple environments, excluding files and folders from deployment, and taking web applications offline during the deployment process.</span></span>

## <a name="where-to-start"></a><span data-ttu-id="051d3-160">Jak zacząć</span><span class="sxs-lookup"><span data-stu-id="051d3-160">Where to Start</span></span>

<span data-ttu-id="051d3-161">Ten zestaw samouczki używa przykładowe rozwiązanie z realistyczne poziom złożoności, oraz scenariusz wdrażania fikcyjnej organizacji do implementacji odwołania i zadania i wskazówki dotyczące typowych kontekstu.</span><span class="sxs-lookup"><span data-stu-id="051d3-161">This set of tutorials uses a sample solution with a realistic level of complexity, together with a fictional enterprise deployment scenario, to provide a reference implementation and to give the tasks and walkthroughs a common context.</span></span> <span data-ttu-id="051d3-162">Następnym temacie [wdrożenia sieci Web w przedsiębiorstwie: omówienie scenariusza](enterprise-web-deployment-scenario-overview.md), wprowadza scenariusza i przykładowe rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="051d3-162">The next topic, [Enterprise Web Deployment: Scenario Overview](enterprise-web-deployment-scenario-overview.md), introduces the scenario and the sample solution.</span></span> <span data-ttu-id="051d3-163">Z tego miejsca pracy za pośrednictwem samouczki i tematy, które najlepiej odpowiadają Twoim potrzebom.</span><span class="sxs-lookup"><span data-stu-id="051d3-163">From there you can work through the tutorials and topics that most closely match your needs.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="051d3-164">Dalej</span><span class="sxs-lookup"><span data-stu-id="051d3-164">Next</span></span>](enterprise-web-deployment-scenario-overview.md)