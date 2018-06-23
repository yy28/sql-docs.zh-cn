---
title: 检测类别 （有关 Excel 表分析工具） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Table Analysis tools
- clustering [data mining]
- mining model, decision tree
- category detection
ms.assetid: 3c7e9ebb-d0c9-498e-a9ba-cc13eaa43520
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: d46840e2c2f7de1d56d6b528706ae908e7627a3e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024690"
---
# <a name="detect-categories-table-analysis-tools-for-excel"></a>检测类别（Excel 表分析工具）
  ![功能区中的检测类别按钮](media/tat-detectcat.gif "功能区中的检测类别按钮")  
  
 **检测类别**工具自动查找具有类似特征的表中的行。  
  
 此工具完成查找后，它将创建一个报表，其中列出所找到的类别以及这些类别的区分特征。 默认情况下，它会针对每一行数据向数据表中添加一个包含所推荐类别的新列。 然后，您可以检查这些类别并重命名它们。  
  
## <a name="using-the-detect-categories-tool"></a>使用检测类别工具  
  
1.  打开 Excel 表。  
  
2.  单击**检测类别**。  
  
3.  指定要在分析中使用的列。 您可以取消选择具有非重复值（例如人名或记录 ID）的列，因为这些列对于分析来说可能无用。  
  
4.  您可以选择指定要创建的类别的最大数目。 默认情况下，该工具找到多少个类别，就会自动创建多少个类别。  
  
5.  单击 **“运行”**。  
  
6.  此工具创建一个名为“类别报表”的新工作表，其中包含类别的列表以及它们的特征。  
  
 有关如何指定该工具的选项的详细信息，请参阅[检测类别对话框中 （Excel 表分析工具）](detect-categories-table-analysis-tools-for-excel.md)。  
  
## <a name="understanding-the-categories-report"></a>了解分类报表  
 **类别报表**包含两个表，**类别列表**和**类别特征**，和一个**类别配置文件**图表。  
  
### <a name="category-list"></a>类别列表  
 第一个表列出找到的类别。 **行计数**列指示如何很多行数据已分配到每个类别。  
  
 该模型创建每个类别的临时名称，但是您可以随意将其重命名。 例如，在下面的示例中，第一类已重命名**低收入**，因为，在群集的最上面的属性。  
  
 ![检测类别工具创建的报表](media/dm13-tat-detectcat-report1.gif "检测类别工具创建的报表")  
  
 键入新标签后，更改即传播到所有其他图表以及源数据工作表中添加的类别列表。  
  
### <a name="category-characteristics"></a>类别特征  
 第二个表，**类别特征**，显示有关组成部分的每个类别的详细信息。 单击**筛选器**顶部的按钮**类别**列以查看上一个或几个类别的焦点。  
  
 ![检测类别工具创建的报表](media/dm13-tat-detectcat-report2.gif "检测类别工具创建的报表")  
  
 在列中，明暗度**相对重要性**，该值指示如何重要的属性和值的组合是作为可分辨的因素。 该条越长，此属性越可能充分代表此类别。  
  
### <a name="categories-profile-chart"></a>类别分布图  
 中的最后一个图表**类别报表**工作表，**类别配置文件**，是交互式**透视图**可用于重新排列和隐藏字段，对值进行筛选并自定义图表的外观。  
  
 Excel 2013 现在提供**图表样式**和**图表元素**控制方便地提高图表设计的设计图面中的权限。  
  
 ![检测类别工具创建的报表](media/dm13-tat-detectcat-report3.gif "检测类别工具创建的报表")  
  
## <a name="requirements"></a>要求  
 **检测类别**工具为量或数据类型有没有要求。  
  
> [!NOTE]  
>  当你使用**检测类别**工具，它在原始表中数据创建一个新列，类别。 如果将此列保留在数据表中，然后执行后续数据挖掘操作，则此列的存在可能会影响您的分析结果。 为了确保这不会影响其他操作，您应制作一份不包含“类别”列的数据表副本，然后再使用其他数据挖掘工具。  
  
## <a name="related-tools"></a>相关工具  
 当**检测类别**工具将分析数据，将会创建数据挖掘结构和数据挖掘模型使用[!INCLUDE[msCoName](../includes/msconame-md.md)]聚类分析算法。  
  
 使用创建数据挖掘模型后**分析关键影响因素**工具，你可以使用 Excel 数据挖掘客户端可以浏览该模型和浏览更多详细信息中的关系。 Excel 数据挖掘客户端是一个独立的外接程序，它提供了更多的高级数据挖掘功能。 有关信息，请参阅[Excel 中浏览模型&#40;SQL Server 数据挖掘外接程序&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)。  
  
 有关使用 excel 建模中数据挖掘客户端功能的数据的详细信息，请参阅[创建数据挖掘模型](creating-a-data-mining-model.md)。  
  
 有关使用的算法的详细信息**检测类别**工具，请参阅中的主题"Microsoft 聚类分析算法"[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]联机丛书。  
  
## <a name="see-also"></a>请参阅  
 [Excel 表分析工具](table-analysis-tools-for-excel.md)  
  
  