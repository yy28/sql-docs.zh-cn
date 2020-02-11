---
title: 管理报表数据源 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], data
- published reports [Reporting Services], data source connections
- shared data sources [Reporting Services]
- data sources [Reporting Services], managing
ms.assetid: 0475aded-c8fe-4337-a2b5-4df0ec4c46af
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 737e5eb03cabe655b4b1dc1da6735b9b4ef68c05
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66107249"
---
# <a name="manage-report-data-sources"></a>管理报表数据源
  在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，报表、报表模型以及数据驱动订阅都从外部数据源检索数据。 若要连接到外部数据源，报表服务器可以使用报表、模型或订阅中定义的或从中引用的数据源连接信息。 数据源连接属性始终在创建报表或模型时通过该报表或模型进行定义，但是可以在将报表或模型发布到报表服务器后对这些属性进行单独管理。  
  
 若要管理报表数据源，对于本机模式下的报表服务器，可使用报表管理器，如果报表服务器部署在 SharePoint 集成模式下，则可以使用 SharePoint 站点上的应用程序页。  
  
 管理数据源连接的特点是包含下列任务，本主题对这些任务进行了介绍：  
  
-   更改连接字符串。  
  
-   更改凭据。  
  
-   在报表服务器上创建和使用共享数据源，包括将嵌入数据源切换为共享数据源。  
  
-   通过设置对报表、模型或所使用的任何共享数据源的权限可以控制对数据源属性的访问。  
  
 请注意，修改查询不是数据源连接管理的一部分。 若要修改报表或模型的查询，必须使用创作工具并在报表或模型定义中进行更改。  
  
## <a name="managed-properties-data-source-type-connection-strings-and-credentials"></a>托管属性：数据源类型、连接字符串和凭据  
 可以在报表服务器上管理的数据源属性为：  
  
|properties|说明|管理方式|  
|--------------|-----------------|----------------------|  
|数据源类型|确定要对外部数据使用的报表服务器数据处理扩展插件。 数据处理器的示例包括 SQL Server、Analysis Services 和 Oracle。|数据源类型是托管属性，因为它是可配置的。 但是，如果要创建新的共享数据源，则应仅配置数据源类型。<br /><br /> 请不要在已发布报表或模型的属性页中更改数据源类型，这样做几乎可以肯定会使连接无效。 不同数据平台上的报表或模型所需的数据结构不太可能相同。|  
|连接字符串|建立到外部数据源的初始连接。 报表可以使用静态或动态连接字符串。<br /><br /> “静态连接字符串” ** 是报表在每次运行时始终用于连接到同一数据源的一组值。<br /><br /> “动态连接字符串” ** 是允许用户选择将要在运行时使用的数据源的报表内置表达式。 在报表设计器中创建报表时，必须将该表达式和数据源选择列表置入该报表中。|更改连接字符串在以下情况中非常有用：将数据源移到另一个计算机中，或如果您使用测试数据创建了报表，但是希望根据生产数据库部署该报表。<br /><br /> 可以通过将原始字符串替换为另一个字符串来管理静态连接字符串。<br /><br /> 若要在报表管理器或 SharePoint 站点中管理动态连接字符串，只能将原始字符串替换为静态字符串。 您不能编辑表达式本身，也不能更改数据源选择列表。 若要更改表达式或有效值列表，必须编辑报表定义并将它重新发布到报表服务器。 有关详细信息，请参阅 [ Reporting Services 中的数据连接、数据源和连接字符串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)。|  
|凭据|提供有权读取数据源中数据的用户名和密码。<br /><br /> 如果数据源不支持身份验证（例如，如果数据源是文件系统中的 XML 文件），则可以配置无人参与的执行帐户，以允许报表服务器在不传递凭据的情况下连接到外部数据源。|可以通过在用户帐户或密码过期时进行更新来管理凭据。<br /><br /> 还可以更改获取凭据的方式（例如，在运行时提示用户输入凭据）。<br /><br /> 如果希望用户能够订阅报表，必须将报表配置为使用存储凭据。|  
  
## <a name="creating-and-using-shared-data-sources"></a>创建和使用共享数据源  
 若要发布数据源属性嵌入其中的报表，请考虑切换到共享数据源属性。 共享数据源更易于管理，因为您可以在一页中更新凭据和连接字符串。 使用该数据源的所有报表、模型和数据驱动订阅会立即拾取这些更改。 还可以使共享数据源处于离线状态，从而有效暂停报表或订阅，以便您在排除故障或调查任何出现的问题时能够阻止报表或订阅运行。  
  
