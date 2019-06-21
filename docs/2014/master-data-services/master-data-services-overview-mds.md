---
title: Master Data Services 概述 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- Master Data Services, overview
- Master Data Services
ms.assetid: 8a4c28b1-6061-4850-80b6-132438b8c156
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 982f8a3d91a5f594658b4ec911bcbc78f62e9f1d
ms.sourcegitcommit: 0818f6cc435519699866db07c49133488af323f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284998"
---
# <a name="master-data-services-overview"></a>Master Data Services 概述
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，模型是你的主数据结构中的最高级别的容器。 创建一个模型来管理类似数据的组，例如管理联机产品数据。 模型包含一个或多个实体，而实体包含属于数据记录的成员。  
  
|||  
|-|-|  
|![Azure 虚拟机](../../2014/master-data-services/media/azure-virtual-machine.png "Azure 虚拟机")|是否想要试用 SQL Server 2016？ 注册 Microsoft Azure，然后转到 **[此处](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)** 以加速已安装有 SQL Server 2016 的虚拟机。 完成后，可以删除虚拟机。|  
  
 例如，你的在线产品模型可能包含多个实体（如 Product、Color 和 Style）。 Color 实体可以含有红色、银色和黑色成员。  
  
 ![具有颜色实体的产品型号](../../2014/master-data-services/media/mds-colorentity-productmodel.png "具有颜色实体的产品型号")  
  
 模型还包含实体中定义的属性。 属性包含可帮助描述实体成员的值。 存在自由格式的属性和基于域的属性。  基于域的属性包含实体成员填充的值，并且可用作其他实体的属性值。  
  
 例如，Product 实体可能具有针对 Cost 和 Weight 的自由格式的属性。 并且，存在颜色的基于域的属性，该颜色包含 Color 实体成员填充的值。 此颜色主列表将用作 Product 实体的属性值。  
  
 ![使用颜色基于域的属性的 product 实体](../../2014/master-data-services/media/mds-productentity-colorattribute.png "Product 实体具有颜色的基于域的属性")  
  
 派生的层次结构来自模型中各个实体之间的关系。 这些都是基于域的属性关系。 例如，在产品模型中，你可以具有来自 Color 和 Product 实体之间的关系的颜色派生层次结构。  
  
 ![](../../2014/master-data-services/media/mds-derivedhierarchy.png)  
  
 在定义了数据的基本结构后，可以开始使用导入功能来添加数据记录（成员）。 将数据加载到临时表、使用业务规则验证数据并将数据加载到 MDS 表。  业务规则还可用于设置属性值。  
  
 下表概述了关键 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 任务。 除非另有说明，否则，所有以下过程都要求您是模型管理员。 有关详细信息，请参阅 [管理员 (Master Data Services)](administrators-master-data-services.md)。  
  
> [!NOTE]  
>  您最好在测试环境中完成以下任务并且使用在按照 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]时提供的示例数据。 有关详细信息，请参阅[部署模型 (Master Data Services)](../../2014/master-data-services/deploying-models-master-data-services.md)。  
  
