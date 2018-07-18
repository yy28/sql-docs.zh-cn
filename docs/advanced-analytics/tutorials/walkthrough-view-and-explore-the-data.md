---
title: 查看和浏览数据使用 SQL （演练） |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b933337c1234f09f0a8963c1979a86a9ab61db53
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
ms.locfileid: "31201729"
---
# <a name="view-and-explore-the-data-using-sql-walkthrough"></a>查看和浏览使用 SQL （演练） 的数据
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

数据浏览是数据建模的重要组成部分，涉及查看要用于分析以及数据可视化的数据对象的汇总。 在本课程中，你浏览数据对象和生成图形，同时使用[!INCLUDE[tsql](../../includes/tsql-md.md)]和 R 函数纳入[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。

然后生成图来可视化数据，使用与安装的包提供的新函数[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。

> [!TIP]
> 已是 R maestro？
>   
> 现已下载了所有数据且环境准备就绪，则可以在 RStudio 或任何其他环境中运行完整的 R 脚本并自行浏览功能。 只需打开文件 RSQL_Walkthrough.R，突出显示并运行各个行，或作为演示运行整个脚本。
>   
> 若要获得 RevoScaleR 函数的其他说明和在 R 中使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据的提示，请继续学习本教程。 它使用完全相同的脚本。

## <a name="verify-downloaded-data-using-sql-server"></a>验证下载的数据使用 SQL Server

首先，请花一点时间确定数据已正确加载。

1. 连接到你[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例使用你最喜欢的数据库的管理工具，如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，在 Visual Studio 或 Visual Studio 代码中的服务器资源管理器。

2. 选择你创建，并展开以查看新的数据库、 表和函数的数据库。
  
    ![rsql_e2e_ssms_newobjects](media/rsql-e2e-ssms-newobjects.PNG)
  
3.  若要验证数据正确加载，右键单击的表，然后选择**选择前 1000年行**。 菜单选项运行此查询：

    ```SQL
    SELECT TOP 1000 * FROM [dbo].[nyctaxi_sample]
    ```
    如果表中看不到任何数据，请参考上一主题中的 [疑难解答](walkthrough-prepare-the-data.md) 部分。

4. 此数据表已通过添加[列存储索引](../../relational-databases/indexes/columnstore-indexes-overview.md)针对基于集的计算进行了优化。 运行此语句，以生成对表的快速摘要。

    ```SQL
    SELECT DISTINCT [passenger_count]
        , ROUND (SUM ([fare_amount]),0) as TotalFares
        , ROUND (AVG ([fare_amount]),0) as AvgFares
    FROM [dbo].[nyctaxi_sample]
    GROUP BY [passenger_count]
    ORDER BY  AvgFares DESC
    ````
    在下一课中，将使用 R 生成一些更复杂的摘要。

## <a name="next-lesson"></a>下一课

[使用 R 汇总数据](walkthrough-view-and-summarize-data-using-r.md)

## <a name="previous-lesson"></a>上一课

[准备使用 PowerShell 的数据](walkthrough-prepare-the-data.md)
