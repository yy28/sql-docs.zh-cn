---
title: 定义半累加行为 （商业智能向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.semiadditivememberdetection.f1
ms.assetid: e57080ba-ce96-40f8-bca7-6701d1725b3c
caps.latest.revision: 24
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 201a5a24e8bafa2f2f919f6ad0b072ca801a694e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37310807"
---
# <a name="define-semiadditive-behavior-business-intelligence-wizard"></a>定义半累加行为（商业智能向导）
  可以使用“定义半累加性行为”页启用或禁用针对度量值的半累加行为。 半累加行为确定多维数据集所包含的度量值在一定时间维度内如何聚合。  
  
> [!NOTE]  
>  除了可用于标准版本的 LastChild 之外，其他的半累加行为仅可用于商业智能或企业版本。 此外，由于半累加性行为是只针对度量值而不针对维度定义的，如果从维度设计器或者通过在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]的解决方案资源管理器中右键单击维度启动了商业智能向导，将不会看到此页。  
  
## <a name="options"></a>“常规”  
 **关闭半累加性行为**  
 在多维数据集所包含的所有度量值中禁用半累加性行为。  
  
 **向导检测到\<维度名称 > 包含半累加性成员的帐户维度。服务器将聚合此维度根据为每个帐户类型指定的半累加性行为的成员。**  
 对包含半累加性成员的帐户维度启用半累加性行为。 选择此选项设置的所有度量值的聚合函数引用为该帐户维度的度量值组中`ByAccount`。  
  
 有关帐户维度的详细信息，请参阅 [创建父子类型维度的财务帐户](multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md)。  
  
 **为各个成员定义半累加性行为**  
 为特定度量值启用半累加性行为，并指定半累加性聚合函数。 该聚合函数将应用于包含该度量值的度量值组所引用的所有维度。  
  
 **度量值**  
 显示多维数据集所包含的度量值的名称。  
  
 **半累加性函数**  
 为所选度量值选择聚合函数。 下表列出了可用的聚合函数：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**AverageOfChildren**|通过返回度量值子成员的平均值进行聚合。|  
|`ByAccount`|通过与帐户维度中属性的指定帐户类型关联的聚合函数进行聚合。|  
|`Count`|使用 `Count` 函数聚合。|  
|`DistinctCount`|使用 `DistinctCount` 函数聚合。|  
|**FirstChild**|通过返回度量值在一定时间维度内的第一个子成员聚合。|  
|**FirstNonEmpty**|通过返回度量值在一定时间维度内的第一个非空成员聚合。|  
|**LastChild**|通过返回度量值在一定时间维度内的最后一个子成员聚合。|  
|**LastNonEmpty**|通过返回度量值在一定时间维度内的最后一个非空成员聚合。|  
|`Max`|使用 `Max` 函数聚合。|  
|`Min`|使用 `Min` 函数聚合。|  
|**无**|不执行聚合。|  
|`Sum`|使用 `Sum` 函数聚合。|  
  
> [!NOTE]  
>  只有在选择了“为各个成员定义半累加性行为”之后，才会应用对此选项所做的选择。  
  
## <a name="see-also"></a>请参阅  
 [商业智能向导的 F1 帮助](business-intelligence-wizard-f1-help.md)   
 [多维数据集设计器&#40;Analysis Services-多维数据&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [维度设计器&#40;Analysis Services-多维数据&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
