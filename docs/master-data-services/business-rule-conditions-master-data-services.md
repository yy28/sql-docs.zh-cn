---
title: 业务规则条件 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d2e0a8c3-4c2e-407c-856e-68d95ebda9ed
caps.latest.revision: 10
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: bc7113fefba29b709ab9c0488ca6643ff6c85c28
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35333851"
---
# <a name="business-rule-conditions-master-data-services"></a>业务规则条件 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，业务规则条件确定对于要执行的一个或多个操作必须满足的条件。  
  
> [!NOTE]  
>  条件是可选的。 如果您未指定条件，则每当针对业务规则验证数据时都要执行操作。  
  
## <a name="business-rule-conditions"></a>业务规则条件  
  
|条件名称|描述|  
|--------------------|-----------------|  
|**等于**|所选属性 **“等于”** 特定属性、特定属性值或者为空。<br /><br /> 此条件对文本、数字、日期和链接值有效。|  
|**不等于**|所选属性 **“不等于”** 特定属性、特定属性值或者为空。<br /><br /> 此条件对文本、数字、日期和链接值有效。|  
|**大于**|所选属性 **“大于”** 特定属性、特定属性值或者为空。<br /><br /> 此条件对文本、数字和日期值有效。|  
|**大于或等于**|所选属性 **“大于或等于”** 特定属性、特定属性值或者为空。<br /><br /> 此条件对文本、数字和日期值有效。|  
|**小于**|所选属性 **“小于”** 特定属性、特定属性值或者为空。<br /><br /> 此条件对文本、数字和日期值有效。|  
|**小于或等于**|所选属性 **“小于或等于”** 特定属性、特定属性值或者为空。<br /><br /> 此条件对文本、数字和日期值有效。|  
|**开头为**|所选属性 **“开头为”** 特定属性、特定属性值或者为空。<br /><br /> 此条件对文本和链接值有效。|  
|**开头不为**|所选属性 **开头不为** 特定属性、特定属性值或者为空。<br /><br /> 此条件对文本和链接值有效。|  
|**结尾为**|所选属性 **“结尾为”** 特定属性、特定属性值或者为空。<br /><br /> 此条件对文本和链接值有效。|  
|**结尾不为**|所选属性 **结尾不为** 特定属性、特定属性值或者为空。<br /><br /> 此条件对文本和链接值有效。|  
|**包含**|所选属性 **“包含”** 特定属性、特定属性值或者为空。<br /><br /> 此条件对文本和链接值有效。|  
|**不包含**|所选属性 **不包含** 特定属性、特定属性值或者为空。<br /><br /> 此条件对文本和链接值有效。|  
|**包含模式**|所选属性 **“包含模式”** 来自特定属性、特定属性值或者为空。 使用 .NET Framework 正则表达式可以指定模式。<br /><br /> 有关正则表达式的详细信息，请参阅 MSDN Library 中的 [Regular Expression Language Elements](http://go.microsoft.com/fwlink/?LinkId=164401) （正则表达式语言元素）。<br /><br /> 此条件对文本和链接值有效。|  
|**不包含模式**|所选属性 **不包含模式** 来自特定属性、特定属性值或者为空。 使用 .NET Framework 正则表达式可以指定模式。<br /><br /> 有关正则表达式的详细信息，请参阅 MSDN Library 中的 [Regular Expression Language Elements](http://go.microsoft.com/fwlink/?LinkId=164401) （正则表达式语言元素）。<br /><br /> 此条件对文本和链接值有效。|  
|**包含子集**|所选属性 **“包含的子集”** 来自特定属性或特定属性值。 您必须指定搜索的起始位置（例如，1 表示从第一个字符开始搜索）。<br /><br /> 此条件对文本和链接值有效。|  
|**不包含子集**|所选属性 **不包含子集** 来自特定属性或特定属性值。 您必须指定搜索的起始位置（例如，1 表示从第一个字符开始搜索）。<br /><br /> 此条件对文本和链接值有效。|  
|**已更改**|自上次将业务规则应用于成员以来，所选属性 **“已更改”** 。 必须指定属性作为其成员的更改组。<br /><br /> 有关更改跟踪组的详细信息，请参阅[向更改跟踪组添加属性 (Master Data Services)](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)。<br /><br /> 此条件对文本、数字、日期和链接值有效。|  
|**未更改**|所选属性 **未更改** 。 必须指定属性作为其成员的更改组。<br /><br /> 有关更改跟踪组的详细信息，请参阅[向更改跟踪组添加属性 (Master Data Services)](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)。<br /><br /> 此条件对文本、数字、日期和链接值有效。|  
|**介于**|所选属性 **“介于”** 两个特定属性值之间。<br /><br /> 此条件对文本、数字和日期值有效。|  
|**不介于**|所选属性 **不介于** 两个特定属性值之间。<br /><br /> 此条件对文本、数字和日期值有效。|  
  
> [!NOTE]  
>  当业务规则包含比较两个值的条件且该规则应用到两个值均为 NULL 的成员时，该成员将会验证失败。  
  
## <a name="see-also"></a>另请参阅  
 [业务规则操作 (Master Data Services)](../master-data-services/business-rule-actions-master-data-services.md)   
 [业务规则 (Master Data Services)](../master-data-services/business-rules-master-data-services.md)   
 [创建和发布业务规则 (Master Data Services)](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)  
  
  
