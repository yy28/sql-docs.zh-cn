---
title: 安全性（报表生成器）| Microsoft Docs
description: 报表生成器安全功能与发布位置、发布的报表、基于它们的外部数据源和模型以及交互式功能相关。
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: ed38291a-6afe-449f-9f32-3ae04502bd6f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1d2c4c195b0d21d2090e13eff578cc533871da4d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "80290837"
---
# <a name="security-report-builder"></a>安全性（报表生成器）
  报表生成器是一类设计用来与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器配合使用的报表创作客户端应用程序。 可以将报表服务器配置为在本机模式中作为独立服务器运行，也可以将报表服务器配置为在 SharePoint 集成模式中运行以支持 SharePoint 站点上的报表。  
  
 在报表生成器中，可以创作报表、共享数据集和可重用的报表部件。 可以从报表服务器或 SharePoint 站点中编辑报表和添加共享数据源、共享数据集和共享报表部件。  
  
 若要创作、发布和使用报表以及与报表相关的项，则应了解安全性功能是如何与以下几个方面相关的：  
  
-   **在其上发布报表的报表服务器或 SharePoint 站点** 这些功能由报表服务器管理员或 SharePoint 站点管理员管理。  
  
-   **已发布的报表以及与报表相关的项** ：与报表相关的项包括嵌入数据源和共享数据源及其凭据、共享数据集、参数、报表部件和报表模型。 应用于这些项的安全性功能由报表作者管理。 报表作者必须获得由报表服务器管理员或 SharePoint 站点管理员授予的足够权限，才能发布和共享项。  
  
-   **报表使用的外部数据源** 这些功能由外部数据源的所有者管理。  
  
-   **基于外部数据源的报表模型** 这些功能由模型设计器管理。  
  
-   **交互式报表功能（如参数）** 这些功能由报表作者管理。  
  
 查看本主题中的信息，更好地了解如何使用安全性功能来帮助管理和保护报表以及与报表相关的项。  
  
##  <a name="understanding-security-for-report-servers"></a><a name="ReportServers"></a> 了解报表服务器的安全性  
 发布报表和查看报表是需要特权的操作。 报表服务器管理员授予权限以确保只有得到授权的用户才能在下列某个类型的报表服务器上发布和查看报表：  
  
-   在本机模式中配置的报表服务器  
  
     若要连接到或浏览到一个报表服务器，您必须具有有效的 URL，并且对该服务器具有足够的访问权限。  
  
     若要在报表服务器上查看或发布项，需将应用于与报表相关的项和操作的权限集组织到角色中。 报表服务器管理员为您分配了一个或多个角色。 例如，利用预定义的角色浏览器，可以查看报表、文件夹、模型和资源。  
  
     如果您无法连接到或浏览到报表服务器，请与报表服务器管理员联系。 有关详细信息，请参阅 [Reporting Services 安全性和保护](../../reporting-services/security/reporting-services-security-and-protection.md)。  
  
-   在 SharePoint 集成模式中配置的报表服务器  
  
     若要连接到与报表服务器集成的 SharePoint 站点，您必须具有 SharePoint 站点或子站点的有效 URL，并且具有对其的足够访问权限。  
  
     通过 SharePoint 安全策略来授予与报表相关的项和操作的访问权限，这些策略可映射拥有与项相关的某个权限级别的用户帐户或组帐户。  
  
     如果您无法连接到或浏览到 SharePoint 站点或子站点，请与 SharePoint 站点管理员联系。  
  
  
##  <a name="understanding-security-for-published-reports-and-report-related-items"></a><a name="Reports"></a> 了解已发布的报表以及与报表相关的项的安全性  
 报表以及与报表相关的项的安全性由报表服务器管理员管理。 与报表相关的项包括嵌入数据源和共享数据源（包括凭据、共享数据集、参数、报表部件和模型）。  
  
 在报表服务器或 SharePoint 站点上，可以单独保护报表以及与报表相关的项和操作。 通过安全策略来授予项和操作的访问权限，这些策略可映射拥有与项相关的某个权限级别的用户帐户或组帐户。 为了降低维护大量策略所带来的复杂性和管理负担，容器（如文件夹）的权限由容器中的项来继承。 例如，如果用户具有某个文件夹的特定“查看报表”权限，则用户具有该文件夹中的项的“查看报表”权限。  
  
 可以使用项级别安全性来覆盖项或文件夹的权限。 在应用项级别安全性时，从父容器进行的权限继承将不再适用于项。 如果对文件夹应用项级别安全性，则嵌套文件夹将继承相同的权限。  
  
 如果无法浏览并找到其他人已为您发布的项，则您对项或文件夹所具有的权限可能有问题。  
  
 为了让其他人能够浏览并找到您已发布的共享项，您必须与报表服务器管理员协作，设置用于为您的用户提供访问权的文件夹组织。 创作报表和运行已发布的报表时必须具有访问权。  
  
 有关详情，请参阅以下主题：  
  
