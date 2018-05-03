---
title: 刷新数据源视图 (Analysis Services) 中的架构 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9d3cf2ef0c5368664d52ecc9ff0c21a8edfa6061
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="refresh-the-schema-in-a-data-source-view-analysis-services"></a>刷新数据源视图中的架构 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目或数据库中定义数据源视图 (DSV) 后，基础数据源中的架构可能会更改。 无法在开发项目中自动检测或更新这些更改。 此外，如果您已将项目部署到服务器，当 Analysis Services 不再连接到外部数据源时，现在会遇到处理错误。  
  
 为了更新 DSV 以便它与外部数据源匹配，您可以在 Business Intelligence Development Studio (BIDS) 中刷新 DSV。 刷新 DSV 会检测 DSV 所基于的外部数据源的更改，并生成枚举外部数据源中的添加或删除操作的更改列表。 然后您可以将这些更改集应用到 DSV，以便它与基础数据源重新对齐。 请注意，在使用 DSV 的项目中，通常需要做其他工作以进一步更新多维数据集和维度。  
  
 本主题包含以下各节：  
  
 [刷新中支持的更改](#bkmk_changlist)  
  
 [在 SQL Server Data Tools 中刷新 DSV](#bkmk_DSVrefresh)  
  
##  <a name="bkmk_changlist"></a> 刷新中支持的更改  
 “DSV 刷新”可以包含以下任意操作：  
  
-   删除表、列和关系  
  
-   添加列和关系并应用到 DSV 中已包含的表  
  
-   添加新的唯一约束。 如果 DSV 中的表存在逻辑主键，那么，在数据源的表中添加物理键时，逻辑键将被删除并由物理键替换。  
  
 刷新永远不会将新表添加到 DSV 中。 如果要添加新表，必须手动添加。 有关详细信息，请参阅 [在数据源视图中添加或删除表或视图 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md)中的解决方案资源管理器运行数据源视图向导。  
  
##  <a name="bkmk_DSVrefresh"></a> 在 SQL Server Data Tools 中刷新 DSV  
 若要刷新 DSV，双击解决方案资源管理器中从 DSV [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。  这将启动数据源视图设计器。  然后单击设计器中的刷新数据源视图按钮或选择**刷新**从数据源视图菜单。  
  
 在刷新过程中，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将查询所有基础关系数据源以确定 DSV 中包含的表/视图是否发生了更改。 如果建立了到所有基础数据源的连接，并且发生了更改，则您会在 **“刷新数据源视图”** 对话框中看到这些更改。  
  
 ![刷新数据源视图对话框中](../../analysis-services/multidimensional-models/media/ssas-olapdsv-refresh.gif "刷新数据源视图对话框中")  
  
 该对话框将列出要在 DSV 中删除或添加的表、列、约束和关系。 该报表还将列出无法准备好的任意命名查询或计算。 受影响的对象将列在树视图中，其中的列和关系嵌套在表下面，并且指示出每个对象的更改类型（删除或添加）。 标准数据源视图对象图标指示受影响的对象类型。  
  
 刷新操作完全基于基础对象的名称进行。 因此，如果在数据源中重命名了一个基础对象，则数据源视图设计器将把重命名对象视为两个单独的操作 - 删除和添加。 在这种情况下，必须手动将重命名后的对象重新添加到数据源视图中。 您还可能必须重新创建关系或逻辑主键。  
  
> [!IMPORTANT]  
>  如果已经知道已在数据源中重命名了表，则可以在刷新数据源视图之前，使用 **“替换表”** 命令将表替换为重命名后的表。 有关详细信息，请参阅[在数据源视图中替换表或命名查询 (Analysis Services)](../../analysis-services/multidimensional-models/replace-a-table-or-a-named-query-in-a-data-source-view-analysis-services.md)。  
  
 检查了报表之后，可以接受更改，也可以取消更新以拒绝任何更改。 必须接受或拒绝所有更改。 不能选择列表中的单个项。 您还可以保存更改报告。  
  
## <a name="see-also"></a>另请参阅  
 [多维模型中的数据源视图](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
