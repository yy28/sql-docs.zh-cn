---
title: 业务规则条件
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: d2e0a8c3-4c2e-407c-856e-68d95ebda9ed
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ab2b632307f966a0f8e37d290c3cc12d52cda064
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "73728718"
---
# <a name="business-rule-conditions-master-data-services"></a>业务规则条件 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，业务规则条件确定对于要执行的一个或多个操作必须满足的条件。  
  
> [!NOTE]  
>  条件是可选的。 如果您未指定条件，则每当针对业务规则验证数据时都要执行操作。  
  
## <a name="business-rule-conditions"></a>业务规则条件  
  
|条件名称|说明|  
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
|**有**|所选属性 **“包含”** 特定属性、特定属性值或者为空。<br /><br /> 此条件对文本和链接值有效。|  
|**不包含**|所选属性 **不包含** 特定属性、特定属性值或者为空。<br /><br /> 此条件对文本和链接值有效。|  
|**包含模式**|所选属性 **“包含模式”** 来自特定属性、特定属性值或者为空。 使用 .NET Framework 正则表达式可以指定模式。<br /><br /> 有关正则表达式的详细信息，请参阅 MSDN Library 中的 [Regular Expression Language Elements](https://go.microsoft.com/fwlink/?LinkId=164401) （正则表达式语言元素）。<br /><br /> 此条件对文本和链接值有效。|  
|**不包含模式**|所选属性 **不包含模式** 来自特定属性、特定属性值或者为空。 使用 .NET Framework 正则表达式可以指定模式。<br /><br /> 有关正则表达式的详细信息，请参阅 MSDN Library 中的 [Regular Expression Language Elements](https://go.microsoft.com/fwlink/?LinkId=164401) （正则表达式语言元素）。<br /><br /> 此条件对文本和链接值有效。|  
|**包含子集**|所选属性 **“包含的子集”** 来自特定属性或特定属性值。 您必须指定搜索的起始位置（例如，1 表示从第一个字符开始搜索）。<br /><br /> 此条件对文本和链接值有效。|  
|**不包含子集**|所选属性 **不包含子集** 来自特定属性或特定属性值。 您必须指定搜索的起始位置（例如，1 表示从第一个字符开始搜索）。<br /><br /> 此条件对文本和链接值有效。|  
|**已更改**|自上次将业务规则应用于成员以来，所选属性 **“已更改”** 。 必须指定属性作为其成员的更改组。<br /><br /> 有关更改跟踪组的详细信息，请参阅[向更改跟踪组添加属性 (Master Data Services)](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)。<br /><br /> 此条件对文本、数字、日期和链接值有效。|  
|**未更改**|所选属性 **未更改** 。 必须指定属性作为其成员的更改组。<br /><br /> 有关更改跟踪组的详细信息，请参阅[向更改跟踪组添加属性 (Master Data Services)](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)。<br /><br /> 此条件对文本、数字、日期和链接值有效。|  
|**介于**|所选属性 **“介于”** 两个特定属性值之间。<br /><br /> 此条件对文本、数字和日期值有效。|  
|**不介于**|所选属性 **不介于** 两个特定属性值之间。<br /><br /> 此条件对文本、数字和日期值有效。|  
  
> [!NOTE]  
>  当业务规则包含比较两个值的条件且该规则应用到两个值均为 NULL 的成员时，该成员将会验证失败。  
  
## <a name="see-also"></a>另请参阅  
 [业务规则操作 &#40;Master Data Services&#41;](../master-data-services/business-rule-actions-master-data-services.md)   
 [业务规则 &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)   
 [创建和发布业务规则 &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)  
  
  
