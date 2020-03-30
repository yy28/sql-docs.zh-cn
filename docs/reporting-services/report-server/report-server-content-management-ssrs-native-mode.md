---
title: 报表服务器内容管理（本机模式）| Microsoft Docs
ms.date: 06/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- administering Reporting Services
- published reports [Reporting Services], managing
- report servers [Reporting Services], content management
- content management [Reporting Services]
ms.assetid: 641961ac-53a5-4997-9d42-cf4ecce1f892
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 78fb75acfefce3a1f0c8cb28ea286a028463a56b
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "79286381"
---
# <a name="report-server-content-management-ssrs-native-mode"></a>报表服务器内容管理（SSRS 本机模式）
在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，内容管理是指对报表服务器项进行管理。 通过属性和安全设置，所有项可以彼此独立地进行管理。 可以将任何一项移动到报表服务器文件夹命名空间中的不同位置。 为了有效管理项，您需要了解道内容管理员所执行的任务。 从 SQL Server 2016 Reporting Services 或更高版本 (SSRS) CTP 3.2 开始，[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web 门户可用。 本文将介绍 Web 门户和新的 Web 门户体验。  
  
> [!NOTE]  
> 内容管理不同于报表服务器管理。 有关如何管理报表服务器运行环境的详细信息，请参阅 [Reporting Services 报表服务器（本机模式）](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)。  
  
 内容管理包括以下任务：  
  
-   通过应用随 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]提供的基于角色的安全设置，确保报表服务器站点和项的安全。  
  
-   通过添加、修改和删除文件夹创建报表服务器文件夹层次结构。  
  
-   设置应用到报表服务器所管理的项的默认值和属性。 例如，您可以设置确定报表历史记录存储策略的基线最大值。  
  
-   创建共享数据源项，这些数据源项可用来代替报表特定的数据源连接。 发布者或内容管理员可以选择与最初为报表定义的数据源不同的其他数据源；例如用对生产数据库的引用代替对测试数据库的引用。  
  
-   创建可代替报表特定计划和订阅特定计划的共享计划，可以更方便地随时间推移维护计划信息。  
  
-   创建数据驱动订阅，通过从数据存储区中检索数据来生成收件人列表。  
  
-   通过制定报表处理计划，并指定哪些报表按需运行，哪些报表应从缓存加载，从而均衡服务器上的报表处理需求。  
  
-   通过使用以下两个预定义的角色提供执行管理任务的权限： **系统管理员** 和 **内容管理员**。 若要有效地管理报表服务器内容，要求您同时分配有这两个角色。  
  
用于管理报表服务器内容的工具包括 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 或 Web 门户。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 允许您设置默认值和启用功能。 Web 门户用于向用户授予对报表服务器项和操作的访问权限，用于查看和使用报表以及其他内容类型，并用于查看和使用所有共享项和报表分发功能。 Web 门户是更新后的站点，提供了已弃用报表管理器的许多功能。 有关详细信息，请参阅 [Reporting Services 工具](../../reporting-services/tools/reporting-services-tools.md)。  
  
##  <a name="report-server-items"></a><a name="bkmk_ReportServerItems"></a> 报表服务器项  
 报表服务器项包括报表、共享数据源、共享数据库、报表部件、资源（存储在报表服务器上但不由报表服务器处理的项）及文件夹。 项可以依赖其他项，例如，一个报表可以依赖它所引用的共享数据源。 如果您移动一个依赖项，报表服务器会自动更新引用信息。  
  
 您可以将报表服务器项移动到报表服务器文件夹层次结构中的不同位置。 移动项时，所有属性（包括安全设置）也随之移至新的位置。 移动文件夹时，文件夹中的所有项也随之移动。  
  
> [!NOTE]  
>  对于 CTP 3.2，若要移动项的位置，必须在 Web 门户中执行此操作。  
  
 在 Web 门户中，文件夹层次结构指明了可以移动的项。 下图展示了每个可移动项的图标。  
  
  ![用于可移动项的报表服务器图标](media/report-server-content-management-ssrs-native-mode/report-server-content-icons.png)

 并非所有使用的项都可以移动。 不能移动与报表相关联的项，例如订阅或报表历史记录。 这些项随其关联报表一起移动。 同样，也不能移动文件夹层次结构之外的项（如共享计划）。 不具备相应权限时不能移动项。 移动项的权限在你为相关项在角色分配中选择了以下任务时传递：“管理报表”、“管理文件夹”和“管理数据源”。  
  
