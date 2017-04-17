---
title: "第 2 课：查看和浏览数据（数据科学端到端演练）| Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: d3835d6d-e68b-486d-81a0-81b717cc6134
caps.latest.revision: 32
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a51901c29fc34c119a589694fa9a5d76e9067b57
ms.lasthandoff: 04/11/2017

---
# <a name="lesson-2-view-and-explore-the-data-data-science-end-to-end-walkthrough"></a>第 2 课：查看和浏览数据（数据科学端到端演练）
数据浏览是数据建模的重要组成部分，涉及查看要用于分析以及数据可视化的数据对象的汇总。 在本课程中，将同时使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]中的 R 函数浏览数据对象并生成绘图。  
  
然后将使用随 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]安装的包提供的新函数生成绘图，以便直观显示数据。  
  
> [!TIP]  
> 已是 R maestro？  
>   
> 现已下载了所有数据且环境准备就绪，则可以在 RStudio 或任何其他环境中运行完整的 R 脚本并自行浏览功能。 只需打开文件 RSQL_Walkthrough.R，突出显示并运行各个行，或作为演示运行整个脚本。  
>   
> 若要获得 RevoScaleR 函数的其他说明和在 R 中使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据的提示，请继续学习本教程。 它使用完全相同的脚本。  
  
## <a name="verify--downloaded-data-using-sql-server"></a>使用 SQL Server 验证已下载的数据 

首先，请花一点时间确定数据已正确加载。  
  
1.  使用你最喜欢的数据库管理工具（如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Visual Studio 中的服务器资源管理器或 VS Code）连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
2.  单击所创建的数据库，并展开以查看新的数据库、表和函数  
  
    ![rsql_e2e_ssms_newobjects](../../advanced-analytics/r-services/media/rsql-e2e-ssms-newobjects.PNG) 
  
3.  若要验证是否已正确加载数据，请右键单击表并选择“Select top 1000 rows”来运行此查询：  
  
    ```  
    SELECT TOP 1000 * FROM [dbo].[nyctaxi_sample]  
    ```  
    如果表中看不到任何数据，请参考上一主题中的 [疑难解答](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md) 部分。
      
4.  此数据表已通过添加[列存储索引](../../relational-databases/indexes/columnstore-indexes-overview.md)针对基于集的计算进行了优化。 有关如何完成该操作的详细信息，请查看用于创建该表的脚本 `create-db-tb-upload-data.sql`

    现在，运行此语句，以生成该表的快速摘要。    
  
    ````  
    SELECT DISTINCT [passenger_count]  
        , ROUND (SUM ([fare_amount]),0) as TotalFares   
        , ROUND (AVG ([fare_amount]),0) as AvgFares  
    FROM [dbo].[nyctaxi_sample]  
    GROUP BY [passenger_count]   
    ORDER BY  AvgFares DESC  
    ````
    在下一课中，将使用 R 生成一些更复杂的摘要。
 
## <a name="next-steps"></a>后续步骤  
[使用 R 查看和汇总数据（数据科学端到端演练）](../../advanced-analytics/r-services/lesson-2-1-view-and-summarize-data-using-r.md)  
  
[使用 R 创建图形和绘图（数据科学端到端演练）](../../advanced-analytics/r-services/lesson-2-2-create-graphs-and-plots-using-r.md)  
  
## <a name="previous-lesson"></a>前一课  
[第 1 课：准备数据（数据科学端到端演练）](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)  
  
## <a name="see-also"></a>另请参阅  
[列存储索引指南](../../relational-databases/indexes/columnstore-indexes-overview.md)  
  
  
  


