---
title: 列属性 (SSAS 表格) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.columnprop.f1
ms.assetid: 4046c1a3-46c7-47db-b355-52e9c2f23671
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2773c2b837aa9344e2e8427c6f960fa098fa2408
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66067612"
---
# <a name="column-properties-ssas-tabular"></a>列属性（SSAS 表格）
  本主题介绍表格模型列属性。  
  
 本主题的内容：  
  
-   [列属性](#bkmk_properties)  
  
-   [若要配置列属性设置](#bkmk_config_prop)  
  
##  <a name="bkmk_properties"></a> 列属性  
 **基本**  
  
|属性|默认设置|Description|  
|--------------|---------------------|-----------------|  
|**列名**||存储在模型中的列的名称和显示在报告客户端字段列表中的列的名称。|  
|**数据格式**|在导入过程中自动确定。|指定要用于此列中的数据的显示格式。 设置数据格式后，可以设置特定于每种格式的属性。 例如，如果选择 **“货币”** 格式，则可以设置可见小数位数，然后依次选择千位分隔符和货币符号。 此属性具有以下选项：<br /><br /> **常规**<br /><br /> **小数**<br /><br /> **整数**<br /><br /> **货币**<br /><br /> **百分比**<br /><br /> **科学记数**<br /><br /> 如果列值包含图像，请查看 **“代表图像”**。|  
|**数据类型**|在导入过程中自动确定。|指定列中所有值的数据类型。|  
|**说明**||列的文本说明。<br /><br /> 在某些报表客户端中，如果最终用户将游标置于字段列表的此列上方，则说明将以工具提示的形式出现。|  
|**Hidden**|False|指定是否在报告客户端字段列表中隐藏列。<br /><br /> 将此属性设置为 **“True”** 可在显示中隐藏该列。 例如，包含标识符或键的列通常对最终用户没有任何用处。<br /><br /> 如果在报告客户端上隐藏列，则该字段会显示在模型数据中。 如果您创建针对模型的查询，则该字段仍将可见。 隐藏的列仍可用于分组或排序。<br /><br /> **“隐藏”** 属性不提供任何形式的数据安全性。 若要确保数据安全，请在角色中使用行筛选器。 有关详细信息，请参阅 [角色（SSAS 表格）](roles-ssas-tabular.md)中创建的表格模型项目。|  
|**按列排序**||指定另一个列以对此列中的值进行排序。 两个列之间必须存在关系。<br /><br /> 该值必须为现有列的名称。 不能指定公式或度量值。|  
  
 **报表属性**  
  
 有关设置 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 表行为属性的详细信息，请参阅 [为 Power View 报表配置表行为属性（SSAS 表格）](power-view-configure-table-behavior-properties-for-reports.md)。  
  
|属性|默认设置|Description|  
|--------------|---------------------|-----------------|  
|默认图像|False|指定哪一行提供用于表示行数据的图像（例如，员工记录中的照片 ID）。|  
|默认标签|False|指定哪一列提供显示名称来表示行数据（例如，员工记录中的员工姓名）。|  
|图像 URL/数据类别 (SP1)|False|指定此列中的值作为指向服务器上图像的超链接。 例如： http://localhost/images/image1.jpg。|  
|保留唯一行|False|指定哪些列提供应视为唯一的值，即使这些值重复也不例外（例如，员工的姓氏和名字，而两个或更多员工同名）。|  
|行标识符|False|指定只包含唯一值的一列，同时允许将该列用作内部分组键。|  
|汇总方式|默认|指定在将此列添加到字段列表时，报表客户端工具将对列计算应用聚合函数 SUM。 若要更改默认计算，请从下拉列表中选择它。 此属性仅应用于属于可聚合类型的列。|  
|表详细信息位置|没有默认字段集|指定将此列或度量值添加到单个表中的一组字段中，以便在报表客户端中增强表的可视化体验。|  
  
###  <a name="bkmk_config_prop"></a> 若要配置列属性设置  
  
1.  在模型设计器的表中，选择一个列。  
  
2.  在 **“属性”** 窗口中，单击某个属性，然后键入值或单击向下箭头选择设置选项。  
  
## <a name="see-also"></a>请参阅  
 [Power View 报表属性（SSAS 表格）](properties-ssas-tabular.md)   
 [隐藏或冻结列（SSAS 表格）](hide-or-freeze-columns-ssas-tabular.md)   
 [将列添加到表（SSAS 表格）](add-columns-to-a-table-ssas-tabular.md)  
  
  