##  <a name="folders"></a><a name="bkmk_Folders"></a> 文件夹  
 文件夹层次结构用于对报表服务器存储和管理的项进行寻址。  默认情况下，文件夹结构由名为“主文件夹”的根节点和支持可选的“我的报表”功能的保留文件夹组成。 其他文件夹是用户定义的。 如果您需要对多个项授予同一级别的访问权限，则报表服务器文件夹将非常有用。 对文件夹设置的权限可以由文件夹中的项继承到该文件夹中的子文件夹。 例如，您可以在主文件夹下创建一系列文件夹，将组权限分配给每个文件夹，然后让组成员根据需要再组文件夹下自定义文件夹。  
  
 如果使用浏览器直接连接到报表服务器，文件夹结构的根节点就是报表服务器虚拟目录的名称。 从根节点中，您可以根据需要创建、修改和删除文件夹以组织报表服务器内容。 您可以向文件夹添加内容、在文件夹之间移动项、修改文件夹名或位置，还可以删除不再需要的文件夹。  
  
 文件夹是已发布项的虚拟容器，你通过 Web 门户或连接到报表服务器的浏览器访问这些项。 实际上，文件夹及其内容都不在文件系统中， 它们存储在报表服务器数据库中，用户可通过报表服务器 Web 服务端点对其进行访问。 报表服务器文件夹命名空间是一种包括根节点、预定义文件夹和用户定义文件夹的层次结构。 命名空间唯一标识存储在报表服务器上的项。 它提供了在 URL 中指定项的寻址方案。 选择报表或定位到某个报表时，文件夹路径将包含在该报表的 URL 中。  
  
 使用文件夹的方式取决于用户角色分配中的任务。 如果使用默认安全性，则“内容管理员”和“发布者”可以创建和管理文件夹。 如果您使用自定义角色分配，角色分配必须包括支持管理文件夹的任务。 有关角色分配和任务的详细信息，请参阅 [授予对本机模式报表服务器的权限](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md) 和 [任务和权限](../../reporting-services/security/tasks-and-permissions.md)。  
  
 报表服务器文件夹可以包含以下各项：  
  
-   报表  
  
-   共享数据源  
  
-   共享数据集  
  
-   报表部件  
  
-   KPI  
  
-   移动报表  
  
-   资源（存储在报表服务器上但不由报表服务器处理的项）  
  
-   其他文件夹  
  
### <a name="reserved-folders"></a>预留文件夹  
 预定义的文件夹是 Reporting Services 的保留文件夹；您不能移动、重命名或删除它们。 用户定义文件夹包含由特定用户或报表服务器管理员创建的所有文件夹，这些用户或管理员需要具有向文件夹添加项的权限。  
  
 下表对支撑文件夹层次结构并为多种功能提供框架的预定义文件夹进行了说明：  
  
|Folder|目的|  
|------------|-------------|  
|主页|文件夹层次结构的根节点。|  
|用户|在您启用了“我的报表”功能时，将显示此文件夹。 它包含使用“我的报表”功能的所有用户的子文件夹，只有报表服务器管理员才可以访问该文件夹。 每个子文件夹的名称都与相应用户的名称匹配。|  
|我的报表|为每个用户提供个人工作区。|  
  
### <a name="creating-folders"></a>创建文件夹  
 可以在层次结构内的任何可用文件夹中创建文件夹。  
  
 如果创建文件夹的目的是限制对特定报表和模型的访问权限，则应该指定允许用户浏览但不允许他们查看文件夹路径中父文件夹内容的角色分配。  
  
### <a name="modifying-folder-properties"></a>修改文件夹属性  
 创建文件夹之后，您可以通过修改属性来重命名文件夹、添加或修改说明，或将文件夹移至其他位置。 这些属性显示在文件夹的“常规属性”页中。 有关设置授予文件夹访问权限的属性的详细信息，请参阅 [保护文件夹](../../reporting-services/security/secure-folders.md)。  
  
