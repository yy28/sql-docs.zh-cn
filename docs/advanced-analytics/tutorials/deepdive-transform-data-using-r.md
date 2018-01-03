---
title: "转换数据使用 R （SQL 和 R 深入） |Microsoft 文档"
ms.date: 12/24/2017
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
ms.assetid: 0327e788-94cc-4a47-933b-7c5c027b9208
caps.latest.revision: "19"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: b55b2a0ae152cc0fb00d21a7c1221bc3dcdcbcc7
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2017
---
# <a name="transform-data-using-r-sql-and-r-deep-dive"></a>转换使用 R （SQL 和 R 深入） 的数据

本文是有关如何使用数据科学深入了解教程的一部分[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)与 SQL Server。

**RevoScaleR** 包提供了用于在不同的分析阶段转换数据的多个函数：

- **rxDataStep** 可用于创建和转换数据的子集。

- **rxImport** 支持在 XDF 文件或内存中数据帧中导入或导出数据时转换数据。

- 函数 **rxSummary**、 **rxCube**、 **rxLinMod**、 **rxLogit** 虽然不是专门用于数据移动，但都支持数据转换。

在本部分中，你将了解如何使用这些函数。 让我们开始[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep)。

## <a name="use-rxdatastep-to-transform-variables"></a>使用 rxDataStep 转换变量

rxDataStep 函数一次处理一个数据区块，从一个数据源中读取，并写入另一个数据源。 可以指定要转换的列、要加载的转换等等。

若要使此示例更加有趣，让我们使用来自另一个的 R 包的函数来转换数据。  **引导** 包是一个“建议”包，也就是说， **引导** 包包含在每个 R 分发版中，但是不会在启动时自动加载。 因此，在和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 结合使用的 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]实例中此包应是可用的。

从**启动**包，请使用函数`inv.logit`，其计算的 logit 的反向属性。 也就是说， `inv.logit` 函数将 logit 转换为范围在 [0，1] 之间的概率。

> [!TIP] 
> 在此规模下获取预测另一种方法是设置*类型*参数**响应**rxPredict 原始调用中。

1. 通过创建数据源，以保存数据发送到表中，启动`ccScoreOutput`。
  
    ```R
    sqlOutScoreDS <- RxSqlServerData( table =  "ccScoreOutput",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
2. 添加另一个数据源，以保存表数据`ccScoreOutput2`。
  
    ```R
    sqlOutScoreDS2 <- RxSqlServerData( table =  "ccScoreOutput2",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
    在新的表中，将存储从以前的所有变量`ccScoreOutput`表，加上新创建的变量。
  
3. 设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的计算环境。
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. 使用函数**rxSqlServerTableExists**以检查是否输出表`ccScoreOutput2`已存在; 并且如果是这样，使用函数**rxSqlServerDropTable**可以删除该表。
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput2"))     rxSqlServerDropTable("ccScoreOutput2")
    ```
  
5. 调用 **rxDataStep** 函数，并在列表中指定所需的转换。
  
    ```R
    rxDataStep(inData = sqlOutScoreDS,
        outFile = sqlOutScoreDS2,
        transforms = list(ccFraudProb = inv.logit(ccFraudLogitScore)),
        transformPackages = "boot",
        overwrite = TRUE)
    ```

    定义应用于每一列的转换时，还可指定执行转换所需的任何其他 R 包。  有关你可以执行的转换的类型的详细信息，请参阅[如何转换和子集的数据使用 RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-transform)。
  
6. 调用 **rxGetVarInfo** ，在新数据集中查看变量的汇总。
  
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

请注意，因素变量已写入表`ccScoreOutput2`为字符数据。 若要在后续分析中将它们用作因子，可使用参数 *colInfo* 指定级别。

## <a name="next-step"></a>下一步

[使用 rxImport 将数据加载到内存中](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)

## <a name="previous-step"></a>上一步

[创建并运行 R 脚本](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
