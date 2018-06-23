---
title: 分析关键影响因素 （Excel 表分析工具） |Microsoft 文档
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
- key influencers
- factor analysis
ms.assetid: 54d7b4ce-7b79-407a-985c-aa655ad19280
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 41b30eb0f3f0dc68c5666581a2682470fac7f978
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018330"
---
# <a name="analyze-key-influencers-table-analysis-tools-for-excel"></a>分析关键影响因素（Excel 表分析工具）
  ![功能区中的分析关键影响因素按钮](media/tat-aki.gif "功能区中的分析关键影响因素按钮")  
  
 与**分析关键影响因素**工具，你选择一列以包含目标结果，然后由算法确定哪些因素有的结果的最高影响。  
  
 该工具可创建若干新数据表，这些表将报告与每个结果相关联的因素，并以图形方式显示它们之间存在关系的概率。 可以基于不同因素和结果对这些表进行筛选，以更深入地研究结果。  
  
 还可选择可能得到的一对结果并对它们进行比较。 例如，您可以比较不同的使用者组来确定可能影响决策的因素。  
  
## <a name="using-the-analyze-key-influencers-tool"></a>使用“分析关键影响因素”工具  
  
1.  打开 Excel 数据表。  
  
2.  在**表工具**上**分析**功能区上，单击**分析关键影响因素。**  
  
3.  选择单个列作为分析目标。  
  
4.  （可选） 单击**选择要用于分析列**。 在**高级列选择**对话框框中，选择最有可能包含相关数据的列。 若要改进性能和精确性，请取消选择诸如 ID 或名称等对模式分析不重要的列。 单击**确定**关闭**高级列选择**对话框。  
  
5.  单击 **“运行”**。  
  
     **分析关键影响因素**工具进行分析的数据以确定最佳的设置，并自动设置所有参数。  
  
6.  如果未检测到模式，该向导会创建一个新工作表，该表含有对问题的说明。  
  
7.  如果检测到模式，则向导将在新的工作表中创建一个报表以显示这些模式。 此报告称为**有关的关键影响因素\<列 >**。 可以按照以下步骤所述自定义该报表。  
  
#### <a name="create-a-custom-report"></a>创建自定义报表  
  
1.  在**对比基于关键影响因素**对话框框中，选择你想要通过选择从它们进行比较的两个值**值 1**和**值 2**的下拉列表. 例如，您可以将购买者与非购买者进行比较。  
  
2.  单击**添加报表**。  
  
     该向导将创建新工作表，并为每对关键因素比较添加一个表。  
  
3.  完成进行比较后，单击**关闭**。  
  
## <a name="understanding-the-key-influencers-report"></a>了解关键影响因素报表  
 创建数据模型后，**分析关键影响因素**工具可创建报告，帮助你浏览和比较关键影响因素。  
  
-   左侧的报表是默认情况下生成的一个报表。 其中显示对于结果列（因变量）影响最大的预测因子。  
  
-   右侧的报表是可选报表，可通过比较两个特定的结果值创建该报表。 此报表将比较购买者与非购买者。  
  
-   注意，对于所创建的每个报表都会添加一个新的工作表。 在创建表后，可移动这些表；我们将这些表并行放在一起进行比较。  
  
 ![DM13](media/dm13-tat-aki-report.gif "DM13")  
  
 **相对影响**  
 第一个报表中的阴影条指示此属性与结果的关联强度。  
  
 色条长度指示该因素影响结果的概率；因此，阴影条越长，关联性越强。  
  
 **优先**  
 第二个报表中，在两列中列出所比较的目标值，其中按置信度降序列出相关因素。  
  
-   **蓝色**栏显示特性导致的结果，"否"(= 未购买)。  
  
-   **红色**栏显示特性提供的结果，"是"(= 购买自行车)。  
  
 阴影条的颜色是任意的， 在 Excel 中设置表设计选项即可更改这些颜色。  
  
 在比较两个值的报表中，第二个报表根据对目标值的影响程度为关键影响因素排名。  
  
 由于所有图表都基于 Excel 表，因此可进行筛选和排序，重点关注特定的因素或结果。  
  
## <a name="more-about-the-analyze-key-influencers-tool"></a>有关“分析关键影响因素”工具的详细信息  
 当**分析关键影响因素**工具将分析数据，则它不以下：  
  
-   创建一个数据结构，其中存储有关数据分布的关键信息。  
  
-   使用 Microsoft Naïve Bayes 算法创建一个模型。  
  
-   创建将每列数据与指定结果关联起来的预测。  
  
-   使用每个预测的置信度分数找出对产生目标结果影响最大的因素。  
  
-   创建一个报表，其中描述按置信度得分排序的关键影响因素。  
  
### <a name="requirements"></a>要求  
 如果目标列包含连续数值，该工具会自动将这些数值分组。 这些分组表示具有相似特征的事例的分类。 但该工具可能不会将这些数值分成用户友好组。 例如，该报告可能包含如的分组"\<12.85701"，而报表用户通常想要查看使用整数 10-19、 20-29 个，等的分组。  
  
 如果希望以其他方式对数值数据分组，必须在创建分析之前以希望的方式拆分这些数据。 例如，你可以使用[重新标记发生](relabel-sql-server-data-mining-add-ins.md)中用于在单独的列中，创建新的分组标签，然后使用在分析中的仅该新列的 Excel 数据挖掘客户端工具。  
  
### <a name="related-tools"></a>相关工具  
 **数据挖掘**功能区提供更高级的工具，包括自定义数据挖掘模型的功能  
  
 如果使用保存您的模型**分析关键影响因素**工具，你可以使用数据挖掘客户端可以浏览该模型和浏览更多详细信息中的关系。 有关信息，请参阅[Excel 中浏览模型&#40;SQL Server 数据挖掘外接程序&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)。 还可以使用 Microsoft Office Visio 创建图表和关系图，将关系显示为分类或依赖关系网络。 有关详细信息，请参阅[疑难解答 Visio 数据挖掘图&#40;SQL Server 数据挖掘外接程序&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)。  
  
> [!NOTE]  
>  在关闭工作表或终止与 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服务器的连接时，将删除使用表分析工具创建的模型。 因此，只有在连接处于打开状态时才能浏览模型。 如果关闭连接或关闭工作表，则无法在 Visio 中呈现模型。  
  
 有关使用的算法的详细信息**分析关键影响因素**工具，请参阅 SQL Server 联机丛书中的"Microsoft 的 Naïve Bayes 算法"。  
  
## <a name="see-also"></a>请参阅  
 [Excel 表分析工具](table-analysis-tools-for-excel.md)   
 [创建数据挖掘模型](creating-a-data-mining-model.md)  
  
  