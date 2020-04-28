---
title: 部署清单： PowerPivot for SharePoint 2010 的多服务器安装 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 4380040a-1368-4a47-8930-47c65a192e59
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: ed0cd8bad3a99c7f1f59b5121aafb06ccdee63b2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "71952243"
---
# <a name="deployment-checklist-multi-server-installation-of-powerpivot-for-sharepoint-2010"></a>部署核对清单：PowerPivot for SharePoint 2010 的多服务器安装
  此核对清单将指导你完成将 for [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] SharePoint 添加到从头开始生成的三层 sharepoint 2010 场的步骤。 一个三层场包括数据库层、应用程序层和 Web 层。 若[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]要添加到此拓扑中，需要运行 SQL Server 安装[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]程序以在应用程序层上安装。 PowerPivot 程序文件将添加到 web 层中，但仅在部署 web 应用程序解决方案时作为安装后任务。 尽管这些是部署步骤，但对于 Web 层或数据层而言，并没有需要执行的单独的安装步骤。 你需要执行的唯一安装步骤是在应用程序[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]服务器上安装。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2010|  
  
  
  
## <a name="prerequisites"></a>先决条件  
 您必须是本地管理员才能安装 SQL Server 和 SharePoint 2010。  
  
 还必须由安装 SharePoint 的人员来配置场。 若要配置场，您必须具有数据库服务器的 SQL Server 登录名。 必须将此登录名分配给以下角色：`dbcreator`、`securityadmin` 和 `public`。  
  
 您必须具有 SharePoint Server 2010 的企业版或企业评估版。  
  
 必须将计算机加入到域中。  
  
 您必须了解将用于运行数据库引擎、场中的服务以及 SharePoint 集成模式下的 Analysis Services 的帐户。 尽管稍后您可以更改这些帐户，但在首次安装时应指定这些帐户。  
  
 您在安装过程中指定的服务帐户必须是域用户帐户。  
  
 开始安装前，请检查您的浏览器设置以确认您具有 Internet 连接。 必备安装程序将打开 Internet 连接以下载所需的软件。 您应进行以下更改，以确保获取所有必需的软件：  
  
-   在服务器管理器中，暂时禁用 Internet Explorer 增强安全性配置，以允许下载到服务器。 为了下载所需软件，您可以仅对管理员关闭 IE ESC。  
  
-   在 Internet Explorer 中，可能还需要将浏览器配置为跳过代理服务器，以允许 localhost 访问 Internet URL。  
  
    1.  在 Internet Explorer 中的“工具”菜单上，单击“Internet 选项”。  
  
    2.  在“局域网 (LAN) 设置”区域的“连接”选项卡上，单击“局域网设置”。  
  
    3.  在“自动配置”区域中，清除“自动检测设置”复选框。  
  
    4.  在“代理服务器”区域中，选中“为 LAN 使用代理服务器”复选框。  
  
    5.  在“地址”框中键入代理服务器的地址。  
  
    6.  在“端口”框中键入代理服务器的端口号。  
  
    7.  选中“跳过本地地址的代理服务器”复选框。  
  
    8.  单击“确定”以关闭“局域网 (LAN) 设置”对话框。  
  
    9. 单击“确定”以关闭“Internet 选项”对话框。  
  
