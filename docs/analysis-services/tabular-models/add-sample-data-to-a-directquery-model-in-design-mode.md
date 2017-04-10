---
title: "在设计模式下将示例数据添加到 DirectQuery 模型中 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1af1e823-85aa-4319-a93f-98b35f7c7322
caps.latest.revision: 9
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 9
---
# 在设计模式下将示例数据添加到 DirectQuery 模型中
 在 DirectQuery 模式下，表分区用于创建在模型设计过程中使用的示例数据子集或创建完整数据视图的替代。
 
 部署 DirectQuery 表格模型时，每个表只允许有一个分区，并且该分区必须是完整数据视图。 所有其他分区要么是完整数据视图的替代，要么是示例数据。 在本主题中，我们将介绍使用数据子集创建示例分区。
 
 默认情况下，在 SSDT 中的 DirectQuery 模式下的设计表格模型时，模型的工作数据库不包含任何数据。 每个表都有一个默认分区，此分区会将所有查询都定向到数据源。 
  
但是，可以在设计时将较少量的示例数据添加到模型的工作数据库以供使用。 通过仅在设计中使用的示例分区查询指定示例数据。 它随模型一起在内存中进行缓存。 这有助于根据自己的意愿验证建模决策，而不会影响数据源。 在 SQL Server Data Tools (SSDT) 中使用“在 Excel 中分析”时，可以使用示例数据集测试建模决策，或从连接到工作区数据集的其他客户端应用程序进行测试。  
  
> [!TIP]  
>  即使在空模型的 DirectQuery 模式下，也始终都能查看每个表的小型内置行集。 在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中，请单击“表” > “表属性”来查看 50 行的数据集。  
  
## 创建示例分区
 这些说明适用于在兼容级别 1200 上创建表格模型或将其升级到该级别。 较低兼容性级别的模型使用不同的属性来获取缓存数据。 有关属性说明，请参阅[在 SSMS 中启用 DirectQuery 模式](../../analysis-services/tabular-models/enable-directquery-mode-in-ssms.md)。  
  
1.  在 SQL Server Data Tools 中，请在关系图或数据视图中单击事实数据表以打开其属性页。 事实数据表提供模型中聚合的数值数据和度量值。 你可以具有多个事实数据表。  
  
2.  单击“表” > “属性”以打开“分区管理”对话框。  
  
    请注意，默认分区是“(直接查询) \<表名>”。 这是完整数据视图。 不要删除此分区。 部署模型时会使用此分区。  
  
4.  选择分区，然后单击“复制”。  

    这会创建默认分区的副本，但是，此副本会包含在查询中指定的示例数据。 例如：
  
     ![ssas_tabularproject_copypartition](../../analysis-services/tabular-models/media/ssas-tabularproject-copypartition.jpg "ssas_tabularproject_copypartition")  
  
5.  选择复制的分区，然后单击“SQL 查询编辑器”按钮以添加筛选器。 在创作模型时减少示例数据大小。 例如，如果从 AdventureWorksDW 中选择了 **FactInternetSales**，则筛选器的外观可能如下所示：  
  
    ```  
    SELECT [dbo].[FactInternetSales].* FROM [dbo].[FactInternetSales]  
    JOIN DimSalesTerritory as ST  
    ON ST.SalesTerritoryKey = FactInternetSales.SalesTerritoryKey  
    WHERE ST.SalesTerritoryGroup='North America';  
    ```  
  
6.  单击“验证”  以检查有无语法错误。  
  
     请注意，在 DirectQuery 模式下，除了“分区”对话框中的“新建”、“复制”和“删除”按钮外，还有一个切换按钮，可交替显示为“设置为示例”和“设置为 DirectQuery”。  
  
     只有一个分区可以是 DirectQuery 分区。 可以通过选择为表定义的分区并单击“设置为示例”来进行控制。  
  
7.  处理表。  
  


  
  