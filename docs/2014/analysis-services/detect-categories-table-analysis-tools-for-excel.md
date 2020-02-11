---
title: 检测类别（Excel 表分析工具） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- clustering [data mining]
- mining model, decision tree
- category detection
ms.assetid: 3c7e9ebb-d0c9-498e-a9ba-cc13eaa43520
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 06c466eb5e3275818a710a9f9d90c705ed93c957
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66081856"
---
# <a name="detect-categories-table-analysis-tools-for-excel"></a>检测类别（Excel 表分析工具）
  ![功能区中的“检测类别”按钮](media/tat-detectcat.gif "功能区中的“检测类别”按钮")  
  
 "**检测类别**" 工具在表中自动查找具有类似特征的行。  
  
 此工具完成查找后，它将创建一个报表，其中列出所找到的类别以及这些类别的区分特征。 默认情况下，它会针对每一行数据向数据表中添加一个包含所推荐类别的新列。 然后，您可以检查这些类别并重命名它们。  
  
## <a name="using-the-detect-categories-tool"></a>使用检测类别工具  
  
1.  打开 Excel 表。  
  
2.  单击 "**检测类别**"。  
  
3.  指定要在分析中使用的列。 您可以取消选择具有非重复值（例如人名或记录 ID）的列，因为这些列对于分析来说可能无用。  
  
4.  您可以选择指定要创建的类别的最大数目。 默认情况下，该工具找到多少个类别，就会自动创建多少个类别。  
  
5.  单击 **“运行”** 。  
  
6.  此工具创建一个名为“类别报表”的新工作表，其中包含类别的列表以及它们的特征。  
  
 有关如何为该工具指定选项的详细信息，请参阅 "[检测类别" 对话框（Excel 表分析工具）](detect-categories-table-analysis-tools-for-excel.md)。  
  
## <a name="understanding-the-categories-report"></a>了解分类报表  
 "**类别" 报表**包含两个表： "**类别列表**" 和 "**类别特征**"，以及 "**类别配置文件**" 图表。  
  
### <a name="category-list"></a>类别列表  
 第一个表列出找到的类别。 "**行计数**" 列指示分配给每个类别的数据行数。  
  
 该模型创建每个类别的临时名称，但是您可以随意将其重命名。 例如，在下面的示例中，第一个类别已重命名为**低收入**，因为这是群集的顶级属性。  
  
 ![用“检测类别”工具创建的报告](media/dm13-tat-detectcat-report1.gif "用“检测类别”工具创建的报告")  
  
 键入新标签后，更改即传播到所有其他图表以及源数据工作表中添加的类别列表。  
  
### <a name="category-characteristics"></a>类别特征  
 第二个表 "**类别特征**" 显示有关每个类别的构成的详细信息。 单击 "**类别**" 列顶部的 "**筛选器**" 按钮，以查看焦点上的一个或多个类别。  
  
 ![用“检测类别”工具创建的报告](media/dm13-tat-detectcat-report2.gif "用“检测类别”工具创建的报告")  
  
 列中的底纹**相对重要性**表明，属性和值的组合是一种区分因素的重要程度。 该条越长，此属性越可能充分代表此类别。  
  
### <a name="categories-profile-chart"></a>类别分布图  
 "**类别报表**" 工作表中的最终图表是一个交互式**透视图** **，可**用于重新排列和隐藏字段、对值进行筛选和自定义图表的外观。  
  
 Excel 2013 现在提供了设计图面中的**图表样式**和**图表元素**控件，使您可以轻松地改进图表设计。  
  
 ![用“检测类别”工具创建的报告](media/dm13-tat-detectcat-report3.gif "用“检测类别”工具创建的报告")  
  
## <a name="requirements"></a>要求  
 "**检测类别**" 工具不要求数据量或数据类型。  
  
> [!NOTE]  
>  使用 "**检测类别**" 工具时，它会在原始数据表中创建新的列 "类别"。 如果将此列保留在数据表中，然后执行后续数据挖掘操作，则此列的存在可能会影响您的分析结果。 为了确保这不会影响其他操作，您应制作一份不包含“类别”列的数据表副本，然后再使用其他数据挖掘工具。  
  
## <a name="related-tools"></a>相关工具  
 当 "**检测类别**" 工具分析您的数据时，它将使用[!INCLUDE[msCoName](../includes/msconame-md.md)]聚类分析算法创建数据挖掘结构和数据挖掘模型。  
  
 使用 "**分析关键影响因素**" 工具创建数据挖掘模型之后，您可以使用 Excel 数据挖掘客户端浏览该模型并更详细地浏览关系。 Excel 数据挖掘客户端是一个独立的外接程序，它提供了更多的高级数据挖掘功能。 有关信息，请参阅[在 Excel 中浏览模型 &#40;SQL Server 数据挖掘外接程序&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)。  
  
 有关使用 Excel 数据挖掘客户端中的数据建模功能的详细信息，请参阅[创建数据挖掘模型](creating-a-data-mining-model.md)。  
  
 有关 "**检测类别**" 工具使用的算法的详细信息，请参阅联机丛书中[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的主题 "Microsoft 聚类分析算法"。  
  
## <a name="see-also"></a>另请参阅  
 [Excel 表分析工具](table-analysis-tools-for-excel.md)  
  
  
