---
title: "隐藏或冻结列 (SSAS 表格) |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.bidtoolset.hideunhidecolumnsdb.f1
ms.assetid: 5407aee5-6a07-4559-a2ba-2ca00a242f02
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8334a3e6087740a2060425e764e9de6afa365e19
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="hide-or-freeze-columns-ssas-tabular"></a>隐藏或冻结列（SSAS 表格）
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]在模型设计器中，如果没有不想要显示在一个表的列可以暂时隐藏它们。 隐藏列可为您在屏幕上提供更多空间，以便添加新列或仅使用相关的数据列。 从模型设计器的“列”菜单或者每个列标题的右键单击菜单中，可以隐藏和取消隐藏列。 要在滚动到模型的其他区域时使模型的某一区域可见，可以通过冻结该区域的特定列来锁定它们。  
  
> [!IMPORTANT]  
>  隐藏列的功能不是为了用于数据安全性，而是为了简化和缩短模型设计器或报表中可见列的列表。 要保护数据，您可以定义安全角色。 角色可以将可查看的元数据和数据限制为在角色中定义的那些对象。 有关详细信息，请参阅 [角色（SSAS 表格）](../../analysis-services/tabular-models/roles-ssas-tabular.md)中创建的表格模型项目。  
  
 在隐藏某一列时，你可以选择在模型设计器或报表中工作时隐藏该列。 如果隐藏所有列，则整个表在模型设计器中显示为空白。  
  
> [!NOTE]  
>  如果您要隐藏的列很多，可以创建一个透视来替代隐藏列和取消隐藏列。 透视是自定义的数据视图，它更便于使用相关数据的子集。 有关详细信息，请参阅[创建和管理透视表（SSAS 表格）](../../analysis-services/tabular-models/create-and-manage-perspectives-ssas-tabular.md)。  
  
### <a name="to-hide-an-individual-column"></a>隐藏单个列  
  
1.  在模型设计器中，选择包含要隐藏的列的表。  
  
2.  右键单击该列，单击“隐藏列”，然后单击“从设计器和报表”、“从报表”或“从设计器”。  
  
### <a name="to-hide-multiple-columns"></a>隐藏多个列  
  
1.  在模型设计器中，选择包含要隐藏的列的表。  
  
2.  单击 **“列”** 菜单，然后单击 **“隐藏和取消隐藏”**。  
  
3.  在 **“隐藏和取消隐藏列”** 对话框中，找到要隐藏的每个列，然后取消选中 **“在设计器中”** 和/或 **“在报表中”**。  
  
4.  单击“确定” 。  
  
### <a name="to-freeze-columns"></a>冻结列  
  
1.  在模型设计器中，选择包含要冻结的列的表。  
  
2.  选择一个或多个要冻结的列。  
  
3.  单击 **“列”** 菜单，然后单击 **“冻结”**。  
  
    > [!NOTE]  
    >  冻结列时，将它移到设计器中表的左侧（或前面）。 解冻该列并不将它移回原始位置。  
  
## <a name="see-also"></a>另请参阅  
 [表和列（SSAS 表格）](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)   
 [透视表（SSAS 表格）](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [角色（SSAS 表格）](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  