##  <a name="install-a-database-server"></a><a name="installdb"></a>安装数据库服务器  
 本主题假定您的场拓扑基于为[三层场的多个服务器](https://go.microsoft.com/fwlink/?LinkId=182771)一文中所述的拓扑。 如果你已有可正常运行的场，请直接跳到[安装 PowerPivot for SharePoint](#installppapp)。  
  
 如果您刚开始接触拓扑，请从安装 SQL Server 数据库引擎着手。 按照这些说明操作将生成一个可由场中的 SharePoint 服务器访问的数据库服务器。  
  
1.  在要用于数据库服务器的计算机上，运行 SQL Server 安装程序以安装 SQL Server 数据库引擎（请参阅安装[向导 &#40;安装程序&#41;安装 SQL Server 2014 ](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)）。  
  
     在选择要安装的功能时，请选择以下选项：  
  
    -   数据库引擎服务  
  
    -   客户端工具连接  
  
    -   管理工具 – 完整（将自动包含基本组件）  
  
2.  在数据库引擎安装完成后，对远程连接启用 TCP/IP，然后重新启动该服务：  
  
    1.  启动 SQL Server 配置管理器。  
  
    2.  打开“SQL Server 网络配置”。  
  
    3.  选择“MSSQLSERVER 的协议”  。  
  
    4.  右键单击 " **tcp/ip** "，然后选择 "**启用**"。  
  
    5.  单击 " **SQL Server 服务**"。  
  
    6.  右键单击**SQL Server （MSSQLSERVER）**，然后单击 "**重新启动**"。  
  
3.  启用通过 Windows 防火墙对数据库服务器进行入站访问。 这使场中的 SharePoint 服务器可以连接到 SharePoint 数据库。 有关详细信息，请参阅 [配置 Windows 防火墙以允许 SQL Server 访问](../../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)。  
  
    1.  在 Windows "控制面板" 的 "管理工具" 中，单击 "**高级安全 Windows 防火墙**"。  
  
    2.  单击 **“入站规则”**。  
  
    3.  单击 "**新建规则**"。  
  
    4.  在 "规则类型" 中，单击 "**自定义**"。  
  
    5.  单击“下一步”。   
  
    6.  在程序的 "服务" 部分中，单击 "**自定义**"。  
  
    7.  单击 "**应用到此服务**"。  
  
    8.  如果已将 SQL Server 作为默认实例安装，请选择 " **SQL Server （MSSQLSERVER）** "，然后单击 **"确定"**。  
  
    9. 单击“下一步”。   
  
    10. 在 "协议和端口" 中，接受默认设置，然后单击 "**下一步**"。  
  
    11. 在 "作用域" 中，接受默认设置，然后单击 "**下一步**"。  
  
    12. 在 "操作" 中，接受默认设置，然后单击 "**下一步**"。  
  
    13. 在 "配置文件" 中，清除 "**专用**" 和 "**公用**" 复选框，然后单击 "**下一步**"  
  
    14. 在 "名称" 中，为入站规则键入说明性名称（例如**SQL Server**）。  
  
    15. 单击 **“完成”** 。  
  
##  <a name="install-and-configure-a-three-tier-sharepoint-2010-farm"></a><a name="installsp"></a>安装和配置三层 SharePoint 2010 场  
 在用作 SharePoint 服务器的每台计算机上，运行 SharePoint Prerequisite Installer 程序，然后运行 SharePoint Server 安装程序。  
  
 使用 SharePoint 2010 文档中的以下说明来安装和配置 SharePoint 2010 场，该场包含两个 Web 服务器和一个应用程序服务器：  
  
 [三层服务器场的多个服务器（SharePoint Server 2010）](https://go.microsoft.com/fwlink/?LinkId=182771)  
  
 在系统要求您指定数据库服务器时，指定前面安装的数据库服务器。  
  
 在下列过程中，假定已使用为三层场安装程序提供的说明配置了该场。 该场应包含以下服务和功能：  
  
-   Excel Services、搜索服务和 Secure Store Service  
  
-   一个 Web 应用程序和网站集  
  
-   使用情况和运行状况数据收集  
  
-   诊断日志记录  
  
##  <a name="install-powerpivot-for-sharepoint-on-an-application-server"></a><a name="installppapp"></a>在应用程序服务器上安装 PowerPivot for SharePoint  
 运行 SQL Server 安装程序以便将 PowerPivot for SharePoint 添加到某一 SharePoint 场。 如果该场由多个 SharePoint 服务器构成，则必须在已加入到该场中的应用程序服务器上运行 SQL Server 安装程序。  
  
 始终在应用程序服务器上安装 PowerPivot for SharePoint。 虽然 Web 前端服务器也将运行 PowerPivot for SharePoint 服务器组件，但在 Web 前端上运行的组件是在场中部署解决方案时，在执行 PowerPivot for SharePoint 配置步骤期间安装的。 有关设置的详细信息，请参阅[Install PowerPivot for SharePoint 2010](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md)。  
  
 如果您的部署拓扑要求两个 PowerPivot for SharePoint 实例，请在每台应用程序服务器上运行 SQL Server 安装程序。 一台计算机上只能有一个 PowerPivot for SharePoint 实例。 如果您需要多个实例，则必须使用其他服务器。 有关将多个 PowerPivot for SharePoint 服务器添加到同一个场的详细信息，请参阅[部署清单：通过将 PowerPivot 服务器添加到 SharePoint 2010 场进行扩展](../../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md)。  
  
##  <a name="install-analysis-services-client-libraries-on-sharepoint-applications-servers-that-do-not-have-an-installation-of-powerpivot-for-sharepoint"></a><a name="installclientlib"></a>在未安装 PowerPivot for SharePoint 的 SharePoint 应用程序服务器上安装 Analysis Services 客户端库  
 场拓扑（包含运行以下应用程序的 Web 前端或应用程序服务器，但未在同一台计算机上安装 PowerPivot for SharePoint）将要求附加的软件以便支持 PowerPivot 数据访问和功能：  
  
-   Excel Services 或 PerformancePoint Services  
  
-   在自己的服务器上作为独立应用程序运行的管理中心  
  
 Excel Services 和 PerformancePoint Services 都要求 Analysis Services OLE DB 访问接口的较新版本以便支持 PowerPivot 数据访问。 如果您在不具有最新 OLE DB 访问接口的计算机上运行上述任一应用程序，则必须手动安装访问接口。 有关详细信息，请参阅[在 SharePoint 服务器上安装 Analysis Services OLE DB Provider](../../../2014/sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)  
  
 同样，如果一台计算机上仅具有管理中心，而没有 PowerPivot for SharePoint，则要求 ADOMD.NET 客户端库。 PowerPivot 管理面板使用此库来访问它用于填充面板的内部数据。 有关详细信息，请参阅 [在运行管理中心的 Web 前端服务器上安装 ADOMD.NET](../../../2014/sql-server/install/install-adomd-net-on-web-front-end-servers-running-central-administration.md)。  
  
##  <a name="configure-the-server"></a><a name="configsrvr"></a>配置服务器  
 使用 PowerPivot 配置工具来配置 PowerPivot for SharePoint。 该工具将扫描场的现有配置，并提供安装或激活 PowerPivot for SharePoint 所需的 SharePoint 功能的选项。 在此步骤中，将启动 Claims to Windows Token Service。 此外，如果其他必需的 SharePoint 功能尚未启用，配置工具会将这些功能添加到列表中，并提供用于启用这些功能的操作。  
  
 有关详细信息，请参阅[PowerPivot for SharePoint 2010 &#40;PowerPivot 配置工具&#41;中配置或修复](../../../2014/analysis-services/configure-repair-powerpivot-sharepoint-2010.md)。  
  
##  <a name="configure-alternate-access-mapping-for-web-front-end-servers"></a><a name="AAM"></a>为 Web 前端服务器配置备用访问映射  
 为了确保每台 Web 前端服务器都可处理 PowerPivot 数据访问或数据刷新请求，必须将每台服务器的不同 URL 映射到同一个 Web 应用程序。  
  
1.  在 "管理中心" 的 "应用程序管理" 中，单击 "**配置备用访问映射**"。  
  
2.  在“备用访问映射集”中，选择您的 Web 应用程序。  
  
3.  单击 "**添加内部 URL**"。  
  
4.  指定第一个 Web 前端服务器的 URL。  
  
5.  重复上述步骤以添加第二个 Web 前端服务器的 URL。  
  
##  <a name="activate-powerpivot-feature-integration-for-site-collections"></a><a name="activatePP"></a>激活网站集的 PowerPivot 功能集成  
 网站集级别的功能激活使应用程序页和模板可用于您的站点，包括用于计划的数据刷新的配置页以及用于 PowerPivot 库和数据馈送库的应用程序页。  
  
 PowerPivot 配置工具将针对您指定的网站集激活功能集成。 您可以多次运行该工具以选择其他网站集。 此外，站点管理员还可以从 SharePoint 中配置功能激活。 有关详细信息，请参阅[在管理中心为网站集激活 PowerPivot 功能集成](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca)。  
  
##  <a name="verify-integration-and-server-availability"></a><a name="verify"></a>验证集成和服务器可用性  
 当用户或应用程序打开包含 PowerPivot 数据的 Excel 工作簿时，在场中发生 PowerPivot 查询处理。 至少，您可以检查 SharePoint 网站上的页面以便确认 PowerPivot 功能可用。 但是，若要完全验证某一安装，您必须具有可发布到 SharePoint 并从库中访问的 PowerPivot 工作簿。 出于测试目的，您可以发布已包含 PowerPivot 数据的示例工作簿并使用它来确认 SharePoint 集成已正确配置。  
  
 若要验证 PowerPivot 与 SharePoint 网站的集成，请执行以下操作：  
  
1.  在浏览器中，打开您创建的 Web 应用程序。 如果使用了默认值，则可以在 URL\<地址中指定 http://计算机名>。  
  
2.  验证 PowerPivot 数据访问和处理功能在应用程序中可用。 您可以通过验证 PowerPivot 提供的库模板是否存在来验证此可用性：  
  
    1.  在 "网站操作" 上，单击 "**更多选项 ...**"  
  
    2.  在 "库" 中，应会看到 "**数据馈送库**" 和 " **PowerPivot 库**"。 这些库模板由 PowerPivot 功能提供，并且在正确集成了该功能的情况下在“库”列表中将可见。  
  
 若要验证服务器上的 PowerPivot 数据访问，请执行以下操作：  
  
1.  [下载](https://go.microsoft.com/fwlink/?LinkID=219108) Reporting Services 教程附带的“野餐”数据示例。 您将使用此下载中的示例工作簿来验证 PowerPivot 数据访问。 解压缩文件。  
  
2.  将 PowerPivot 工作簿上载到 PowerPivot 库或任何 SharePoint 库。  
  
3.  单击该文档以便从库中打开它。  
  
4.  单击某个切片器或对数据进行筛选以启动 PowerPivot 查询。 该服务器将在后台加载 PowerPivot 数据并返回结果。 在下一步骤中，您将连接到该服务器以便确认数据已加载并且缓存。  
  
5.  从“开始”菜单中的 Microsoft SQL Server 2008 R2 程序组启动 SQL Server Management Studio。 如果未在您的服务器上安装此工具，则可以跳到最后一步以便确认缓存文件是否存在。  
  
6.  在“服务器类型”中，选择 **“Analysis Services”**。  
  
7.  在 "服务器名称" 中，输入** \<服务器名称> \powerpivot**，其中** \<，服务器名称>** 是安装了 PowerPivot for SharePoint 的计算机的名称。  
  
8.  单击“连接”  。  
  
9. 在对象资源管理器中，单击 "**数据库**" 查看加载的 PowerPivot 数据文件的列表。  
  
10. 在计算机文件系统上，检查以下文件夹以便确定文件是否已缓存到磁盘。 存在缓存文件将进一步证实您的部署正常工作。 若要查看文件缓存，请转到 \Program Files\Microsoft SQL Server\MSAS10_50.POWERPIVOT\OLAP\Backup 文件夹。  
  
##  <a name="post-installation-steps"></a><a name="nextsteps"></a>安装后步骤  
 在验证了安装后，通过创建 PowerPivot 库或优化单独的配置设置完成服务配置。 为了充分利用您刚安装的服务器组件，可以下载 [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] 以便创建然后发布您的第一个 PowerPivot 工作簿。  
  
####  <a name="set-upper-limits-on-disk-space-usage"></a><a name="bkmk_disk"></a>设置磁盘空间使用情况的上限  
 您可以为用于缓存到磁盘的 PowerPivot 数据文件的磁盘空间量设置一个上限。 默认设置是使用所有可用磁盘空间量。 有关如何限制磁盘空间使用情况的说明，请参阅[&#40;PowerPivot for SharePoint 配置磁盘空间使用情况&#41;](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-disk-space-usage-power-pivot-for-sharepoint)。  
  
####  <a name="increase-file-maximum-upload-size-for-sharepoint-web-applications"></a><a name="Upload"></a>增加 SharePoint Web 应用程序的最大文件上载大小  
 因为 PowerPivot 工作簿可能很大，所以，您可能要增加最大文件上载大小。 有两个要配置的文件大小设置：针对 Web 应用程序的“最大上载大小”和 Excel Services 中的“最大工作簿大小”。 在这两个应用程序中，最大文件大小应该设置为相同值。 有关说明，请参阅[&#40;PowerPivot for SharePoint&#41;配置最大文件上传大小](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint)。  
  
#### <a name="grant-sharepoint-permissions-to-workbook-users"></a>向工作簿用户授予 SharePoint 权限  
 用户将首先需要 SharePoint 权限，然后才能发布或查看工作簿。 请确保向需要查看已发布工作簿的用户授予 "**查看**" 权限，**并向**发布或管理工作簿的用户提供权限。 您必须是网站集管理员才能授予权限。  
  
1.  在网站中，单击 **“网站操作”**。  
  
2.  单击 **“网站权限”**。  
  
3.  选中 "网站集**成员**" 组的复选框。  
  
4.  在功能区上，单击 "**授予权限**"。  
  
5.  输入应有权添加或删除文档的 Windows 域用户或组帐户。  
  
6.  单击“确定”。   
  
7.  选中 "网站集**访问者**" 组的复选框。  
  
8.  在功能区上，单击 "**授予权限**"。  
  
9. 输入应有权查看文档的 Windows 域用户或组帐户。 与前面一样，如果将应用程序配置为采用经典身份验证，则不要使用电子邮件地址或分发组。  
  
10. 单击“确定”。   
  
#### <a name="install-adonet-data-services-35-sp1"></a>安装 ADO.NET Data Services 3.5 SP1  
 ADO.NET Data Services 是 SharePoint 列表的数据馈送导出所必需的。 SharePoint 2010 在 PrerequisiteInstaller 程序中不包括此组件，因此您必须手动安装它。 有关如何安装 ADO.NET 数据服务的详细信息，请参阅[安装 ADO.NET Data services 以支持 SharePoint 列表的数据馈送导出](../../../2014/sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md)。  
  
#### <a name="install-data-providers-used-in-data-refresh-and-check-user-permissions"></a>安装数据刷新中使用的数据访问接口和检查用户权限  
 服务器端数据刷新使用户可以在无人参与模式下将更新后的数据重新导入到其工作簿中。 为了成功执行数据刷新，服务器必须具有用于最初导入数据的同一个数据访问接口。 此外，运行数据刷新的用户帐户通常需要对外部数据源具有读取权限。 请务必检查启用和配置数据刷新的要求，以确保获得成功结果。 有关详细信息，请参阅[通过 SharePoint 2010 进行 PowerPivot 数据刷新](../../../2014/analysis-services/powerpivot-data-refresh-with-sharepoint-2010.md)。  
  
#### <a name="create-a-powerpivot-gallery"></a>创建 PowerPivot 库  
 PowerPivot 库是包括预览和展示选项以便在 SharePoint 网站上查看 PowerPivot 工作簿的一种库。 使用 PowerPivot 库可以发布和查看为其预览功能推荐的 PowerPivot 工作簿。 此外，如果您还将 Reporting Services 部署到了同一 SharePoint 服务器上，则 PowerPivot 库将简化创建报表的工作。 您可以从 PowerPivot 库内启动报表生成器，以便在已发布的 PowerPivot 工作簿的基础上创建新的报表。 有关创建和使用库的详细信息，请参阅[创建和自定义 Powerpivot 库](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/create-and-customize-power-pivot-gallery)并[使用 powerpivot 库](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/use-power-pivot-gallery)。  
  
#### <a name="tune-configuration-settings"></a>优化配置设置  
 PowerPivot 服务应用程序使用默认属性和值创建。 您可以修改单独服务应用程序的配置设置，以便更改分配请求所采用的方法、设置服务器超时、更改查询响应报告事件的阈值或者指定保留多长时间的使用情况数据。 有关管理中心中的配置或者在 SharePoint Web 应用程序中使用 PowerPivot 功能的详细信息，请参阅[在管理中心中管理和配置 Powerpivot 服务器](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 2012 的各个版本支持的功能](https://go.microsoft.com/fwlink/?linkid=232473)   
 [安装 PowerPivot for SharePoint 2010](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md)   
 [部署清单：通过将 PowerPivot 服务器添加到 SharePoint 2010 场进行扩展](../../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md)  
  
  
