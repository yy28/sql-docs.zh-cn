---
title: "对表 (SSAS 表格) 中的数据进行排序 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5fa6ad56-bf68-4aac-a226-52556173b7e2
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6cfced262d6b178712da538e9b678ac46357bc1a
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="sort-data-in-a-table-ssas-tabular"></a>对表中的数据进行排序（SSAS 表格）
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]您可以通过文本 (A 到 Z 或 Z 到 A) 和一个或多个列中 （最小到最大或最大到最小） 的数字的数据进行排序。  
  
### <a name="to-sort-the-data-in-a-table-based-on-a-text-column"></a>基于文本列对表数据进行排序  
  
1.  在模型设计器中，选择某一字母数字数据列或者列中的某一范围的单元，或者确保活动单元处于包含字母数字数据的表列中，然后单击要作为筛选依据的列标题中的箭头。  
  
2.  在“自动筛选”菜单中，执行以下操作之一：  
  
    -   若要按字母数字的升序排序，请单击 **“从 A 到 Z 排序”**。  
  
    -   若要按字母数字的降序排序，请单击 **“从 Z 到 A 排序”**。  
  
    > [!NOTE]  
    >  在某些情况下，从其他应用程序导入的数据之前可能插入了前导空格。 您必须删除这些前导空格才能正确对数据进行排序。  
  
### <a name="to-sort-the-data-in-a-table-based-on-a-numeric-column"></a>基于数字列对表数据进行排序  
  
1.  在模型设计器中，选择某一字母数字数据列或者列中的某一范围的单元，或者确保活动单元处于包含字母数字数据的表列中，然后单击要作为筛选依据的列标题中的箭头。  
  
2.  在“自动筛选”菜单中，执行以下操作之一：  
  
    -   若要从小到大对数字进行排序，请单击 **“从小到大排序”**。  
  
    -   若要从大到小对数字进行排序，请单击 **“从大到小排序”**。  
  
    > [!NOTE]  
    >  如果得到的并不是期望的结果，列中可能包含存储为文本而不是数字的数字。 例如，从某些会计系统导入的负数或是以 '（撇号）开头的数字均存储为文本。  
  
## <a name="see-also"></a>另请参阅  
 [对数据进行筛选和排序（SSAS 表格）](http://msdn.microsoft.com/library/55ebd7a6-2458-4398-911f-fcfeb2413f1b)   
 [透视表（SSAS 表格）](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [角色（SSAS 表格）](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  
