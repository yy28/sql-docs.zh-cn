---
title: 创建显式层次结构 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- creating explicit hierarchies [Master Data Services]
- explicit hierarchies, creating
ms.assetid: ba768393-6990-4eda-8cb0-d58cb3cfc2e2
caps.latest.revision: 10
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b35af751769b07aba9a30c7a32cb2a452c44965c
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="create-an-explicit-hierarchy-master-data-services"></a>创建显式层次结构 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，在您需要其成员可在任何级别存在的不规则层次结构时，创建显式层次结构。 显式层次结构包含来自单个实体的成员。  
  
 创建显式层次结构后，可以在 **“资源管理器”** 功能区域中为该层次结构添加成员。  
  
## <a name="prerequisites"></a>必备条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅 [管理员 (Master Data Services)](../master-data-services/administrators-master-data-services.md)。  
  
-   必须为显式层次结构和集合启用了实体。  
  
### <a name="to-create-an-explicit-hierarchy"></a>创建显式层次结构  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  在“管理模型”  页上，从网格中选择一个模型，然后单击“实体” 。  
  
3.  在“管理实体”  页上，从网格中选择要为其创建显式层次结构的实体所在的行。  
  
4.  单击“显式层次结构” 。  
  
5.  在“管理显式层次结构”  页上，单击“添加” 。  
  
6.  在“名称”  框中，键入层次结构的名称。  
  
7.  也可以取消选中“强制的层次结构”复选框，以便将层次结构创建为非强制的层次结构。 有关层次结构类型的详细信息，请参阅[显式层次结构 (Master Data Services)](../master-data-services/explicit-hierarchies-master-data-services.md)。  
  
8.  单击 **“保存”**。  
  
## <a name="grid-columns"></a>网格列  
 对于你创建的每个显式层次结构，系统都会在网格中添加一行（其中包含七列）。 下面介绍了这些列。  
  
|“属性”|Description|  
|----------|-----------------|  
|“登录属性”|实体状态。 单击“保存”  时，将显示下图，指示实体正在更新。<br /><br /> ![更新状态图标](../master-data-services/media/mds-statusicon-updating.png "Icon for updating status")<br /><br /> 如果在创建或编辑实体时出错，将显示下面的图像。<br /><br /> ![错误状态图标](../master-data-services/media/mds-statusicon-error.png "Icon for error status")<br /><br /> 如果状态为“正常”，则将显示下面的图像。<br /><br /> ![正常状态图标](../master-data-services/media/mds-statusicon-ok.png "Icon for OK status")|  
|“属性”|显式层次结构名称。|  
|必需|指定显式层次结构是否必需。|  
|创建者|创建显式层次结构的用户的用户名。|  
|创建时间|创建显式层次结构的日期和时间。|  
|更新者|上次更新显式层次结构的用户的用户名。|  
|更新时间|上次更新显式层次结构的日期和时间。|  
  
## <a name="next-steps"></a>Next Steps  
  
-   [创建合并成员 (Master Data Services)](../master-data-services/create-a-consolidated-member-master-data-services.md)  
  
  
  
## <a name="see-also"></a>另请参阅  
 [显式层次结构 (Master Data Services)](../master-data-services/explicit-hierarchies-master-data-services.md)   
 [具有显式顶端的派生层次结构 &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-with-explicit-caps-master-data-services.md)   
 [更改显式层次结构名称 (Master Data Services)](../master-data-services/change-an-explicit-hierarchy-name-master-data-services.md)  
  
  

