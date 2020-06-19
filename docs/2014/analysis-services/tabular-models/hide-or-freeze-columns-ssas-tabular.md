---
title: 隐藏或冻结列（SSAS 表格） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.hideunhidecolumnsdb.f1
ms.assetid: 5407aee5-6a07-4559-a2ba-2ca00a242f02
author: minewiskan
ms.author: owend
ms.openlocfilehash: 4a6e447b827b54eb126a867746e12b0ddfc10fec
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938888"
---
# <a name="hide-or-freeze-columns-ssas-tabular"></a>隐藏或冻结列（SSAS 表格）
  在模型设计器中，如果不想在表中显示某些列，则可以暂时隐藏它们。 隐藏列可为您在屏幕上提供更多空间，以便添加新列或仅使用相关的数据列。 从模型设计器的“列”**** 菜单或者每个列标题的右键单击菜单中，可以隐藏和取消隐藏列。 要在滚动到模型的其他区域时使模型的某一区域可见，可以通过冻结该区域的特定列来锁定它们。  
  
> [!IMPORTANT]  
>  隐藏列的功能不是为了用于数据安全性，而是为了简化和缩短模型设计器或报表中可见列的列表。 要保护数据，您可以定义安全角色。 角色可以将可查看的元数据和数据限制为在角色中定义的那些对象。 有关详细信息，请参阅 [角色（SSAS 表格）](roles-ssas-tabular.md)中创建的表格模型项目。  
  
 在隐藏某一列时，你可以选择在模型设计器或报表中工作时隐藏该列。 如果隐藏所有列，则整个表在模型设计器中显示为空白。  
  
> [!NOTE]  
>  如果您要隐藏的列很多，可以创建一个透视来替代隐藏列和取消隐藏列。 透视是自定义的数据视图，它更便于使用相关数据的子集。 有关详细信息，请参阅[创建和管理透视表（SSAS 表格）](perspectives-ssas-tabular.md)。  
  
### <a name="to-hide-an-individual-column"></a>隐藏单个列  
  
1.  在模型设计器中，选择包含要隐藏的列的表。  
  
2.  右键单击该列，单击“隐藏列”，然后单击“从设计器和报表”、“从报表”或“从设计器”。****************  
  
### <a name="to-hide-multiple-columns"></a>隐藏多个列  
  
1.  在模型设计器中，选择包含要隐藏的列的表。  
  
2.  单击 **“列”** 菜单，然后单击 **“隐藏和取消隐藏”**。  
  
3.  在 **“隐藏和取消隐藏列”** 对话框中，找到要隐藏的每个列，然后取消选中 **“在设计器中”** 和/或 **“在报表中”**。  
  
4.  单击“确定”。  
  
### <a name="to-freeze-columns"></a>冻结列  
  
1.  在模型设计器中，选择包含要冻结的列的表。  
  
2.  选择一个或多个要冻结的列。  
  
3.  单击 **“列”** 菜单，然后单击 **“冻结”**。  
  
    > [!NOTE]  
    >  冻结列时，将它移到设计器中表的左侧（或前面）。 解冻该列并不将它移回原始位置。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;SSAS 表格&#41;的表和列](tables-and-columns-ssas-tabular.md)   
 [SSAS 表格&#41;&#40;透视](perspectives-ssas-tabular.md)   
 [角色（SSAS 表格）](roles-ssas-tabular.md)  
  
  
