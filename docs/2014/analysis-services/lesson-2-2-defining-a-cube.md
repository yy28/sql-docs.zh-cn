---
title: 定义多维数据集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 8aa4ac2d-857f-4048-baa0-0f314e207cf6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 167121188939bcf82ed359ac3f8cf7e3aae47635
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66079059"
---
# <a name="defining-a-cube"></a>定义多维数据集
  多维数据集向导可以帮助您为多维数据集定义度量值组和维度。 在下面的任务中，将使用维度向导来构建多维数据集。  
  
### <a name="to-define-a-cube-and-its-properties"></a>定义多维数据集及其属性  
  
1.  在解决方案资源管理器中，右键单击“多维数据集”****，然后单击“新建多维数据集”****。 多维数据集向导将显示。  
  
2.  在“欢迎使用多维数据集向导”**** 页上，单击“下一步”****。  
  
3.  在“选择创建方法”**** 页上，确认已选中“使用现有表”**** 选项，然后单击“下一步”****。  
  
4.  在“选择度量值组表”**** 页上，确认已选中“Adventure Works DW 2012”**** 数据源视图。  
  
5.  单击“建议”**** 允许多维数据集向导建议要用来创建度量值组的表。  
  
     该向导会检查这些表并建议将 **InternetSales** 作为度量值组表。 度量值组表（又称为事实数据表）包含你感兴趣的度量值（如已销售的单位数）。  
  
6.  单击“下一步”  。  
  
7.  在“选择度量值”**** 页上，查看在“Internet 销售”**** 度量值组中选择的度量值，然后清除下列度量值的复选框：  
  
    -   **促销关键字**  
  
    -   **货币关键字**  
  
    -   **销售区域关键字**  
  
    -   **修订号**  
  
     默认情况下，该向导会选择将事实数据表中未链接到维度的所有数值列作为度量值。 但这四列不是实际的度量值。 前三列是将事实数据表与未在此多维数据集的初始版本中使用的维度表链接起来的键值。  
  
8.  单击“下一步”  。  
  
9. 在“选择现有维度”**** 页上，确保选择了以前创建的“日期”**** 维度，然后单击“下一步”****。  
  
10. 在“选择新维度”**** 页上，选择要创建的新维度。 为此，请确认已选中“客户”****、“地域”**** 和“产品”**** 复选框，然后清除“InternetSales”**** 复选框。  
  
11. 单击“下一步”  。  
  
12. 在 "**完成向导**" 页上，将多维数据集的名称`Analysis Services Tutorial`更改为。 在“预览”窗格中，可以看到 **InternetSales** 度量值组及其度量值。 还可以看到“日期”****、“客户”**** 和“产品”**** 维度。  
  
13. 单击 **“完成”** 以完成向导。  
  
     在解决方案资源管理器的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 项目中，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 多维数据集显示在“多维数据集”**** 文件夹中，而“客户”和“产品”数据库维度则显示在“维度”**** 文件夹中。 此外，“多维数据集结构”选项卡在开发环境的中央显示 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 多维数据集。  
  
14. 在“多维数据集结构”选项卡的工具栏上，将“缩放”**** 级别更改为 50 %，以便更轻松地查看多维数据集内的维度和事实数据表。 注意，事实数据表是黄色的，维度表是蓝色的。  
  
15. 在“文件” **** 菜单上，单击“全部保存” ****。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [向维度添加属性](lesson-2-3-adding-attributes-to-dimensions.md)  
  
## <a name="see-also"></a>另请参阅  
 [多维模型中的多维数据集](multidimensional-models/cubes-in-multidimensional-models.md)   
 [多维模型中的维度](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
