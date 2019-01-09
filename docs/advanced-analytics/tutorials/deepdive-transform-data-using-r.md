---
title: 使用 RevoScaleR rxDataStep-SQL Server 机器学习转换数据
description: 有关如何在 SQL Server 上使用 R 语言转换数据的教程演练。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e124825e29392111a453cae0c41b49e8984c9906
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645386"
---
# <a name="transform-data-using-r-sql-server-and-revoscaler-tutorial"></a>使用 R （SQL Server 和 RevoScaleR 教程） 转换数据
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本课程中属于[RevoScaleR 教程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)如何使用[RevoScaleR 函数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)与 SQL Server。

在本课程中，了解**RevoScaleR**函数用于在不同的分析阶段转换数据。

> [!div class="checklist"]
> * 使用**rxDataStep**来创建和转换数据子集
> * 使用**rxImport**来导入过程中转换到或从 XDF 文件或内存中数据帧中传输数据

函数 **rxSummary**、 **rxCube**、 **rxLinMod**、 **rxLogit** 虽然不是专门用于数据移动，但都支持数据转换。

## <a name="use-rxdatastep-to-transform-variables"></a>使用 rxDataStep 转换变量

rxDataStep[](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) 函数一次处理一个数据区块，从一个数据源中读取，并写入另一个数据源。 可以指定要转换的列、要加载的转换等等。

若要使此示例有趣，让我们使用来自另一个 R 包的函数来转换数据。 **引导** 包是一个“建议”包，也就是说， **引导** 包包含在每个 R 分发版中，但是不会在启动时自动加载。 因此，包应可在上找到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例配置为与 R 集成。

从**引导**包，请使用函数**inv.logit**，它可以计算 logit 的反函数。 也就是说，**inv.logit** 函数将 logit 转换为范围在 [0，1] 之间的概率。

> [!TIP] 
> 获取此范围的预测值的另一种方法是在对 rxPredict 的最初调用中将 type 参数设为 **response**。

1. 首先，创建要为表的数据的数据源`ccScoreOutput`。
  
    ```R
    sqlOutScoreDS <- RxSqlServerData( table =  "ccScoreOutput",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
2. 添加另一个数据源以保留表的数据`ccScoreOutput2`。
  
    ```R
    sqlOutScoreDS2 <- RxSqlServerData( table =  "ccScoreOutput2",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
    在新表中，存储从以前的所有变量`ccScoreOutput`表，以及新创建的变量。
  
3. 设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的计算环境。
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. 使用函数**rxSqlServerTableExists**若要检查是否输出表`ccScoreOutput2`已经存在; 并且如果是这样，使用函数**rxSqlServerDropTable**以删除的表。
  
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

    定义应用于每一列的转换时，还可指定执行转换所需的任何其他 R 包。  有关你可以执行的转换类型的详细信息，请参阅[如何使用 RevoScaleR 的转换和子集数据](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-transform)。
  
6. 调用 **rxGetVarInfo** ，在新数据集中查看变量的汇总。
  
```R
rxGetVarInfo(sqlOutScoreDS2)
```

**结果**

```R
Var 1: ccFraudLogitScore, Type: numeric
Var 2: state, Type: character
Var 3: gender, Type: character
Var 4: cardholder, Type: character
Var 5: balance, Type: integer
Var 6: numTrans, Type: integer
Var 7: numIntlTrans, Type: integer
Var 8: creditLine, Type: integer
Var 9: ccFraudProb, Type: numeric
```

原始 logit 分数已保留，但添加了新列 *ccFraudProb*，其中 logit 分数表示介于 0 和 1 之间的值。

请注意，因子变量已写入表`ccScoreOutput2`为字符数据。 若要在后续分析中将它们用作因子，可使用参数 *colInfo* 指定级别。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [使用 rxImport 将数据加载到内存中](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)