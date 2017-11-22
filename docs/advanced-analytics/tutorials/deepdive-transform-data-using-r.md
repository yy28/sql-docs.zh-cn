---
title: "转换使用 R 数据 |Microsoft 文档"
ms.custom: SQL2016_New_Updated
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 0327e788-94cc-4a47-933b-7c5c027b9208
caps.latest.revision: "19"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 24f37dd048f9eb7f8bb872515958006874a9b3a7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="transform-data-using-r"></a>转换数据使用 R

**RevoScaleR** 包提供了用于在不同的分析阶段转换数据的多个函数：

- **rxDataStep** 可用于创建和转换数据的子集。

- **rxImport** 支持在 XDF 文件或内存中数据帧中导入或导出数据时转换数据。

- 函数 **rxSummary**、 **rxCube**、 **rxLinMod**、 **rxLogit** 虽然不是专门用于数据移动，但都支持数据转换。

在本部分中，将学习如何使用这些函数。 让我们从 rxDataStep 开始。

## <a name="use-rxdatastep-to-transform-variables"></a>使用 rxDataStep 转换变量

RxDataStep 函数处理一次，从一个数据源读取和写入到另一个块区的数据。 可以指定要转换的列、要加载的转换等等。

若要使本示例有趣，可以使用另一个 R 包中的函数来转换数据。  **引导** 包是一个“建议”包，也就是说， **引导** 包包含在每个 R 分发版中，但是不会在启动时自动加载。 因此，在和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 结合使用的 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]实例中此包应是可用的。

在 **引导** 包中，使用函数 `inv.logit`，它可以计算 logit 的反函数。 也就是说， `inv.logit` 函数将 logit 转换为范围在 [0，1] 之间的概率。

> [!TIP] 
> 在此规模下获取预测另一种方法是设置*类型*参数**响应**rxPredict 原始调用中。

1. 首先创建用于承载表 ccScoreOutput 的数据的数据源。
  
    ```R
    sqlOutScoreDS <- RxSqlServerData( table =  "ccScoreOutput",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
2. 添加另一个用于承载表 ccScoreOutput2 的数据的数据源。
  
    ```R
    sqlOutScoreDS2 <- RxSqlServerData( table =  "ccScoreOutput2",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
    在新表中，可获取之前的 ccScoreOutput 表中的所有变量，以及新创建的变量。
  
3. 设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的计算环境。
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. 使用函数 rxSqlServerTableExists 来检查是否输出表*ccScoreOutput2*已存在; 并且如果是，使用函数 rxSqlServerDropTable 可以删除该表。
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput2"))     rxSqlServerDropTable("ccScoreOutput2")
    ```
  
5. 调用 rxDataStep 函数，并在列表中指定所需的转换。
  
    ```R
    rxDataStep(inData = sqlOutScoreDS,
        outFile = sqlOutScoreDS2,
        transforms = list(ccFraudProb = inv.logit(ccFraudLogitScore)),
        transformPackages = "boot",
        overwrite = TRUE)
    ```

    定义应用于每一列的转换时，还可指定执行转换所需的任何其他 R 包。  有关可执行的转换类型的详细信息，请参阅  [转换数据和创建数据子集](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-transform)
  
6. 调用 rxGetVarInfo 若要在新的数据集中查看变量的摘要。
  
    ```R
    rxGetVarInfo(sqlOutScoreDS2)
    ```

    **结果**
    
    *Var 1: ccFraudLogitScore, Type: numeric*
    
    *Var 2: state, Type: character*
    
    *Var 3: gender, Type: character*
    
    *Var 4: cardholder, Type: character*
    
    *Var 5: balance, Type: integer*
    
    *Var 6: numTrans, Type: integer*
    
    *Var 7: numIntlTrans, Type: integer*
    
    *Var 8: creditLine, Type: integer*
    
    *Var 9: ccFraudProb, Type: numeric*

原始 logit 分数已保留，但添加了新列 *ccFraudProb*，其中 logit 分数表示介于 0 和 1 之间的值。

请注意，因子变量已作为字符数据写入表 *ccScoreOutput2* 。  若要在后续分析中将它们用作因子，可使用参数 *colInfo* 指定级别。

## <a name="next-step"></a>下一步

[将数据加载到内存中用 rxImport](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)

## <a name="previous-step"></a>上一步

[创建和运行 R 脚本](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