-   [角色和权限 (Reporting Services)](../../reporting-services/security/roles-and-permissions-reporting-services.md)  
  
-   [管理共享数据集](../../reporting-services/report-data/manage-shared-datasets.md)  
  
### <a name="update-notifications-for-report-parts"></a>报表部件的更新通知  
 报表部件将发布到报表服务器以供其他人进行共享。 根据设计来指定将报表部件发布到的位置。  
  
 将报表部件包含在其报表中的用户可以启用更新功能。 在启用此功能后，当报表服务器上的报表部件发生更改时，用户会收到通知。  
  
 如果报表部件是从原始位置移动的，则更新通知将包含报表部件的当前位置和先前位置。 仅接受来自受信任位置的更新。  
  
 有关详细信息，请参阅 [报表部件（报表生成器和 SSRS）](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)。  
  
  
##  <a name="understanding-security-for-report-data-and-external-data-sources"></a><a name="Data"></a> 了解报表数据和外部数据源的安全性  
 若要在报表中访问来自每个外部数据源的数据，请在报表中创建嵌入数据源或添加对共享数据源或共享数据集的引用。  
  
 对于每个外部数据源，您必须提供足以用来访问源和基础数据的凭据。 数据源所有者将指定用于提供此访问的凭据的类型。  
  
 凭据不保存在报表定义中。 将从报表服务器或 SharePoint 站点和报表创作客户端上的报表中独立管理这些凭据。  
  
 在报表设计时，凭据用于运行数据集查询和预览报表。 在运行时，凭据用于运行报表和缓存查询结果。 也可以单独缓存数据集查询结果。 设计时凭据和运行时凭据可能不同。 有关详细信息，请参阅 [在报表生成器中指定凭据](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)。  
  
 有关安全功能的详细信息，请参阅 [SQL Server 数据库引擎和 Azure SQL 数据库的安全中心](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)。 
  
  
 有关数据源的详细信息，请参阅[创建数据连接字符串 - 报表生成器和 SSRS](../report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)。  
  
  
##  <a name="understanding-models-and-security-filters"></a><a name="Models"></a> 了解模型和安全筛选器  
 在从基于外部数据的报表模型中检索数据时，可以在该模型中应用安全筛选器。这是保护数据的好方法，使每个运行报表的用户只能看到其有权使用的数据。  
  
 报表参数不能提供行级安全性；它们并不防止用户或用户组查看特定的数据行。 若要对报表中显示的数据应用安全性，必须使用安全筛选器或模型项安全性。  
  
  
##  <a name="understanding-security-for-report-authoring-for-interactive-features"></a><a name="Interactive"></a> 了解为报表创作交互式功能的安全性  
 报表经常会使用参数，使用户能够以交互方式自定义其报表视图。 使用以下提示可帮助设计遵循良好实践的报表：  
  
-   除非您提供了有效的值，否则不要使用基于查询参数且类型为 **Text** 的参数。 可用值列表可帮助用户只选择有效值。 如果不使用可用值列表，则无法限制用户可输入的值。  
  
-   不要使用全局 [&UserID] 来保护私有数据。 当此值作为报表参数时，可以使用 URL 访问语法在报表 URL 中指定此值。 在共享数据集的表达式中使用此值可防止数据集被缓存。 有关详细信息，请参阅 [URL 访问参数引用](../../reporting-services/url-access-parameter-reference.md)。  
  
 在将项发布到报表服务器后，报表服务器管理员可通过分配基于角色的安全性或文件夹和项级别安全性来帮助保护这些项。 有关详细信息，请参阅 [保护报表和资源](../../reporting-services/security/secure-reports-and-resources.md)。  
  
  
## <a name="see-also"></a>另请参阅  
 [安装报表生成器](../install-windows/install-report-builder.md)  
 [报表参数（报表生成器和报表设计器）](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)  
  
  
