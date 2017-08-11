---
title: "将筛选器添加到数据集 （报表生成器和 SSRS） |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eed37e74-6a43-4d7c-9959-2d5fa6a6aba9
caps.latest.revision: 8
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 68838748a77567747cd7f44f7924738d87b68450
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="add-a-filter-to-a-dataset-report-builder-and-ssrs"></a>向数据集添加筛选器（报表生成器和 SSRS）
  向数据集添加筛选器可以在从外部数据源检索数据后限制报表中的数据。 在向数据集添加筛选器后，所有报表部件或数据区域将都只使用与筛选条件匹配的数据。  
  
 对于共享数据集，应用于所有依赖项的筛选器必须是报表服务器上共享数据集定义的一部分。 包含某一共享数据集实例的报表或报表部件可以创建仅应用于该实例的其他筛选器。  
  
 若要添加筛选器，必须指定一个或多个作为筛选器公式的条件。 筛选器公式由标识了要筛选的数据的表达式、运算符和要比较的值组成。 所筛选数据的数据类型和值必须匹配。 不支持筛选数据集的聚合值。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-filter-to-a-shared-dataset"></a>向共享数据集添加筛选器  
  
1.  在共享数据集模式下打开一个共享数据集。  
  
2.  在 **“主页”** 选项卡上的 **“共享数据集”** 组中，单击“数据集”。 此时将打开 **“数据集属性”** 对话框。  
  
3.  单击 **“筛选器”**。 此时将显示当前筛选器公式的列表。 默认情况下，此列表是空的。  
  
4.  单击 **“添加”**。 此时将显示一个新的空白筛选器公式。  
  
5.  在 **“表达式”**中，键入或选择要筛选的字段的表达式。 若要编辑该表达式，请单击表达式 (*fx*) 按钮。  
  
6.  从列表框中选择与您在步骤 5 中创建的表达式的数据类型相匹配的数据类型。  
  
7.  在 **“运算符”** 框中，选择一个供筛选器使用的运算符，以比较 **“表达式”** 框和 **“值”** 框中的值。 您所选择的运算符将决定下一步中使用的值数。  
  
8.  在 **“值”** 框中，键入筛选器对 **“表达式”**中的值进行比较时的目标表达式或值。  
  
     有关筛选器公式的示例，请参阅[筛选器公式示例（报表生成器和 SSRS）](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-add-a-filter-to-an-embedded-dataset-or-a-shared-dataset-instance"></a>向嵌入数据集或共享数据集实例添加筛选器  
  
1.  在报表设计模式下打开一个报表。  
  
2.  右键单击“报表数据”窗格中的数据集，然后单击“数据集属性”。 此时将打开 **“数据集属性”** 对话框。  
  
3.  单击 **“筛选器”**。 此时将显示当前筛选器公式的列表。 默认情况下，此列表是空的。  
  
4.  单击 **“添加”**。 此时将显示一个新的空白筛选器公式。  
  
5.  在 **“表达式”**中，键入或选择要筛选的字段的表达式。 若要编辑该表达式，请单击表达式 (*fx*) 按钮。  
  
6.  从下拉框中选择与您在步骤 5 中创建的表达式的数据类型相匹配的数据类型。  
  
7.  在 **“运算符”** 框中，选择一个供筛选器使用的运算符，以比较 **“表达式”** 框和 **“值”** 框中的值。 您所选择的运算符将决定下一步中使用的值数。  
  
8.  在 **“值”** 框中，键入筛选器对 **“表达式”**中的值进行比较时的目标表达式或值。  
  
     有关筛选器公式的示例，请参阅[筛选器公式示例（报表生成器和 SSRS）](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [添加数据集筛选器、 数据区域筛选器和组筛选器 （&） #40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [表达式示例 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [添加筛选器 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/add-a-filter-report-builder-and-ssrs.md)  
  
  
