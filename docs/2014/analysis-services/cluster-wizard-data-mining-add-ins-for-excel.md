---
title: 群集向导（Excel 数据挖掘外接程序） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- clustering [data mining]
ms.assetid: 85b25625-a7ab-4960-9f9c-df22e8ecae37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d93f676aec67b5d791924cbbda8f71a966d5bbc2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66087811"
---
# <a name="cluster-wizard-data-mining-add-ins-for-excel"></a>聚类分析向导（Excel 数据挖掘外接程序）
  ![“数据挖掘”功能区中的聚类分析向导](media/dmc-cluster.gif "“数据挖掘”功能区中的聚类分析向导")  
  
 聚类分析向导可帮助您建立模型，检测共享类似特征的行并对这些行进行分组，以最大限度地增加这些组之间的距离。 此向导对于查找各种类型数据中的模式非常有用。  
  
 聚类分析向导使用 Microsoft 聚类分析算法，可以进行广泛的自定义。 该向导可用于现有的数据，包括 Excel 表、Excel 区域或 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 查询。 与 Excel 表分析工具中提供的 "[检测类别](detect-categories-table-analysis-tools-for-excel.md)" 工具相似，它也提供了类似功能。 不过，检测类别工具无法自定义，必须使用 Excel 表中的数据。  
  
## <a name="using-the-cluster-wizard"></a>使用聚类分析向导  
  
1.  在 "数据挖掘" 功能区中，单击 "**群集**"，然后单击 "**下一步**"。  
  
2.  在 "**选择源数据**" 页中，选择 Excel 表或区域。 也可以指定外部数据源。  
  
     如果使用外部数据源，您可以创建自定义视图或粘贴上自定义查询文本并将数据集另存为 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据源。  
  
3.  在 "**聚类分析**" 页上，您可以自定义模型的生成方式。  
  
    -   对于**段数**，可以让向导创建固定数量的类别，或者让它自动检测最佳的分组数。  
  
    -   查看 "**输入列**" 列表中的列的列表，然后取消选择在创建模式中不起作用的任何列。 应排除的列包括 ID 编号、客户名称等。  
  
4.  （可选）单击 "**参数**" 更改算法参数，并自定义聚类分析模型的行为。  
  
5.  在 "将**数据拆分为定型集和测试集**" 页中，指定要保留多少数据用于测试。 剩余的数据始终用于定型模型。  
  
     默认设置为 30% 的测试数据和 70% 的定型数据。  
  
6.  在 "**完成**" 页上，为数据集和模型提供描述性名称，并设置以下选项来控制使用已完成模型的方式：  
  
    -   **浏览模型**。 如果选择此选项，向导处理完模型后就会立即打开 "**浏览**" 窗口，以帮助您浏览结果。 查看器的内容取决于您建立的模型的类型。 有关详细信息，请参阅[浏览聚类分析模型](browsing-a-clustering-model.md)。  
  
    -   **启用钻取**。 选择此选项可以查看已完成模型中的基础数据。 此选项仅在建立决策树模型时可用。  
  
    -   **使用临时模型**。 如果您选择此选项，模型将不会被保存到服务器。 在您关闭 Excel 时，临时模型将被删除。  
  
## <a name="more-about-clustering-models"></a>有关聚类分析模型的详细信息  
 通过单击 "**高级**" 并使用 "**算法参数**" 对话框，可以更改此向导使用的聚类分析算法。  
  
 Microsoft 聚类分析算法提供以下聚类分析方法：  
  
-   K-means - 可缩放或不可缩放。  
  
-   期望最大化 (EM) - 可缩放或不可缩放。  
  
 您还可以使用 CLUSTER_SEED 参数来控制起始值，确保使用相同数据集的重复模型具有相同的结果。  
  
### <a name="requirements"></a>要求  
 若要使用聚类分析向导，您必须连接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库。 有关详细信息，请参阅[连接到源数据 &#40;Excel 数据挖掘客户端&#41;](connect-to-source-data-data-mining-client-for-excel.md)。  
  
## <a name="see-also"></a>另请参阅  
 [创建数据挖掘模型](creating-a-data-mining-model.md)   
 [检测类别 &#40;Excel&#41;的表分析工具](detect-categories-table-analysis-tools-for-excel.md)  
  
  
