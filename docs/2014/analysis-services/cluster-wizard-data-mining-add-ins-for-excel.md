---
title: 群集向导 （Excel 数据挖掘外接程序） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- clustering [data mining]
ms.assetid: 85b25625-a7ab-4960-9f9c-df22e8ecae37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7803b5a5a2fccd3381b827eb15a19e036ffa017e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62680750"
---
# <a name="cluster-wizard-data-mining-add-ins-for-excel"></a>聚类分析向导（Excel 数据挖掘外接程序）
  ![数据挖掘功能区中的群集向导](media/dmc-cluster.gif "数据挖掘功能区中的群集向导")  
  
 聚类分析向导可帮助您建立模型，检测共享类似特征的行并对这些行进行分组，以最大限度地增加这些组之间的距离。 此向导对于查找各种类型数据中的模式非常有用。  
  
 聚类分析向导使用 Microsoft 聚类分析算法，可以进行广泛的自定义。 该向导可用于现有的数据，包括 Excel 表、Excel 区域或 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 查询。 通过提供类似的功能[检测类别](detect-categories-table-analysis-tools-for-excel.md)Excel 表分析工具中提供的工具。 不过，检测类别工具无法自定义，必须使用 Excel 表中的数据。  
  
## <a name="using-the-cluster-wizard"></a>使用聚类分析向导  
  
1.  在数据挖掘功能区中，单击**群集**，然后单击**下一步**。  
  
2.  在中**选择源数据**页上，选择 Excel 表或范围。 也可以指定外部数据源。  
  
     如果使用外部数据源，您可以创建自定义视图或粘贴上自定义查询文本并将数据集另存为 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据源。  
  
3.  上**聚类分析**页上，你可以自定义构建的模型的方式。  
  
    -   有关**段数**，可以告知向导以创建固定的数量的类别，或让它自动检测最佳的分组数。  
  
    -   查看列表中的列**输入列**列表，并取消选择不在创建模式非常有用的任何列。 应排除的列包括 ID 编号、客户名称等。  
  
4.  （可选） 单击**参数**可更改算法参数以及自定义聚类分析模型的行为。  
  
5.  在中**将数据拆分为定型集和测试集**页上，指定要为进行测试数据量。 剩余的数据始终用于定型模型。  
  
     默认设置为 30% 的测试数据和 70% 的定型数据。  
  
6.  上**完成**页上，提供你的数据集和模型的描述性名称并设置以下选项控制在完成的模型的使用方式：  
  
    -   **浏览模型**。 选中此选项后，尽快在向导完成处理模型，它会打开**浏览**窗口，从而帮助您浏览结果。 查看器的内容取决于您建立的模型的类型。 有关详细信息，请参阅[浏览聚类分析模型](browsing-a-clustering-model.md)。  
  
    -   **启用钻取**。 选择此选项可以查看已完成模型中的基础数据。 此选项仅在建立决策树模型时可用。  
  
    -   **使用临时模型**。 如果您选择此选项，模型将不会被保存到服务器。 在您关闭 Excel 时，临时模型将被删除。  
  
## <a name="more-about-clustering-models"></a>有关聚类分析模型的详细信息  
 你可以通过使用此向导的聚类分析算法**高级**并使用**算法参数**对话框。  
  
 Microsoft 聚类分析算法提供以下聚类分析方法：  
  
-   K-means - 可缩放或不可缩放。  
  
-   期望最大化 (EM) - 可缩放或不可缩放。  
  
 您还可以使用 CLUSTER_SEED 参数来控制起始值，确保使用相同数据集的重复模型具有相同的结果。  
  
### <a name="requirements"></a>要求  
 若要使用聚类分析向导，您必须连接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库。 有关详细信息，请参阅[连接到源数据&#40;Excel 数据挖掘客户端&#41;](connect-to-source-data-data-mining-client-for-excel.md)。  
  
## <a name="see-also"></a>请参阅  
 [创建数据挖掘模型](creating-a-data-mining-model.md)   
 [检测类别&#40;Excel 表分析工具&#41;](detect-categories-table-analysis-tools-for-excel.md)  
  
  