|操作|详细信息|相关主题|  
|------------|-------------|--------------------|  
|创建模型|在您创建一个模型时，该模型将被视作 VERSION_1。|[模型 (Master Data Services)](../../2014/master-data-services/models-master-data-services.md)<br /><br /> [创建模型 (Master Data Services)](../../2014/master-data-services/create-a-model-master-data-services.md)|  
|创建实体|可以创建所需的任何数目的实体以便包含您的成员。|[实体 (Master Data Services)](../../2014/master-data-services/entities-master-data-services.md)<br /><br /> [创建实体 (Master Data Services)](../../2014/master-data-services/create-an-entity-master-data-services.md)|  
|创建要用作基于域的属性的实体|若要创建基于域的属性，请首先创建实体以便填充属性值列表。|[基于域的属性 (Master Data Services)](../../2014/master-data-services/domain-based-attributes-master-data-services.md)<br /><br /> [创建基于域的属性 (Master Data Services)](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)|  
|为实体创建属性|创建用于描述成员的属性。 Name 和 Code 属性自动包括在每个实体中，并且不能被删除。 您可能要创建其他自由格式的属性以便包含文本、日期、数字或文件。|[属性 (Master Data Services)](../../2014/master-data-services/attributes-master-data-services.md)<br /><br /> [创建文本属性 (Master Data Services)](../../2014/master-data-services/create-a-text-attribute-master-data-services.md)<br /><br /> [创建数字属性 (Master Data Services)](../../2014/master-data-services/create-a-numeric-attribute-master-data-services.md)<br /><br /> [创建日期属性 (Master Data Services)](../../2014/master-data-services/create-a-date-attribute-master-data-services.md)<br /><br /> [创建链接属性 (Master Data Services)](../../2014/master-data-services/create-a-link-attribute-master-data-services.md)<br /><br /> [创建文件属性 (Master Data Services)](../../2014/master-data-services/create-a-file-attribute-master-data-services.md)|  
|创建属性组|如果对于某一实体您具有超过四个或五个属性，则最好创建属性组。 这些组是在 **“资源管理器”** 中网格之上显示的选项卡，并且它们有助于通过在单独的选项卡上将某些属性组合在一起，简化导航行为。 \<插入图像 &GT;|[属性组 (Master Data Services)](../../2014/master-data-services/attribute-groups-master-data-services.md)<br /><br /> [创建属性组 (Master Data Services)](../../2014/master-data-services/create-an-attribute-group-master-data-services.md)|  
|为支持实体导入数据记录（成员）|通过使用临时过程为你的支持实体导入数据。<br /><br /> 对于 Product 模型，这可能意味着导入颜色或大小。<br /><br /> 也可以手动创建成员。<br /><br /> 注意：如果用户至少对实体的叶模型对象具有“更新”权限并且有权访问“资源管理器”功能区域，就可以在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 中创建成员   。|[数据导入&#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)<br /><br /> [加载或使用临时过程更新 Master Data Services 中的成员](../../2014/master-data-services/add-update-and-delete-data-master-data-services.md)<br /><br /> [创建叶成员 (Master Data Services)](../../2014/master-data-services/create-a-leaf-member-master-data-services.md)|  
|创建业务规则以确保数据质量|创建和发布业务规则以便确保您的数据的精确性。 可以使用业务规则执行以下操作：<br /><br /> 设置默认属性值。<br /><br /> 更改属性值。<br /><br /> 在数据未通过业务规则验证时发送电子邮件通知。|[业务规则 (Master Data Services)](../../2014/master-data-services/business-rules-master-data-services.md)<br /><br /> [创建和发布业务规则 (Master Data Services)](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md)<br /><br /> [通知 (Master Data Services)](../../2014/master-data-services/notifications-master-data-services.md)<br /><br /> [配置电子邮件通知 (Master Data Services)](../../2014/master-data-services/configure-email-notifications-master-data-services.md)<br /><br /> [配置业务规则以发送通知 (Master Data Services)](../../2014/master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)|  
|为主实体导入数据记录（成员）。 应用业务规则|通过使用临时过程为你的主实体导入数据。 完成操作后，请验证该版本。 这会将业务规则应用于该模型版本中的所有成员。<br /><br /> 然后，您可以纠正任何业务规则验证问题。|[验证 (Master Data Services)](../../2014/master-data-services/validation-master-data-services.md)<br /><br /> [针对业务规则验证版本 (Master Data Services)](../../2014/master-data-services/validate-a-version-against-business-rules-master-data-services.md)<br /><br /> [验证存储过程 (Master Data Services)](../../2014/master-data-services/validation-stored-procedure-master-data-services.md)|  
|创建派生层次结构|派生的层次结构可以随着你的业务需求的变化进行更新，并且确保所有成员都处于适当的级别。|[派生层次结构 (Master Data Services)](../../2014/master-data-services/derived-hierarchies-master-data-services.md)<br /><br /> [创建派生层次结构 (Master Data Services)](../../2014/master-data-services/create-a-derived-hierarchy-master-data-services.md)|  
|如果需要，创建显式层次结构|如果您想要创建不是基于级别并且包括来自单个实体的成员的层次结构，则可以创建显式层次结构。|[显式层次结构 (Master Data Services)](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)<br /><br /> [创建显式层次结构 (Master Data Services)](../../2014/master-data-services/create-an-explicit-hierarchy-master-data-services.md)|  
|如果想要，创建集合|如果您想要查看不同的成员分组以便进行报告或分析并且不需要完整层次结构，则可以创建集合。<br /><br /> 注意：如果用户至少对集合模型对象具有“更新”权限并且有权访问“资源管理器”功能区域，就可以在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 中创建集合   。|[集合 (Master Data Services)](../../2014/master-data-services/collections-master-data-services.md)<br /><br /> [创建集合 (Master Data Services)](../../2014/master-data-services/create-a-collection-master-data-services.md)|  
|创建用户定义元数据|为了描述您的模型对象，请将用户定义元数据添加到您的模型中。 这些元数据可以包括对象的所有者或者数据源。|[元数据&#40;Master Data Services&#41;](../../2014/master-data-services/metadata-master-data-services.md)<br /><br /> [添加元数据&#40;Master Data Services&#41;](../../2014/master-data-services/add-metadata-master-data-services.md)|  
|锁定模型版本和分配版本标志|锁定模型版本可以防止对成员进行的更改，但管理员除外。 在根据业务规则已成功对版本的数据进行了验证后，您可以提交该版本，这阻止所有用户对成员的更改。<br /><br /> 创建一个版本标志并将其分配给模型。 标志帮助用户和订阅系统确定要使用模型的哪个版本。|[版本 (Master Data Services)](../../2014/master-data-services/versions-master-data-services.md)<br /><br /> [锁定版本 (Master Data Services)](../../2014/master-data-services/lock-a-version-master-data-services.md)<br /><br /> [创建版本标志 (Master Data Services)](../../2014/master-data-services/create-a-version-flag-master-data-services.md)|  
|创建订阅视图|为使您的订阅系统可以使用您的主数据，创建订阅视图，这在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库中创建标准视图。|[将数据导出&#40;Master Data Services&#41;](overview-exporting-data-master-data-services.md)<br /><br /> [创建订阅视图&#40;Master Data Services&#41;](create-a-subscription-view-to-export-data-master-data-services.md)|  
|配置用户和组权限|您不能将测试环境中的用户和组权限复制到生产环境。 但是，可以使用您的测试环境确定最终要在生产中使用的安全性。|[安全性 (Master Data Services)](../../2014/master-data-services/security-master-data-services.md)<br /><br /> [添加组 (Master Data Services)](../../2014/master-data-services/add-a-group-master-data-services.md)<br /><br /> [添加用户 (Master Data Services)](../../2014/master-data-services/add-a-user-master-data-services.md)|  
  
 在就绪后，您可以将模型（具有或不具有有关数据）部署到您的生产环境中。 有关详细信息，请参阅[部署模型 (Master Data Services)](../../2014/master-data-services/deploying-models-master-data-services.md)。  
  
  
