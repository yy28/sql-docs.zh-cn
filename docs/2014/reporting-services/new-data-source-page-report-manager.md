---
title: 新建数据源页 （报表管理器） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 35563d4c-a3d5-4f95-bf46-605da9dfcbb8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3128dee728cbb2e9eda6e87232675558fe9413e3
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59947084"
---
# <a name="new-data-source-page-report-manager"></a>“新建数据源”页（报表管理器）
  使用“新建数据源”页，可以创建共享数据源项。 共享数据源定义与外部数据源的连接。 使用共享数据源，可以从使用该数据源的报表、模型和数据驱动订阅分别创建和维护数据源连接设置。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
###### <a name="to-open-the-new-data-source-page"></a>打开“新建数据源”页  
  
1.  打开报表管理器，导航到要在其中创建数据源的文件夹。  
  
2.  在工具栏中，单击 **“新建数据源”**。 必须具有“内容管理员”权限才能创建共享数据源。  
  
## <a name="options"></a>选项  
 **名称**  
 键入共享数据源的名称。此名称用于标识报表服务器文件夹层次结构内的项。  
  
 **说明**  
 提供有关共享数据源的信息。 此说明显示在“内容”页上。  
  
 **在列表视图中隐藏**  
 选择此选项可对正在报表管理器中使用列表视图模式的用户隐藏共享数据源。 列表视图模式是浏览报表服务器文件夹层次结构时的默认视图格式。 在列表视图中，项的名称和说明可跨越页面。 备用格式为详细信息视图。 详细信息视图省略了说明，但包含项的其他信息。 虽然可以在列表视图中隐藏项，但不能在详细信息视图中隐藏项。 如果希望限制对项的访问，则必须创建角色分配。  
  
 **启用此数据源**  
 选择此选项可以启用或禁用共享数据源。 您可以禁用共享数据源，以防止对引用该项的所有报表和模型进行处理。  
  
 **数据源类型**  
 指定用于处理数据源中数据的数据处理扩展插件。 报表服务器包含 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、Oracle、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]、SAP、XML、ODBC 和 OLE DB 的数据处理扩展插件。 其他数据处理扩展插件可能由第三方供应商提供。  
  
 有关远程和非 SQL 数据源支持的详细信息，请参阅[SQL Server 2012 各个版本支持的功能](https://go.microsoft.com/fwlink/?linkid=232473)(超链接"<https://go.microsoft.com/fwlink/?linkid=232473>" <https://go.microsoft.com/fwlink/?linkid=232473>) 和[支持的报表数据源服务&#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)。  
  
 **连接字符串**  
 指定报表服务器用于连接到数据源的连接字符串。 连接类型确定应使用的语法。 例如，XML 数据处理扩展插件的连接字符串是 XML 文档的 URL。 在大多数情况下，常见的连接字符串指定数据库服务器和数据文件。  
  
 下面的示例说明了用于连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] 数据库的连接字符串：  
  
```  
data source=<a SQL Server instance>;initial catalog=AdventureWorks2012  
```  
  
 有关更多示例和不同的方式指定连接字符串的信息，请参阅[数据连接、 数据源和 Reporting Services 中的连接字符串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)。  
  
 **使用连接**  
 指定设置凭据获取方式的选项。  
  
> [!IMPORTANT]  
>  如果连接字符串中提供了凭据，则忽略此部分中提供的选项和值。 请注意，如果在连接字符串中指定了凭据，则会向浏览此页的所有用户以明文显示这些值。  
  
 **提供运行报表 （连接方式） 的用户的凭据**  
 系统将提示每位用户键入用户名和密码，以访问数据源。 可以定义请求用户凭据的提示文本。 默认的文本字符串为“输入用户名和密码以访问数据源”。  
  
 如果用户提供的凭据为 Windows 身份验证凭据，请选择“在与数据源建立连接时用作 Windows 凭据”  。 如果使用数据库身份验证（例如 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证），请不要选中此复选框。  
  
 **凭据安全地存储在报表服务器 （连接方式）**  
 在报表服务器数据库中存储加密的用户名和密码。 选择此选项可在无人参与的模式下运行报表（例如，通过计划或事件而不是用户操作来启动报表）。 如果使用默认安全性，则用户名必须为 Windows 域帐户。 按以下格式指定帐户：\<域 >\\< 用户名\>。 指定的帐户对于用来承载报表所用数据源的计算机必须具有本地登录权限。  
  
 如果凭据为 Windows 身份验证凭据，请选中 **“在与数据源建立连接时用作 Windows 凭据”** 。 如果使用数据库身份验证（例如 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证），请不要选中此复选框。  
  
 如果使用数据库身份验证，请选择 **“与数据源建立连接之后模拟经过身份验证的用户”** ，以便允许委托数据库凭据，但是只有当数据库服务器支持模拟时才能这样做。 对于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库，此选项将设置 SETUSER 函数。  
  
 **Windows 集成的安全性 （连接方式）**  
 使用当前用户的 Windows 凭据来访问数据源。 如果用于访问数据源的凭据与用于登录到网络域的凭据相同，请选择此选项。 如果您的域启用了 Kerberos 身份验证或者数据源与报表服务器位于同一台计算机上，则此选项最为有效。 如果未启用 Kerberos 身份验证，则可以将 Windows 凭据传递到其他计算机上。 如果需要其他计算机连接，您将得到错误提示而不是所需的数据。  
  
 报表服务器管理员可以禁止使用 Windows 集成安全性来访问报表数据源。 如果此值显示为灰色，则说明该功能不可用。  
  
 如果您打算计划或订阅此报表，请不要使用此选项。 计划的或无人参与的报表处理需要可以在没有用户输入或当前用户的安全上下文的情况下获取的凭据。 只有存储的凭据才能提供此功能。 因此，如果报表配置为 Windows 集成安全性凭据类型，则报表服务器会禁止您安排对报表或订阅的处理。 如果为已订阅的报表或者具有计划操作的报表选择此选项，则订阅和计划操作将停止。  
  
 **不需要凭据 （连接方式）**  
 指定访问数据源不需要使用凭据。 注意，如果数据源要求用户登录，则选择此选项将不起任何作用。 只有在数据源连接不需要用户凭据的情况下，才应选择此选项。  
  
 若要使用此选项，则以前必须为报表服务器部署配置过无人参与的执行帐户。 当其他凭据源不可用时，可以使用无人参与的执行帐户连接到外部数据源。 如果您指定此选项，但是未配置无人参与的执行帐户，则到报表数据源的连接将失败，而且将不会进行报表处理。 有关此帐户的详细信息，请参阅[配置无人参与的执行帐户&#40;SSRS 配置管理器&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)。  
  
 **确定**  
 单击此选项可保存所做的更改。  
  
## <a name="see-also"></a>请参阅  
 [创建、删除或修改共享数据源（报表管理器）](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [数据连接、 数据源和 Reporting Services 中的连接字符串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [报表管理器（SSRS 本机模式）](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [“内容”页（报表管理器）](../../2014/reporting-services/contents-page-report-manager.md)   
 [创建、修改和删除共享数据源 (SSRS)](report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)   
 [为报表数据源指定凭据和连接信息](report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
  
