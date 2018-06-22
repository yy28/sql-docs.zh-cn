---
title: 数据源属性页 （报表管理器） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f37edda0-19e6-489e-b544-8751fa6b6cfb
caps.latest.revision: 35
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 68279fffed6d42fd60ce6a3665eeaf3b0590aae6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016308"
---
# <a name="data-sources-properties-page-report-manager"></a>“数据源”属性页（报表管理器）
  使用“数据源”属性页可以定义当前报表连接到外部数据源的方式。 您可以覆盖原先与报表一起发布的数据源连接信息。 如果一个报表有多个数据源，则每个数据源在属性页中都有其自己的特定区域。 数据源按照在报表中定义的顺序列出。  
  
 指定报表的数据源时，可以使用从基于该数据源的报表分别创建和管理的共享数据源。 如果不希望使用共享数据源项，则可以定义要与该报表一起使用的数据源连接。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
### <a name="to-open-the-data-sources-properties-page"></a>打开“数据源”属性页  
  
1.  打开报表管理器，找到要为其选择数据源的报表。  
  
2.  悬停在该报表之上，然后单击下拉箭头。  
  
3.  在下拉菜单中，单击 **“管理”**。 这会打开该报表的 **“常规”** 属性页。  
  
4.  选择 **“数据源”** 选项卡。  
  
## <a name="options"></a>“常规”  
 **共享的数据源**  
 指定报表的共享数据源。 有关创建新的数据源的详细信息，请参阅[创建、 删除或修改共享数据源&#40;报表管理器&#41;](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md)。  
  
 **“浏览”**  
 单击 **“浏览”** 可以打开“选择数据源”页（用于选择共享数据源）。 有关详细信息，请参阅[数据源选择页&#40;报表管理器&#41;](../../2014/reporting-services/data-source-selection-page-report-manager.md)。  
  
 **自定义数据源**  
 指定报表连接到数据源的方式。  
  
 下列选项用于指定自定义数据源连接：  
  
 **数据源类型**  
 指定用于处理数据源中数据的数据处理扩展插件。 内置数据扩展插件的列表，请参阅[Reporting services 支持的数据源&#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)。 其他数据处理扩展插件可能由第三方供应商提供。  
  
 **连接字符串**  
 指定报表服务器用于连接到数据源的连接字符串。 连接类型确定应使用的语法。 例如，XML 数据处理扩展插件的连接字符串是 XML 文档的 URL。 在大多数情况下，常见的连接字符串指定数据库服务器和数据文件。 以下示例演示用于连接到名为 MyData 的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库的连接字符串：  
  
 `data source=<a SQL Server instance>;initial catalog=MyData`  
  
 可以将连接字符串配置为表达式，以便可以在运行时指定数据源。 数据源表达式是在报表设计器中的报表中定义的。 不能在报表管理器中定义、查看或修改数据源表达式。 但可以通过单击 **“覆盖默认值”** ，键入静态连接字符串来替换数据源表达式。 如果要切换回原来的表达式，请单击 **“恢复到默认值”**。 报表服务器将存储原始连接字符串，以便在需要时还原。 若要使用数据源表达式，必须使用最初在报表中发布的数据源连接信息。 共享数据源不支持在连接字符串中使用表达式。  
  
 **使用连接**  
 指定如何获取凭据的选项。  
  
> [!IMPORTANT]  
>  如果连接字符串中提供了凭据，则忽略此部分中提供的选项和值。 请注意，如果在连接字符串中指定了凭据，则会向浏览此页的所有用户以明文显示这些值。  
  
 **运行报表的用户提供的凭据**  
 每一名用户都必须键入用户名和密码以访问数据源。 可以定义请求用户凭据的提示文本。 默认的文本字符串为“输入用户名和密码以访问数据源”。  
  
 如果用户提供的凭据为 Windows 身份验证凭据，请选择“在与数据源建立连接时用作 Windows 凭据”  。 如果你使用数据库身份验证不选择此复选框 (例如，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]身份验证)。  
  
 **安全存储在报表服务器中的凭据**  
 在报表服务器数据库中存储加密的用户名和密码。 选择此选项可在无人参与的模式下运行报表（例如，通过计划或事件而不是用户操作来启动报表）。 如果使用默认安全性，则用户名必须为 Windows 域帐户。 按以下格式指定的帐户：\<域 >\\< 用户名\>。 指定的帐户对于用来承载报表所用数据源的计算机必须具有本地登录权限。  
  
 如果凭据为 Windows 身份验证凭据，请选中 **“在与数据源建立连接时用作 Windows 凭据”** 。 如果你使用数据库身份验证不选择此复选框 (例如，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]身份验证)。  
  
 选中 **“与数据源建立连接之后模拟经过身份验证的用户”** 可允许委托凭据，但是只有当数据源支持模拟时才能这样做。 有关[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]数据库，此选项将设置 SETUSER 函数。  
  
> [!TIP]  
>  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]仅支持 Windows 帐户凭据。 因此选择这两种选项"连接到数据源时用作 Windows 凭据使用"和"模拟经过身份验证的用户到数据源建立连接之后"[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]数据源。  
  
 **Windows 集成的安全性**  
 使用当前用户的 Windows 凭据来访问数据源。 如果用于访问数据源的凭据与用于登录到网络域的凭据相同，请选择此选项。 如果您的域启用了 Kerberos 身份验证或者数据源与报表服务器位于同一台计算机上，则此选项最为有效。 如果未启用 Kerberos，则 Windows 凭据可能会传递到其他计算机上。 如果需要其他计算机连接，您将得到错误提示而不是所需的数据。  
  
 报表服务器管理员可以禁止使用 Windows 集成安全性来访问报表数据源。 如果此值显示为灰色，则说明该功能不可用。  
  
 如果您打算计划或订阅此报表，请不要使用此选项。 计划的或无人参与的报表处理需要可以在没有用户输入或当前用户的安全上下文的情况下获取的凭据。 只有存储的凭据才能提供此功能。 因此，如果报表配置为 Windows 集成安全性凭据类型，则报表服务器会禁止您安排对报表或订阅的处理。 如果为已订阅的报表或者具有计划操作的报表选择此选项，则订阅和计划操作将停止。  
  
 **不需要凭据**  
 指定访问数据源不需要使用凭据。 注意，如果数据源要求用户登录，则选择此选项将不起任何作用。 只有在数据源连接不需要用户凭据的情况下，才应选择此选项。  
  
 若要使用此选项，则以前必须为报表服务器部署配置过无人参与的执行帐户。 当其他凭据源不可用时，可以使用无人参与的执行帐户连接到外部数据源。 如果您指定此选项，但是未配置无人参与的执行帐户，则到报表数据源的连接将失败，而且将不会进行报表处理。  有关此帐户的详细信息，请参阅[配置无人参与的执行帐户&#40;SSRS 配置管理器&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)。  
  
 **应用**  
 单击此选项可保存所做的更改。  
  
## <a name="see-also"></a>请参阅  
 [管理报表数据源](report-data/manage-report-data-sources.md)   
 [为报表数据源指定凭据和连接信息](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)  
  
  