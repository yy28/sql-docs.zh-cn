---
title: "重命名表或列 |Microsoft 文档"
ms.custom: 
ms.date: 05/22/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.bidtoolset.renametableorcolumn.f1
ms.assetid: 88061a39-c5aa-403d-a52b-7fdb365fc235
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bf8d925f0ffe72eab343ebf8af82030a21c0a9b0
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2018
---
# <a name="rename-a-table-or-column"></a>重命名表或列 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
在导入过程中，您可以通过在 **“表导入向导”** 的 **“选择表和视图”** 页中键入 **“友好名称”**，更改表的名称。 如果您通过在 **“表导入向导”** 的 **“指定 SQL 查询”**页上指定查询来导入数据，也可以更改表和列名。  
  
 在您将数据添加到模型中后，表的名称（或标题）将出现在模型设计器底部的表选项卡上。 您可以更改表的名称，以便为其提供更为合适的名称。 您还可以在数据添加到模型中之后重命名列。 在您从多个源导入了数据，并且想要确保不同表中的列具有易于区分的名称时，此选项特别重要。  
  
### <a name="to-rename-a-table"></a>重命名表  
  
1.  在模型设计器中，右键单击包含要重命名的表的选项卡，然后单击 **“重命名”**。  
  
2.  键入新名称。  
  
    > [!NOTE]  
    >  您可以通过使用 **“编辑表属性”** 对话框，编辑表的其他属性，包括连接信息和列映射。 但无法在该对话框中更改名称。  
  
### <a name="to-rename-a-column"></a>重命名列  
  
1.  在模型设计器中，双击要重命名的列的标题，或者右键单击该标题，然后从上下文菜单中选择 **“重命名列”** 。  
  
2.  键入新名称。  
  
## <a name="naming-requirements-for-columns-and-tables"></a>列和表的命名要求  
 下面的单词和字符不能用于表或列的名称中：  
  
-   前导空格或尾随空格  
  
-   控制字符  
  
-   以下字符（字符在 Analysis Services 对象的名称中无效）：.,;':/\\*|?&%$!+=()[]{}<>  
  
-   Analysis Services 保留关键字，包括多维表达式 (MDX) 和数据挖掘扩展插件 (DMX) 函数名称和运算符。  
  
## <a name="effect-of-renaming-on-existing-tables-columns-and-calculations"></a>重命名对现有表、列和计算的影响  
 只要您更改某一表的名称，就会更改可能包含多个列或度量值的基础表对象的名称。 若要在其定义中使用新名称，必须更新任何列都在表中和使用表中，任何关系。 在大多数情况下，此更新自动发生。
  
 此外必须更新使用重命名的表，或使用列重命名的表中，从任何计算，并从这些计算派生的数据必须刷新和重新计算。 根据受到影响的表和计算的数目，上述刷新和重新计算可能需要一些时间才能完成。 因此，重命名表的最佳时机是在导入过程中，或者是在开始生成复杂的关系和计算之前。  
  
## <a name="see-also"></a>另请参阅  
 [表和列](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)   
 [从 Power Pivot 导入](../../analysis-services/tabular-models/import-from-power-pivot-ssas-tabular.md)   
 [从 Analysis Services 导入](../../analysis-services/tabular-models/import-from-analysis-services-ssas-tabular.md)  
  
  