## <a name="controlling-access-data-source-properties"></a>控制访问数据源属性  
 默认情况下，有权管理报表的任何用户都可以设置报表上的任何属性，包括确定数据源类型、连接字符串、凭据的属性以及确定报表获取连接信息的来源是嵌入数据源还是共享数据源。 有关哪些任务和权限可控制对本机模式报表服务器上的数据源属性的访问的详细信息，请参阅 [保护共享数据源项](../security/secure-shared-data-source-items.md) 和 [保护报表和资源](../security/secure-reports-and-resources.md)。  
  
 查看和编辑 SharePoint 库中项属性的权限由站点管理员确定。 有关哪些权限可控制对数据源连接属性的访问的详细信息，请参阅 [报表服务器项的 SharePoint 站点和列表权限参考](../security/sharepoint-site-and-list-permission-reference-for-report-server-items.md)。  
  
## <a name="how-to-work-with-data-source-properties-on-a-report-server"></a>如何在报表服务器上处理数据源属性  
 可以使用多种工具创建和修改数据源属性。 下表汇总了这些方法和工具，并提供指向其他说明的链接。  
  
|任务|工具|链接|  
|----------|----------|----------|  
|查看连接字符串的示例。||[Data Connections, Data Sources, and Connection Strings in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)|  
|选择获取用于连接到数据源的凭据的方法。||[为报表数据源指定凭据和连接信息](specify-credential-and-connection-information-for-report-data-sources.md)|  
|向报表定义 (.rdl) 文件添加数据源连接属性。|报表设计器|[&#40;SSRS 创建嵌入数据源或共享数据源&#41;](../create-an-embedded-or-shared-data-source-ssrs.md)|  
|添加并链接到报表项目中的共享数据源 (.rds) 文件。|报表设计器|[创建、修改和删除共享数据源 (SSRS)](create-modify-and-delete-shared-data-sources-ssrs.md)|  
|创建运行时用户可以选择的预定义的数据源列表。 当用户请求报表时，该报表将提供一个数据源列表。 用户运行报表前必须选择要使用的数据源。 若要向报表添加数据源选择列表，请使用表达式。<br /><br /> 这称为动态数据源连接。|报表设计器|[Data Connections, Data Sources, and Connection Strings in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)|  
|在报表服务器上创建共享数据源项。|报表管理器|[创建、删除或修改共享数据源 &#40;报表管理器&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)|  
|将凭据存储为用于创建订阅或报表快照的必备组件。|报表管理器|[在 Reporting Services 数据源中存储凭据](store-credentials-in-a-reporting-services-data-source.md)|  
|编辑已发布报表的数据源连接属性。|报表管理器|[配置报表的数据源属性 &#40;报表管理器&#41;](configure-data-source-properties-for-a-report-report-manager.md)|  
|在报表服务器上创建共享数据源项。|SharePoint 站点|[在 SharePoint 集成模式下创建和管理共享数据源 &#40;Reporting Services&#41;](../create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)|  
|在报表中使用现有 .odc 连接信息。|SharePoint 站点|[将 Office 数据连接 (.odc) 用于报表（SharePoint 集成模式下的 Reporting Services）](use-an-office-data-connection-odc-with-reports.md)|  
  
> [!NOTE]  
>  管理数据源和报表数据源之间的连接与管理报表服务器和报表服务器数据库之间的连接并不一样。 有关将报表服务器连接到内部数据存储的详细信息，请参阅[配置报表服务器数据库连接（SSRS 配置管理器）](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)。  
  
## <a name="see-also"></a>另请参阅  
 [将报表或模型绑定到共享数据源 &#40;SSRS&#41;](bind-a-report-or-model-to-a-shared-data-source-ssrs.md)   
 [创建、删除或修改共享数据源 &#40;报表管理器&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [在 Reporting Services 数据源中存储凭据](store-credentials-in-a-reporting-services-data-source.md)   
 [Reporting Services 中的数据连接、数据源和连接字符串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Reporting Services &#40;SSRS 支持的数据源&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [报表服务器内容管理（SSRS 本机模式）](../report-server/report-server-content-management-ssrs-native-mode.md)  
  
  