### <a name="deleting-folders-and-folder-contents"></a>删除文件夹和文件夹内容  
 删除文件夹时，会删除其中包含的所有项。 删除文件夹之前，您应该检查其中的内容，确定它是否包含文件夹层次结构中另外部分的其他项可能引用或使用的项。 引用的项包括支持链接报表、共享数据源和资源的报表定义。  
  
 如果删除一个或多个链接报表所引用的报表，链接报表将在删除该报表后失效。 您无法事先确定受影响的链接报表，因为报表并不包含基于它的链接报表的有关信息。 不过，您可以检查链接报表的属性，确定它所基于的报表。 相比之下，共享数据源项则可以列出当前使用该项的所有报表，这样您可以很容易判断出相应的连接信息是否正在使用中。 有关详细信息，请参阅[创建、修改和删除共享数据源 (SSRS)](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)。 最后，报表所用的资源并不能标识这些报表。  
  
 删除文件夹之前，应考虑是否需要保留要删除的任意报表的报表历史记录，或保留报表特定的构件（如数据驱动订阅）。 如果需要任何这方面的信息，请在删除文件夹之前将相应项移出文件夹。  
  
 项在文件夹中的可见性取决于角色分配（即查看项的权限）以及对文件夹有效的查看选项这两个方面。 在 Web 门户中，可以将“内容”页设置为列表视图或详细信息视图。 在某些情况下，可能会在列表视图中隐藏特定报表或项。 在删除某个文件夹的内容之前，请确保先在详细信息视图中查看该文件夹。  
  
##  <a name="resources"></a><a name="bkmk_Resources"></a> Resources  
 资源是指存储在报表服务器上但不由报表服务器处理的托管项。 通常，资源为报表用户提供外部内容。 例如描述报表中所使用业务规则的 .jpg 文件、包含空间数据的 ESRI 形状文件或 HTML 文件中的图像。 JPG、SHP 或 HTML 文件存储在报表服务器上，但报表服务器会将文件直接传递到浏览器，而不会首先对其进行处理。 有关详细信息，请参阅[图像（报表生成器和 SSRS）](../../reporting-services/report-design/images-report-builder-and-ssrs.md)以及[地图（报表生成器和 SSRS）](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)中的“向地图添加数据”部分。  
  
### <a name="adding-and-viewing-a-resource"></a>添加和查看资源  
 若要向报表服务器中添加资源，请上载或发布文件：  
  
|Operation|文件类型|  
|---------------|---------------|  
|上载|若要上传资源，如果报表服务器在本机模式下运行，必须使用 Web 门户；如果报表服务器在 SharePoint 集成模式下运行，必须使用 SharePoint 网站上的应用程序页。 有关详细信息，请参阅[在报表服务器中上传文件或报表](../../reporting-services/reports/upload-a-file-or-report-report-manager.md)，或[将文档上传到 SharePoint 库（SharePoint 模式下的 Reporting Services）](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)。|  
|发布|项目中不是报表、报表部件、数据源或数据集的所有文件都作为资源上载。 若要发布资源，请将现有项添加到报表设计器的一个项目中，然后将该项目发布到报表服务器。|  
  
 所有资源最初都是文件系统中的文件，只是随后上载到报表服务器上而已。 除 ASP.NET 施加的 4 MB 的默认文件大小限制之外，对于可以上载的文件类型没有任何限制。 不过，具有等效 MIME 类型的文件类型比其他类型更适于作为资源发布到报表服务器。 例如，在用户单击基于 HTML 和 JPG 文件的资源时，这些资源将在浏览器窗口中打开，以网页形式呈现 HTML 文件，并以图像形式呈现 JPG 文件，这样，用户就可以看到。 相反，对于不具有等效 MIME 类型的资源（如桌面应用程序文件），则不能在浏览器窗口中呈现。  
  
 报表用户是否可以查看资源取决于浏览器的查看功能。 由于报表服务器不对资源进行处理，因此浏览器必须提供用于呈现特定 MIME 类型的查看功能。 如果浏览器无法呈现资源的内容，则查看资源的用户只能看到资源的常规属性。  
  
### <a name="securing-and-managing-a-resource"></a>保护和管理资源  
 在报表服务器文件夹层次结构中，资源与报表、共享数据源、共享计划和文件夹都以命名项的形式显示在一起。 您可以搜索、查看、保护资源和设置资源属性，就像对报表服务器上存储的任何其他项一样。 若要查看或管理资源，您的角色分配中必须拥有查看资源或管理资源的任务。  
  
