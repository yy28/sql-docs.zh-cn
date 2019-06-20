---
title: 常规属性页上，共享数据源 （报表管理器） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 1b344449-6f7c-47d2-a737-972d88c0faf8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1de9a0091fa072fccea4825d31deb50463f6cd8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109079"
---
# <a name="general-properties-page-shared-data-sources-report-manager"></a>共享数据源的“常规”属性页（报表管理器）
  使用“常规”属性页可以查看或修改共享数据源项的属性。 单击 **“应用”** 后，对属性所做的任何更改对于引用该项的所有报表都将生效。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
###### <a name="to-open-the-general-properties-page-for-a-shared-data-source"></a>打开共享数据源的“常规属性”页  
  
1.  打开报表管理器，找到您要查看其属性的共享数据源。  
  
2.  悬停在该数据源之上，然后单击下拉箭头。  
  
3.  在下拉菜单中，单击 **“管理”**。 这会打开共享数据源的“常规属性”页。  
  
## <a name="options"></a>选项  
 **名称**  
 指定共享数据源的名称。此名称用于在报表服务器命名空间内标识项。  
  
 **说明**  
 提供有关共享数据源的信息。 此说明显示在“内容”页上。  
  
 **在列表视图中隐藏**  
 选择此选项可对正在报表管理器中使用列表视图模式的用户隐藏共享数据源。 列表视图模式是浏览报表服务器文件夹层次结构时的默认视图格式。 在列表视图中，项的名称和说明可跨越页面。 备用格式为详细信息视图。 详细信息视图省略了说明，但包含项的其他信息。 虽然可以在列表视图中隐藏项，但不能在详细信息视图中隐藏项。 如果希望限制访问项，必须创建角色分配。  
  
 **启用此数据源**  
 选择此选项可以启用或禁用共享数据源。 您可以禁用共享数据源，以防止对引用该项的所有报表、报表模型以及数据驱动订阅进行处理。  
  
 **数据源类型**  
 指定用于处理数据源中数据的数据处理扩展插件。 报表服务器包含 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、Oracle、XML、SAP、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]、ODBC 和 OLE DB 的数据处理扩展插件。 其他数据处理扩展插件可能由第三方供应商提供。  
  
 请注意，如果您使用具有高级服务的 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] Edition，则只能选择 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据源。  
  
 **连接字符串**  
 指定报表服务器用于连接到数据源的连接字符串。 连接类型确定应使用的语法。 例如，XML 数据处理扩展插件的连接字符串是 XML 文档的 URL。 在大多数情况下，常见的连接字符串指定数据库服务器和数据文件。 下面的示例说明了用于连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] 数据库的连接字符串：  
  
```  
data source=<a SQL Server instance>;initial catalog=AdventureWorks2012  
```  
  
 **使用连接**  
 指定如何获取凭据的选项。  
  
> [!IMPORTANT]  
>  如果连接字符串中提供了凭据，则忽略此部分中提供的选项和值。 请注意，如果在连接字符串中指定了凭据，则会向浏览此页的所有用户以明文显示这些值。  
  
 **运行该报表的用户提供的凭据**  
 每一名用户都必须键入用户名和密码以访问数据源。 可以定义请求用户凭据的提示文本。 默认的文本字符串为“输入用户名和密码以访问数据源”。  
  
 如果用户提供的凭据为 Windows 身份验证凭据，请选择“在与数据源建立连接时用作 Windows 凭据”  。 如果使用数据库身份验证（例如 SQL Server 身份验证），请不要选中此复选框。  
  
 **在报表服务器中安全地存储凭据**  
 在报表服务器数据库中存储加密的用户名和密码。 选择此选项可在无人参与的模式下运行报表（例如，通过计划或事件而不是用户操作来启动报表）。 如果使用默认安全性，则用户名必须为 Windows 域帐户。 按以下格式指定帐户：\<域 >\\< 用户名\>。 指定的帐户对于用来承载报表所用数据源的计算机必须具有本地登录权限。  
  
 如果凭据为 Windows 身份验证凭据，请选中 **“在与数据源建立连接时用作 Windows 凭据”** 。 如果使用数据库身份验证（例如 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证），请不要选中此复选框。  
  
 如果使用数据库身份验证，请选中 **“与数据源建立连接之后模拟经过身份验证的用户(连接方式)”** ，以便允许委托数据库凭据，但是只有当数据库服务器支持模拟时才能这样做。 对于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库，此选项将设置 SETUSER 函数。  
  
 **Windows 集成的安全性**  
 使用当前用户的 Windows 凭据来访问数据源。 如果用于访问数据源的凭据与用于登录到网络域的凭据相同，请选择此选项。 如果您的域启用了 Kerberos 或者数据源与报表服务器位于同一台计算机上，则此选项最为有效。 如果未启用 Kerberos，则 Windows 凭据可能会传递到其他计算机上。 如果需要其他计算机连接，您将得到错误提示而不是所需的数据。  
  
 报表服务器管理员可以禁止使用 Windows 集成安全性来访问报表数据源。 如果此值显示为灰色，则说明该功能不可用。  
  
 如果您打算计划或订阅此报表，请不要使用此选项。 计划的或无人参与的报表处理需要可以在没有用户输入或当前用户的安全上下文的情况下获取的凭据。 只有存储的凭据才能提供此功能。 因此，如果报表配置为 Windows 集成安全性凭据类型，则报表服务器会禁止您安排对报表或订阅的处理。 如果为已订阅的报表或者具有计划操作的报表选择此选项，则订阅和计划操作将停止。  
  
 **不需要凭据**  
 指定访问数据源不需要使用凭据。 注意，如果数据源要求用户登录，则选择此选项将不起任何作用。 只有在数据源连接不需要用户凭据的情况下，才应选择此选项。  
  
 若要使用此选项，则以前必须为报表服务器部署配置过无人参与的执行帐户。 当其他凭据源不可用时，可以使用无人参与的执行帐户连接到外部数据源。 如果您指定此选项，但是未配置无人参与的执行帐户，则到报表数据源的连接将失败，而且将不会进行报表处理。 有关此帐户的详细信息，请参阅[配置无人参与的执行帐户&#40;SSRS 配置管理器&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)。  
  
 **Apply**  
 单击此选项可保存所做的更改。  
  
 **删除**  
 单击此选项可删除共享数据源。 删除共享数据源将停用使用该共享数据源的所有报表、模型和数据驱动订阅。 若要重新激活报表、模型和订阅，必须打开每个报表、模型或订阅，并将其数据源属性更新为使用其他共享数据源。 对于报表和订阅，可以将数据源连接信息指定为数据源属性值。  
  
 **“移动”**  
 单击此选项可将共享数据源移至报表服务器文件夹命名空间中的其他位置。  
  
 **生成模型**  
 单击此选项可基于共享数据源创建新模型。  
  
## <a name="see-also"></a>请参阅  
 [报表管理器（SSRS 本机模式）](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [“新建数据源”页（报表管理器）](../../2014/reporting-services/new-data-source-page-report-manager.md)   
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)   
 [为报表数据源指定凭据和连接信息](report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
  
