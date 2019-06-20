---
title: 将数据加载到内存使用 RevoScaleR rxImport-SQL Server 机器学习
description: 有关如何在 SQL Server 上使用 R 语言加载数据的教程演练。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 5fc29872795623bd0d9e72414a15add92591ec7d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62641388"
---
# <a name="load-data-into-memory-using-rximport-sql-server-and-revoscaler-tutorial"></a>数据加载到内存使用 rxImport （SQL Server 和 RevoScaleR 教程）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本课程中属于[RevoScaleR 教程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)如何使用[RevoScaleR 函数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)与 SQL Server。

[RxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport)函数可用于将数据从数据源移到会话内存中的数据框或 XDF 文件在磁盘上。 如果未指定某个文件作为目标，数据会作为数据框放入内存中。

在此步骤中，了解如何将数据从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，然后使用**rxImport**函数以将所需的数据放入本地文件。 这样一来，就可以在本地计算上下文中重复对数据进行分析，而无需重新查询数据库。

## <a name="extract-a-subset-of-data-from-sql-server-to-local-memory"></a>从 SQL Server 中的数据子集提取到本地内存

您已决定你想要检查的高风险个体将更多详细信息中。 表中的源表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]很大，因此你想要获取只是高风险客户有关的信息。 然后将该数据加载到本地工作站的内存中的数据帧。

1. 将计算上下文重置为本地工作站。

    ```R
    rxSetComputeContext("local")
    ```

2. 如果 sqlQuery  参数中存在效的 SQL 语句，则创建新的 SQL Server 数据源对象。 此示例获取具有最高风险评分的观测值的子集。 这样一来，只有真正需要的数据才会放入本地内存。

    ```R
    sqlServerProbDS \<- RxSqlServerData(
        sqlQuery = paste("SELECT * FROM ccScoreOutput2",
        "WHERE (ccFraudProb > .99)"),
        connectionString = sqlConnString)
    ```

3. 调用函数[rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport)若要在本地 R 会话中将数据读取到数据帧。

    ```R
    highRisk <- rxImport(sqlServerProbDS)
    ```

    如果操作成功，你应看到类似如下的状态消息："读取的行数：35，处理的总行数：35，区块总时间：0.036 秒"

4. 现在，高风险观察均在内存中数据帧中，可以使用各种 R 函数来操纵该数据框。 例如，可以根据风险评分，订单的客户，并打印存在最高风险的客户的列表。

    ```R
    orderedHighRisk <- highRisk[order(-highRisk$ccFraudProb),]
    row.names(orderedHighRisk) <- NULL
    head(orderedHighRisk)
    ```

**结果**

```R
ccFraudLogitScore   state gender cardholder balance numTrans numIntlTrans creditLine ccFraudProb1
9.786345    SD   Male  Principal   23456       25            5 75   0.99994382
9.433040    FL Female  Principal   20629       24           28 75   0.99992003
8.556785    NY Female  Principal   19064       82           53 43   0.99980784
8.188668    AZ Female  Principal   19948       29            0 75   0.99972235
7.551699    NY Female  Principal   11051       95            0 75   0.99947516
7.335080    NV   Male  Principal   21566        4            6  75   0.9993482
```

## <a name="more-about-rximport"></a>详细了解 rxImport

不仅可以使用 rxImport  来移动数据，还可在读取它的过程中转换数据。 例如，可以为固定宽度的列指定字符数，提供变量的说明，设置因子列的级别，甚至还能创建可在导入后使用的新级别。

**RxImport**函数在导入过程中，将变量名称分配到的列，但可以通过使用指示新变量名称*colInfo*参数或更改数据类型使用*colClasses*参数。

通过在 *transforms* 参数中指定其他操作，可以对读取的每个数据区块执行基本处理。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [使用 rxDataStep 创建新的 SQL Server 表](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)