### <a name="referencing-an-image-resource-from-a-report"></a>引用报表中的图像资源  
 资源可以包含报表中引用的图像。 如果报表要求包括使用外部图像，则可以考虑将图像存储为资源的以下好处：  
  
-   在报表服务器数据库中集中存储。 如果将报表服务器数据库及其内容移到其他计算机，则外部图像会与报表保存在一起。 无需跟踪不同计算机的磁盘上存储的图像文件。  
  
-   通过角色分配而不是文件系统安全来进行保护。 可以将用于查看报表的权限同样应用于资源。 相反，如果将图像存储在磁盘上，则必须确保匿名用户帐户或无人参与的执行帐户拥有访问该文件的权限。  
  
 若要在报表中使用某个图像资源，请将该图像文件添加到项目，并与报表一起发布。 发布图像之后，可以更新报表中的图像引用，使之指向报表服务器上的相应资源，然后只需重新发布该报表即可保存所做的更改。 随后，即可通过重新发布资源来独立更新报表的图像。 报表将使用报表服务器上可用的最新版本的图像。  
  
 有关详细信息，请参阅[更新资源（Web 门户）](../../reporting-services/report-server/update-a-resource-report-manager.md)。  
  
##  <a name="my-reports"></a><a name="bkmk_MyReports"></a> 我的报表  
 “我的报表”文件夹是使用有效域帐户登录到报表服务器中的用户的个人工作区。 此专用文件夹为制作中的报表、不准备大范围分发的报表或为特定需要定制的报表提供了存储区域。 您不能限制“我的报表”文件夹中存储的项数量或大小，也不能将“我的报表”文件夹配置为在多个用户间共享。  
  
 从技术角度上讲，“我的报表”可以将每个用户看到的虚拟文件夹的名称（“我的报表”）映射到“用户文件夹”文件夹以及基于用户名的唯一子文件夹。 在用户访问自己的“我的报表”文件夹时，该用户实际上要重定向到位于“用户文件夹”下其自己的子文件夹。 每个子文件夹为用户添加到其“我的报表”文件夹中的报表和项提供了存储区。 在 Web 门户中，不会在根级别处看到“我的报表”。 需要深化到“用户”文件夹。  
  
 在安装报表服务器时将创建“用户文件夹”文件夹。 后续基于用户的子文件夹在用户首次打开“我的报表”（例如，单击 Web 门户中的“我的报表”）时创建。 所有文件夹名均采用以下格式：  
  
```  
/Users Folders/<username>/My Reports  
```  
  
 系统只为具有有效系统帐户的用户分配文件夹。 如果用户名包含特殊字符，创建时将使用相应的转义符。 下表列出了相应的转义符：  
  
|字符|转义值|示例|  
|---------------|------------------|-------------|  
|（空格）|[ ]|Firstname Lastname  将变为 Firstname[ ]Lastname |  
|\（反斜杠）|替换为一个空格字符|DomainName\Username  将变为 DomainName Username |  
|@（@ 符号）|[at]|username  @hotmail.com 将变为 username  [at]hotmail.com|  
|&（与号）|[amp]|username  @company  &company.com  将变为 username[at]company[amp]company.com   |  
|$（美元符号）|[dollar]|User*Name* $  将变为 User[ ][dollar]Name  |  
  
 “我的报表”功能是可选的。 安装报表服务器时，默认情况下将禁用“我的报表”功能。 有关启用此功能的详细信息，请参阅 [启用和禁用“我的报表”](../../reporting-services/report-server/enable-and-disable-my-reports.md)。 有关详细信息，请参阅 [保护我的报表](../../reporting-services/security/secure-my-reports.md)。  
  
## <a name="tasks"></a>任务  
 [将文件上载到文件夹](../../reporting-services/report-server/upload-files-to-a-folder.md)  
 [创建、删除或修改文件夹（Web 门户）](../../reporting-services/report-server/create-delete-or-modify-a-folder-web-portal.md)  
 [更新资源（Web 门户）](../../reporting-services/report-server/update-a-resource-report-manager.md)  
 [将文件上载到文件夹](../../reporting-services/report-server/upload-files-to-a-folder.md)  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 工具](../../reporting-services/tools/reporting-services-tools.md)   
 [角色和权限 (Reporting Services)](../../reporting-services/security/roles-and-permissions-reporting-services.md)   
 [Reporting Services 报表 (SSRS)](../../reporting-services/reports/reporting-services-reports-ssrs.md)  
  