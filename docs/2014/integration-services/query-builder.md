---
title: 查询生成器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.querybuilder.f1
helpviewer_keywords:
- Query Builder dialog box
ms.assetid: 780752c9-6e3c-4f44-aaff-4f4d5e5a45c5
caps.latest.revision: 37
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fc765cfceb8e52d3fbb578e3c3b6f212f28a3291
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37156318"
---
# <a name="query-builder"></a>查询生成器
  可以使用 **“查询生成器”** 对话框，创建在执行 SQL 任务、OLE DB 源和 OLE DB 目标以及查找转换中使用的查询。  
  
 可以使用查询生成器来执行下列任务：  
  
-   **使用查询的图形表示形式或 SQL 命令** 查询生成器包括以图形方式显示查询的窗格和以 SQL 文本方式显示查询的窗格。 您既可以在图形窗格中工作，也可以在文本窗格中工作。 查询生成器可以同步视图，使其始终保持为最新状态。  
  
-   **联接相关表** 如果将多个表添加到查询中，查询生成器将自动确定这些表之间的关系，并构造相应的联接命令。  
  
-   **查询或更新数据库** 可以使用查询生成器通过 Transact-SQL SELECT 语句来返回数据，还可使用它来创建查询以便更新、添加或删除数据库中的记录。  
  
-   **立即查看和编辑结果** 您可以运行查询，在可滚动和编辑数据库中各记录的网格中对记录集进行操作。  
  
 “查询生成器”对话框中的图形工具使你可以使用拖放操作来构造查询。 默认情况下，“查询生成器”对话框将生成 SELECT 查询，但也可以生成 INSERT、UPDATE 或 DELETE 查询。 还可以在 **“查询生成器”** 对话框中分析和运行所有类型的 SQL 语句。 有关包中 SQL 语句的详细信息，请参阅 [Integration Services (SSIS) 查询](integration-services-ssis-queries.md)。  
  
 若要了解关于 Transact-SQL 语言及其语法的详细信息，请参阅 [Transact-SQL 引用（数据库引擎）](/sql/t-sql/language-reference)。  
  
 还可以在查询中使用变量，以便为输入参数提供值、捕获输出参数的值并存储返回代码。 若要了解包所使用的查询中使用变量的详细信息，请参阅[执行 SQL Task](control-flow/execute-sql-task.md)[OLE DB 源](data-flow/ole-db-source.md) 和 [Integration Services (SSIS) 查询](integration-services-ssis-queries.md)。 若要了解有关在执行 SQL 任务中使用变量的详细信息，请参阅 [执行 SQL 任务中的参数和返回代码](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md) 和 [执行 SQL 任务中的结果集](../../2014/integration-services/result-sets-in-the-execute-sql-task.md)。  
  
 查找转换和模糊查找转换也可以使用带有参数和返回代码和变量。 有关 OLE DB 源的信息也适用于上述两种转换。  
  
## <a name="options"></a>“常规”  
 **工具栏**  
 使用工具栏可以管理数据集、选择要显示的窗格以及控制查询函数。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**显示/隐藏关系图窗格**|显示或隐藏 **“关系图”** 窗格。|  
|**显示/隐藏网格窗格**|显示或隐藏 **“网格”** 窗格。|  
|**显示/隐藏 SQL 窗格**|显示或隐藏 **SQL** 窗格。|  
|**显示/隐藏结果窗格**|显示或隐藏 **“结果”** 窗格。|  
|**运行**|运行查询。 结果将显示在结果窗格中。|  
|**验证 SQL**|验证 SQL 语句是否有效。|  
|**升序排序**|依据网格窗格中的所选列对输出行按升序排序。|  
|**降序排序**|依据网格窗格中的所选列对输出行按降序排序。|  
|**删除筛选器**|在网格窗格中选择列名，再单击 **“删除筛选器”** 可以删除列的排序条件。|  
|**使用分组依据**|向查询中添加 GROUP BY 功能。|  
|**添加表**|向查询中添加新表。|  
  
 **查询定义**  
 查询定义提供可用来定义和测试查询的工具栏和窗格。  
  
|窗格|Description|  
|----------|-----------------|  
|**“关系图”** 窗格|在关系图中显示查询。 关系图可显示查询中包含的表以及这些表的联接方式。 选中或清除表中某列旁边的复选框，即可在查询输出中添加或删除该列。<br /><br /> 当您向查询添加表时，查询生成器将根据表和表中的键在表之间创建联接。 若要添加联接，请将一个表中的字段拖到另一个表中的字段上。 若要管理联接，请右键单击该联接，再选择菜单选项。<br /><br /> 右键单击“关系图”窗格，可以添加或删除表，选择所有表，以及显示或隐藏窗格。|  
|**“网格”** 窗格|在网格中显示查询。 使用此窗格可以在查询中添加和删除列，以及更改每个列的设置。|  
|**SQL** 窗格|以 SQL 文本的形式显示查询。 在 **“关系图”** 窗格和 **“网格”** 窗格中所做的更改将显示在此窗格中，在此窗格中所做的更改也将显示在 **“关系图”** 窗格和 **“网格”** 窗格中。|  
|**“结果”** 窗格|在您单击工具栏上的 **“运行”** 时显示查询的结果。|  
  
## <a name="see-also"></a>请参阅  
 [执行 SQL 任务](control-flow/execute-sql-task.md)   
 [OLE DB 源](data-flow/ole-db-source.md)   
 [OLE DB 目标](data-flow/ole-db-destination.md)   
 [查找转换](data-flow/transformations/lookup-transformation.md)   
 [Integration Services &#40;SSIS&#41;查询](integration-services-ssis-queries.md)   
 [在 Integration Services 包中执行 MERGE](control-flow/merge-in-integration-services-packages.md)  
  
  
