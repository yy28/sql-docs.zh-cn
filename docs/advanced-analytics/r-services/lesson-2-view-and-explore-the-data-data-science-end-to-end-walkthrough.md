---
title: "第 2 课：查看和浏览数据（数据科学端到端演练） | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: d3835d6d-e68b-486d-81a0-81b717cc6134
caps.latest.revision: 32
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 26
---
# 第 2 课：查看和浏览数据（数据科学端到端演练）
数据浏览是数据建模的重要组成部分，涉及查看要用于分析以及数据可视化的数据对象的汇总。 在本课程中，将同时使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]中的 R 函数浏览数据对象并生成绘图。  
  
然后将使用随 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]安装的包提供的新函数生成绘图，以便直观显示数据。  
  
> [!TIP]  
> 已是 R maestro？  
>   
> 现已下载了所有数据且环境准备就绪，则可以在 RStudio 或任何其他环境中运行完整的 R 脚本并自行浏览功能。 只需打开文件 RSQL_Walkthrough.R，突出显示并运行各个行，或作为演示运行整个脚本。  
>   
> 若要获得 RevoScaleR 函数的其他说明和在 R 中使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据的提示，请继续学习本教程。 它使用完全相同的脚本。  
  
## <a name="verify-downloaded-data-using-sql"></a>使用 SQL 验证已下载的数据  
首先，请花一点时间确定数据已正确加载。  
  
1.  连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
    可以使用多种工具连接和查看 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库。  
  
    -   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]    
    -   Visual Studio 中的服务器资源管理器  
  
2.  展开所创建的数据库。 下图显示了“服务器资源管理器”中的新数据库、表和函数。  
  
    ![new database objects created by script](../../advanced-analytics/r-services/media/rsql-e2e-ssms-newobjects.PNG "new database objects created by script")  
  
3.  还可对数据运行简单查询。 例如，在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，右键单击表并选择“选择前 1000 行”来生成并运行此查询：  
  
    ```  
    SELECT TOP 1000 * FROM [dbo].[nyctaxi_sample]  
    ```  
    如果表中看不到任何数据，请参考上一主题中的[疑难解答](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)部分。
      
4.  若要查看数据的架构和数据类型，可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的系统管理视图。  
  
    ```  
    SELECT TABLE_CATALOG, TABLE_SCHEMA, TABLE_NAME, COLUMN_NAME, COLUMN_DEFAULT  
    FROM [TaxiSample].INFORMATION_SCHEMA.COLUMNS  
    WHERE TABLE_NAME = N'nyctaxi_sample';  
    ```  
  
    > [!TIP]  
    > 若要获取有关如何创建数据表的详细信息，还可以查看脚本 `create-db-tb-upload-data.sql`。  
  
### <a name="generate-summaries-using-sql"></a>使用 SQL 生成汇总  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的优势之一是执行基于集的计算的速度非常快，这使其成为 R 的好助手。  本次演练中，创建表的代码还使用了[列存储索引](../Topic/Columnstore%20Indexes%20Guide.md)来提高计算速度。   
  
```  
SELECT DISTINCT [passenger_count]  
    , ROUND (SUM ([fare_amount]),0) as TotalFares   
    , ROUND (AVG ([fare_amount]),0) as AvgFares  
FROM [dbo].[nyctaxi_sample]  
GROUP BY [passenger_count]   
ORDER BY  AvgFares desc  
```  

下一步中，会使用到 SQL Server 中的数据，并使用 R 生成一些更复杂的汇总以及绘图。  
  
## <a name="next-steps"></a>后续步骤  
[使用 R 查看和汇总数据（数据科学端到端演练）](../../advanced-analytics/r-services/view-and-summarize-data-using-r-data-science-end-to-end-walkthrough.md)  
  
[使用 R 创建图形和绘图（数据科学端到端演练）](../../advanced-analytics/r-services/create-graphs-and-plots-using-r-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>前一课  
[第 1 课：准备数据（数据科学端到端演练）](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)  
  
## <a name="see-also"></a>另请参阅  
[列存储索引指南](../Topic/Columnstore%20Indexes%20Guide.md)  
  
  
  
