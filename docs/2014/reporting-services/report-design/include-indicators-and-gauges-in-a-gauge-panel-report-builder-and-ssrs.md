---
title: 在仪表面板中包括指示器和仪表（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4dff9b67-b483-4c51-a822-6dbe706a6840
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 20428f17cf035cf7bae6f098c8a3514e7419ccd0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027161"
---
# <a name="include-indicators-and-gauges-in-a-gauge-panel-report-builder-and-ssrs"></a>在仪表面板中包括指示器和仪表（报表生成器和 SSRS）
  仪表面板是包含一个或多个仪表和指示器的顶级容器。 指示器可以嵌入在仪表中或在仪表面板放置于仪表旁。  
  
 如果指示器和仪表在仪表面板中相邻并且显示来自不同字段的数据，则您最好添加标签，以便清楚地表明仪表和指示器提供的数据。  
  
 可以使用表达式设置仪表和指示器选项。 有关详细信息，请参阅[表达式（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-embed-an-indicator-in-a-gauge"></a>将指示器嵌入在仪表中  
  
1.  打开一个现有报表，或者创建一个新报表（其中包含具有要显示的数据的表或矩阵）。 有关详细信息，请参阅[表（报表生成器和 SSRS）](tables-report-builder-and-ssrs.md)或[矩阵（报表生成器和 SSRS）](create-a-matrix-report-builder-and-ssrs.md)。  
  
2.  在您的表或矩阵中插入列。 有关详细信息，请参阅[插入或删除列（报表生成器和 SSRS）](insert-or-delete-a-column-report-builder-and-ssrs.md)。  
  
3.  在 **“插入”** 选项卡的 **“数据区域”** 组中，单击 **“仪表”**，然后单击新列中的单元。 此时将显示 **“选择仪表类型”** 对话框。  
  
4.  单击 **“径向”**。 此时将选中第一个径向仪表。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  单击仪表。 将打开 **“仪表数据”** 窗格。  
  
7.  在“值”区域的“(未指定)”列表框中，单击要将其值显示在仪表中的字段。 或者，从报表数据集拖动要使用的字段。  
  
8.  右键单击仪表，单击“添加指示器”，然后单击“子级”。 **“选择指示器样式”** 对话框将打开。  
  
9. 在 **“选择指示器样式”** 对话框的左窗格中，单击所需的指示器类型，然后单击指示器集。  
  
10. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
11. 单击指示器。 将打开 **“仪表数据”** 窗格。  
  
12. 在“值”区域的“(未指定)”列表框中，单击要将其值显示为指示器的字段。 或者，从报表数据集拖动要使用的字段。  
  
     该字段可与您在仪表中使用的字段相同或不同。  
  
13. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-show-an-indicator-and-gauge-side-by-side"></a>并排显示指示器和仪表  
  
1.  打开一个现有报表，或者创建一个新报表（其中包含具有要显示的数据的表或矩阵）。 有关详细信息，请参阅[表（报表生成器和 SSRS）](tables-report-builder-and-ssrs.md)或[矩阵（报表生成器和 SSRS）](create-a-matrix-report-builder-and-ssrs.md)。  
  
2.  在您的表或矩阵中插入列。 有关详细信息，请参阅[插入或删除列（报表生成器和 SSRS）](insert-or-delete-a-column-report-builder-and-ssrs.md)。  
  
3.  在 **“插入”** 选项卡的 **“数据区域”** 组中，单击 **“仪表”**，然后单击您插入的列中的单元。 将显示 **“选择仪表类型”** 对话框。  
  
4.  单击 **“径向”**。 此时将选中第一个径向仪表。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  单击仪表。 将打开 **“仪表数据”** 窗格。  
  
7.  在“值”区域的“(未指定)”列表框中，单击要将其值显示在仪表中的字段。 或者，从报表数据集拖动要使用的字段。  
  
8.  右键单击仪表，单击“添加指示器”，然后单击“相邻”。 **“选择指示器样式”** 对话框将打开。  
  
9. 在 **“选择指示器样式”** 对话框的左窗格中，单击所需的指示器类型，然后单击指示器集。  
  
10. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
11. 单击指示器。 将打开 **“仪表数据”** 窗格。  
  
12. 在“值”区域的“(未指定)”列表框中，单击要将其值显示为指示器的字段。 或者，从报表数据集拖动要使用的字段。  
  
     该字段可与您在仪表中使用的字段相同或不同。  
  
13. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
14. 右键单击仪表面板，再单击“添加标签”。 此时将向仪表面板添加一个标签。 再重复一次此操作。  
  
     此时仪表面板将具有两个标签。  
  
15. 将每个标签拖到仪表或指示器旁边的位置。  
  
16. 右键单击仪表旁边的标签，单击“标签属性”，然后在“文本”框中键入所需文本。  
  
17. 右键单击指示器旁边的标签，单击“标签属性”，然后在“文本”框中键入所需文本。  
  
18. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [指示器（报表生成器和 SSRS）](indicators-report-builder-and-ssrs.md)  
  
  