---
title: 指定维度类型 （维度向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.bidimensionproperties.f1
ms.assetid: 3215282a-532d-4ff2-b721-286f088967fc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6de1b056942673d358cec4768c6854a6966d139e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66068366"
---
# <a name="specify-dimension-type-dimension-wizard"></a>指定维度类型（维度向导）
  可以定使用 **“指定维度类型”** 页义维度类型，以及将与所选维度类型关联的特殊属性类型添加到维度中。  
  
> [!NOTE]  
>  只有在“选择维度类型”  页上选择了“标准维度”  时，才会显示此页。  
  
## <a name="options"></a>选项  
 **维度类型**  
 选择维度的维度类型。 下表列出了可用的维度类型：  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**帐户**|帐户维度包含了表示帐户列表的数据和元数据。<br /><br /> 有关帐户维度的详细信息，请参阅 [创建父子类型维度的财务帐户](multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md)。|  
|**BillOfMaterials**|物料清单（或 BOM）维度为常规维度，其中的数据和元数据表示库存信息或生产信息，例如产品的零件列表。<br /><br /> 有关常规维度的详细信息，请参阅 [维度类型](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)。|  
|**Channel**|渠道维度为常规维度，其中的数据和元数据表示渠道信息。<br /><br /> 有关常规维度的详细信息，请参阅 [维度类型](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)。|  
|**货币**|货币维度包含表示货币信息的数据和元数据。<br /><br /> 有关货币维度的详细信息，请参阅 [创建货币类型维度](multidimensional-models/database-dimensions-create-a-currency-type-dimension.md)。|  
|**Customers**|客户维度为常规维度，其中的数据和元数据表示客户信息或联系信息。<br /><br /> 有关常规维度的详细信息，请参阅 [维度类型](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)。|  
|**地域**|地域维度为常规维度，其中的数据和元数据表示地域信息，例如城市或邮政编码。<br /><br /> 有关常规维度的详细信息，请参阅 [维度类型](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)。|  
|**组织**|单位维度为常规维度，其中的数据和元数据表示单位信息，例如雇员或分公司。<br /><br /> 有关常规维度的详细信息，请参阅 [维度类型](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)。|  
|**产品**|产品维度为常规维度，其中的数据和元数据表示产品信息。<br /><br /> 有关常规维度的详细信息，请参阅 [维度类型](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)。|  
|**Promotion**|促销维度为常规维度，其中的数据和元数据表示市场营销的促销信息。<br /><br /> 有关常规维度的详细信息，请参阅 [维度类型](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)。|  
|**Quantitative**|定量维度为常规维度，其中的数据和元数据表示定量信息。<br /><br /> 有关常规维度的详细信息，请参阅 [维度类型](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)。|  
|**费率**|比率维度包含表示汇率信息和货币换算信息的数据和元数据。|  
|**Regular**|常规维度是 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]中最常用的维度类型。<br /><br /> 有关常规维度的详细信息，请参阅 [维度类型](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)。|  
|**应用场景**|应用场景维度为常规维度，其中的数据和元数据表示计划信息或策略分析信息。<br /><br /> 有关常规维度的详细信息，请参阅 [维度类型](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)。|  
|**Time**|时间维度包含面向时间的数据和元数据。<br /><br /> 有关时间维度的详细信息，请参阅 [创建日期类型维度](multidimensional-models/database-dimensions-create-a-date-type-dimension.md)。|  
|**实用工具**|效用维度为常规维度，其中的数据和元数据表示不易于与其他维度类型匹配的信息。<br /><br /> 有关常规维度的详细信息，请参阅 [维度类型](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)。|  
  
## <a name="dimension-attributes-options"></a>维度属性选项  
  
> [!NOTE]  
>  只有在所选的 **“维度类型”** 具有与其相关联的特殊属性类型时，此部分中的选项才可用。 并非所有的维度类型都具有与其相关联的特殊属性类型。  
  
 **包括**  
 选中此选项将包括维度中的属性类型。  
  
 **属性类型**  
 显示与“维度类型”  中所选维度类型相关联的属性类型。 有关属性类型的详细信息，请参阅[类型元素（维度属性）(ASSL)](https://docs.microsoft.com/bi-reference/assl/properties/type-element-dimensionattribute-assl)。  
  
 **维度属性**  
 选择特定维度属性，维度向导将为其分配“属性类型”  中显示的特殊属性类型。  
  
## <a name="see-also"></a>请参阅  
 [维度向导的 F1 帮助](dimension-wizard-f1-help.md)   
 [维度&#40;Analysis Services-多维数据&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [多维模型中的维度](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
