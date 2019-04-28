---
title: 创建、修改和删除共享数据源 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- modifying data source properties
- shared data sources [Reporting Services]
- removing shared data sources
- roles [Reporting Services], shared data sources
- data sources [Reporting Services], shared
- data sources [Reporting Services], modifying properties
- deleting shared data sources
ms.assetid: 1e58c1c2-5ecf-4ce6-9d04-0a8acfba17be
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 26bc12ce8c685c4aeb119f43ab594d920a6cef9f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62697266"
---
# <a name="create-modify-and-delete-shared-data-sources-ssrs"></a>创建、修改和删除共享数据源 (SSRS)
  共享数据源是一组可供在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器上运行的多个报表、模型和数据驱动订阅引用的数据源连接属性。 共享数据源为随时间推移经常发生变化的数据源属性的管理提供了一种简单的方法。 如果用户帐户或密码发生更改，或者如果将数据库移到其他服务器，则可在一个位置对连接信息进行更新。  
  
 对于报表和数据驱动订阅，共享数据源是可选的，但对于报表模型，共享数据源是必需的。 如果计划将报表模型用于特别报告，则必须创建和维护一个共享数据源项才能为此模型提供连接信息。  
  
 共享数据源由以下几个部分组成：  
  
|组成部分|Description|  
|----------|-----------------|  
|“属性”|名称用于在报表服务器文件夹层次结构中标识该项。|  
|Description|说明在您查看文件夹的内容时在报表管理器中与该项一起出现。|  
|连接类型|与数据源一起使用的数据处理扩展插件。 您只能使用部署在报表服务器上的数据处理扩展插件。 有关 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 附带的数据处理扩展插件的详细信息，请参阅 [Reporting Services 支持的数据源 (SSRS)](../create-deploy-and-manage-mobile-and-paginated-reports.md)。|  
|连接字符串|数据库的连接字符串。 有关详细信息并查看常用的数据源的连接字符串示例，请参阅[数据连接、 数据源和 Reporting Services 中的连接字符串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)。|  
|凭据类型|指定如何为连接获取凭据以及在建立连接后是否使用这些凭据。 有关详细信息，请参阅[为报表数据源指定凭据和连接信息](../../integration-services/connection-manager/data-sources.md).|  
  
 共享数据源不包含用于检索数据的查询信息。 查询始终保存在报表定义中。  
  
## <a name="creating-and-modifying-a-shared-data-source"></a>创建和修改共享数据源  
 若要创建共享数据源或修改其属性，必须对报表服务器拥有 **管理数据源** 的权限。 如果报表服务器在本机模式下运行，则可使用报表管理器创建和配置共享数据源。 如果报表服务器在 SharePoint 集成模式下运行，则可使用 SharePoint 站点上的应用程序页。 对于任何报表服务器，不管其模式如何，均可在报表设计器中创建共享数据源，然后将该数据源发布到目标服务器。  
  
 有关创建共享数据源的详细信息，请参阅：  
  
-   [创建嵌入数据源或共享数据源 (SSRS)](../create-an-embedded-or-shared-data-source-ssrs.md)  
  
-   [创建和管理共享数据源（SharePoint 集成模式下的 Reporting Services）](../create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)  
  
 在报表服务器上创建共享数据源后，可通过创建角色分配来控制对该共享数据源的访问、将该共享数据源移到其他位置、对其重命名，或使之脱机以防止在对外部数据源执行维护操作时处理报表。 如果您在报表服务器文件夹层次结构中对共享数据源项重命名，或将其移到其他位置，则引用该共享数据源的所有报表或订阅中的路径信息都会相应更新。 如果使共享数据源脱机，则直到您重新启用该数据源后所有报表、模型和订阅才会运行。  
  
 有关如何控制对报表服务器文件夹层次结构中的共享数据源的访问的详细信息，请参阅 [保护共享数据源项](../security/secure-shared-data-source-items.md)。  
  
## <a name="deleting-a-shared-data-source"></a>删除共享的数据源  
 可使用与从报表服务器删除任何项完全相同的方式来删除共享数据源。 在报表管理器中，您在详细信息视图中打开文件夹，选择该项，然后单击**删除**。 在 SharePoint 站点上的应用程序页上，打开 SharePoint 库、 选择项，然后单击**删除**。  
  
 删除共享数据源将停用所有使用该共享数据源的报表、模型或数据驱动订阅。 在没有数据源连接信息的情况下，这些项将不再运行。 若要激活这些项，必须打开每一项并执行以下操作：  
  
-   对于引用共享数据源的报表和数据驱动订阅，可在报表属性或订阅中指定数据源连接信息，或者选择具有要使用的值的新共享数据源。  
  
-   对于模型和使用该模型的报表生成器报表，必须指定新的共享数据源。 模型只能通过共享数据源获取数据源连接信息。  
  
 若要查看使用数据源的报表和模型的列表，请打开相应共享数据源的“依赖项”页。 在报表管理器或 SharePoint 应用程序页中打开该数据源后即可访问此页。 请注意“依赖项”页不显示数据驱动订阅。 如果共享数据源是由订阅使用，则该订阅将不会显示在依赖项列表中。  
  
 删除共享数据源后没有“撤消”操作可用。 不过，如果您意外删除了一个共享数据源，则可以使用与删除的共享数据源相同的属性值来创建一个新的共享数据源。 您必须打开每个报表、模型和数据驱动订阅才能将该共享数据源重新绑定到使用该共享数据源的项，但是只要这些数据源属性和以前的数据源属性相同，这些报表、模型和订阅便可像以前一样正常使用。  
  
## <a name="see-also"></a>请参阅  
 [创建和管理共享数据源（SharePoint 集成模式下的 Reporting Services）](../create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)   
 [数据连接、 数据源和 Reporting Services 中的连接字符串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [管理报表数据源](manage-report-data-sources.md)   
 [报表管理器（SSRS 本机模式）](../report-manager-ssrs-native-mode.md)   
 [嵌入和共享的数据连接或数据源（报表生成器和 SSRS）](../embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [“数据源”属性页（报表管理器）](../data-sources-properties-page-report-manager.md)   
 [创建、删除或修改共享数据源（报表管理器）](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [配置报表的数据源属性（报表管理器）](configure-data-source-properties-for-a-report-report-manager.md)  
  
  
