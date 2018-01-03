---
title: "分析本地计算上下文 （SQL 和 R 深入） 中的数据 |Microsoft 文档"
ms.date: 12/18/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs: R
ms.assetid: 787bb526-4a13-40fa-9343-75d3bf5ba6a2
caps.latest.revision: "13"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: e65a4ad3018cfec6b60dae605945a8641b568c5d
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2017
---
# <a name="analyze-data-in-local-compute-context-sql-and-r-deep-dive"></a>分析本地计算上下文 （SQL 和 R 深入） 中的数据

本文是有关如何使用数据科学深入了解教程的一部分[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)与 SQL Server。

在本部分中，你将了解如何切换回本地计算上下文，并将数据移上下文来优化性能之间。

尽管 i 可能更快地是，若要运行使用服务器上下文的复杂 R 代码，有时很更方便地获取你的数据外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和在本地工作站上对其进行分析。

## <a name="create-a-local-summary"></a>创建本地摘要

1. 更改计算上下文，以在本地完成所有工作。
  
    ```R
    rxSetComputeContext ("local")
    ```
  
2. 从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提取数据时，通常可以通过增加每次读取所提取的行数获得更好的性能。  若要执行此操作，在数据源上增加 rowsPerRead 参数的值。 之前，rowsPerRead 的值设置为 5000。
  
    ```R
    sqlServerDS1 <- RxSqlServerData(
       connectionString = sqlConnString,
       table = sqlFraudTable,
       colInfo = ccColInfo,
       rowsPerRead = 10000)
    ```

3. 调用**rxSummary**上新数据源。
  
    ```R
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)
    ```
  
    实际结果应与在 **计算机的上下文中运行** rxSummary [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的结果相同。  但是，该操作可能更快，也可能更慢。 因为正在将数据传输到本地计算机进行分析，因此操作很大程度取决于数据库的连接。

## <a name="next-step"></a>下一步

[SQL Server 和 XDF 文件之间移动数据](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)

## <a name="previous-step"></a>上一步

[使用 rxDataStep 执行区块分析](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)
