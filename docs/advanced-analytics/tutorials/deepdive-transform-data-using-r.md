---
title: 使用 RevoScaleR rxDataStep 转换数据
description: 有关如何在 SQL Server 上使用 R 语言转换数据的教程演练。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: c7d88137994cf5d920462cc4942eb5b632ae3d6e
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344677"
---
# <a name="transform-data-using-r-sql-server-and-revoscaler-tutorial"></a>使用 R 转换数据 (SQL Server 和 RevoScaleR 教程)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本课程是有关如何在 SQL Server 中使用[RevoScaleR 函数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)的[RevoScaleR 教程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)的一部分。

在本课中, 了解用于在分析的各个阶段转换数据的**RevoScaleR**函数。

> [!div class="checklist"]
> * 使用**rxDataStep**创建和转换数据子集
> * 在导入过程中, 使用**rxImport**在 XDF 文件或内存中数据帧之间转换传输内数据

函数 **rxSummary**、 **rxCube**、 **rxLinMod**、 **rxLogit** 虽然不是专门用于数据移动，但都支持数据转换。

## <a name="use-rxdatastep-to-transform-variables"></a>使用 rxDataStep 转换变量

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) 函数一次处理一个数据区块，从一个数据源中读取，并写入另一个数据源。 可以指定要转换的列、要加载的转换等等。

为了使此示例更有趣, 让我们使用其他 R 包中的函数来转换数据。 **引导** 包是一个“建议”包，也就是说， **引导** 包包含在每个 R 分发版中，但是不会在启动时自动加载。 因此, 包应在配置为 R 集成的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例上可用。

从**启动**包中, 使用**logit**, 该函数可计算 logit 的反函数。 也就是说，**inv.logit** 函数将 logit 转换为范围在 [0，1] 之间的概率。

> [!TIP] 
> 获取此范围的预测值的另一种方法是在对 rxPredict  的最初调用中将 type  参数设为 **response**。

1. 首先, `ccScoreOutput`创建一个数据源来保存表的目标数据。
  
    ```R
    sqlOutScoreDS <- RxSqlServerData( table =  "ccScoreOutput",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
2. 添加另一个数据源以保存表`ccScoreOutput2`的数据。
  
    ```R
    sqlOutScoreDS2 <- RxSqlServerData( table =  "ccScoreOutput2",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
    在新表中, 存储上`ccScoreOutput`表中的所有变量, 以及新创建的变量。
  
3. 设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的计算环境。
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. 使用函数**rxSqlServerTableExists**检查输出表`ccScoreOutput2`是否已存在; 如果是这样, 请使用函数**rxSqlServerDropTable**删除该表。
  
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

    定义应用于每一列的转换时，还可指定执行转换所需的任何其他 R 包。  有关可执行的转换类型的详细信息, 请参阅[如何使用 RevoScaleR 转换和子集化数据](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-transform)。
  
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

请注意, 系数变量已作为字符数据写入到`ccScoreOutput2`表中。 若要在后续分析中将它们用作因子，可使用参数 *colInfo* 指定级别。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [使用 rxImport 将数据加载到内存中](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)