---
title: 创建计算列（SSAS 表格） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.as.daxref.CreataCalculatedColumn.f1
ms.assetid: 59440510-2d76-41dc-9b55-edc15259f9da
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 60218cb5f50777ac07e9a2805d224d80bef7975d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66066522"
---
# <a name="create-a-calculated-column-ssas-tabular"></a>创建计算列（SSAS 表格）
  通过计算列，可以将新数据添加到您的模型。 您可以创建定义列的行级值的 DAX 公式，而不是在列中粘贴或导入值。 计算列中每行的值在您创建有效公式并单击 Enter 后会进行计算和填充。 然后可以将计算列添加到报告或分析应用程序中，就像添加任何其他数据列一样。 本主题说明如何使用模型设计器中的 DAX 编辑栏创建新的计算列。  
  
#### <a name="to-create-a-new-calculated-column"></a>创建新的计算列  
  
1.  在模型设计器的“数据视图”中，选择要添加计算列的表，单击 **“列”** 菜单，然后单击 **“添加列”**。  
  
     **“添加列”** 将在最右侧的空列之上突出显示，并且光标将移到公式栏。  
  
     若要在两个现有列之间创建新列，请右键单击某个现有列，然后单击****“插入列”。  
  
2.  在编辑栏中，执行以下操作之一：  
  
    -   键入等号，后跟公式。  
  
    -   键入等号，后跟 DAX 函数和该函数所需的参数。  
  
    -   单击函数按钮 (**fx**)，在“插入函数”对话框中选择一个类别和函数，然后单击“确定”********。 在编辑栏中键入该函数所需的其他参数。  
  
3.  按 Enter 以接受该公式。  
  
     整个列将用该公式填充，将为每一行计算值。  
  
> [!TIP]  
>  可以在具有嵌套函数的现有公式中使用 DAX 公式记忆式键入功能。 刚好在插入点之前的文本将用于显示下拉列表中的值，并且插入点之后的所有文本都保持不变。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;SSAS 表格&#41;计算列](ssas-calculated-columns.md)   
 [度量值（SSAS 表格）](measures-ssas-tabular.md)  
  
  
