---
title: 突出显示异常 （Excel 表分析工具） |Microsoft 文档
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
- highlight exceptions
ms.assetid: d90a12f8-7bc3-4fdb-95a1-7c89058f0d9a
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 359ca09bdb3e722d44a42bde001eaffc58794ac5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126768"
---
# <a name="highlight-exceptions-table-analysis-tools-for-excel"></a>突出显示异常值（Excel 表分析工具）
  ![突出显示功能区中的异常按钮](media/tat-highlightex.gif "功能区中的突出显示异常按钮")  
  
 有时您的数据可能包含异常的值。 例如，可能列出某位屋主的年龄为 5 岁。 这些值，通常称为*离群值*，由于数据输入错误，可能有误，或者它们可能表示异常的趋势。 不管是哪种情况，异常值都可能影响分析的质量。 **突出显示异常**工具可帮助你查找这些值，并为后续操作中查看它们。  
  
 **突出显示异常**工具可以使用的整个范围的数据在 Excel 数据表中，或者可以选择仅少量的列。 您还可以调整控制数据变化范围的阈值，以找到更多或更少的异常值。  
  
 工具完成分析时将创建一个新工作表，其中包含在所分析的各个列中找到了多少离群值的汇总报表。 该工具还会在原始数据表中突出显示异常值。 由于该工具分析的是整体趋势，因此可能会发现行中的大多数值是正常的，并将只突出显示该行中的一个单元格。 在上面，唯一的户主示例**年龄**列可能会突出显示。  
  
 你还可以更改**异常阈值**中的值**摘要报表**。 此值指示特定单元格包含异常值的概率。 因此，如果您增大该值，则更少的值被突出显示为离群值。 反之，减小该值将显示更多突出显示的单元格。  
  
## <a name="using-the-highlight-exceptions-tool"></a>使用突出显示异常工具  
  
1.  打开的 Excel 表，然后单击**突出显示异常**。  
  
2.  指定要分析的列。  
  
3.  单击 **“运行”**。  
  
4.  打开工作表标题为\<表名 > 离群值来查看离群值找到的摘要。  
  
5.  若要更改突出显示的数，请单击向上和向下箭头中的**异常阈值**一行**突出显示异常报表**。  
  
### <a name="requirements"></a>要求  
 如果有些看似异常的值包含了可用于预测其他行的信息，它们不一定是错误的，您仍可以包含具有这些值的列。 但您应该取消选择缺失了许多值或有许多零值的列。  
  
 由于所有所选列都用于创建常规模式，因此应避免使用类似如下已知包含不良信息的输入列：  
  
-   包含唯一值（如 ID）的列。  
  
-   包含错误值所占比率高的列。  
  
-   包含多个缺失值的列。  
  
     请注意，在某些情况下，需要包含具有多个缺失值的输入列。 例如，如果客户通过零售店购买时总是缺少地址字段的值，数据挖掘算法可以使用此信息识别其他类似的客户。 您必须基于每个案例确定缺失的数据是疏忽造成的还是“缺失”状态是有意义的。  
  
-   创建模式时不太可能有用的列。 例如，每行中具有相同值的列不会添加对生成模式有用的任何信息。  
  
## <a name="understanding-the-highlight-exceptions-report"></a>了解突出显示异常值报表  
 当你单击**运行**，该工具执行三项操作：  
  
-   根据表中的当前数据创建数据挖掘结构。  
  
-   使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 聚类分析算法创建新的数据挖掘模型。  
  
-   按照模式创建预测查询，以确定工作表中的任何值是否是不可能的。  
  
 异常阈值的初始值始终为 75，这表示算法计算的突出显示数据的有错几率为 75%。 该工具自动设置此阈值以便能够通过初始分析，但您可以在报表中更改此值。  
  
 **突出显示异常**工具突出显示了可疑原始数据表中的单元格。 深色突出显示表示需要注意该行。 浅色突出显示表示特定单元格中的值很可疑。 如果更改异常的阈值，突出显示的值将相应地更改。  
  
 摘要图表显示每列中超出异常阈值的单元格的数量。  
  
## <a name="related-tools"></a>相关工具  
 在清除或检查数据以为数据挖掘作准备时，您还可以尝试使用 Excel 数据挖掘客户端中的数据浏览功能。 此外接程序提供了更高级的工具，可以帮助您查找离散值、重新标记数据或者查看数据的分布情况。 Excel 数据挖掘客户端中的数据浏览工具的详细信息，请参阅[浏览和清理数据](exploring-and-cleaning-data.md)。  
  
 **突出显示异常**工具使用[!INCLUDE[msCoName](../includes/msconame-md.md)]聚类分析算法。 聚类分析模型检测各组具有相似特征的行。 Excel 数据挖掘客户端提供**浏览**使用关系图和特征的配置文件来让你浏览数据挖掘模型创建的群集的窗口。 有关如何浏览通过创建的聚类分析模型信息**突出显示异常**工具，请参阅[浏览模型 （数据挖掘客户端 for Excel）](highlight-exceptions-table-analysis-tools-for-excel.md)。  
  
 有关 [!INCLUDE[msCoName](../includes/msconame-md.md)] 聚类分析算法的详细信息，请参阅 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 联机丛书中的主题“Microsoft 聚类分析算法”。  
  
## <a name="see-also"></a>请参阅  
 [Excel 表分析工具](table-analysis-tools-for-excel.md)  
  
  