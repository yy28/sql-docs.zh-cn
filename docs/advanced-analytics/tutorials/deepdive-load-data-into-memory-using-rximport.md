---
title: 使用 RevoScaleR rxImport 将数据加载到内存中
description: 有关如何使用 R 语言在 SQL Server 上加载数据的教程演练。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0e498e2aff0f6c21d11e4c34439301f36119257f
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714926"
---
# <a name="load-data-into-memory-using-rximport-sql-server-and-revoscaler-tutorial"></a>使用 rxImport 将数据加载到内存中 (SQL Server 和 RevoScaleR 教程)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本课程是有关如何在 SQL Server 中使用[RevoScaleR 函数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)的[RevoScaleR 教程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)的一部分。

[RxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport)函数可用于将数据从数据源移到会话内存中的数据帧或磁盘上的 XDF 文件中。 如果未指定某个文件作为目标，数据会作为数据框放入内存中。

在此步骤中, 你将了解如何从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]获取数据, 然后使用**rxImport**函数将感兴趣的数据放入本地文件中。 这样一来，就可以在本地计算上下文中重复对数据进行分析，而无需重新查询数据库。

## <a name="extract-a-subset-of-data-from-sql-server-to-local-memory"></a>将数据的子集从 SQL Server 提取到本地内存中

你已经决定要更详细地检查高风险个人。 源表中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的源表很大, 只需获取有关高风险客户的信息。 然后, 将该数据加载到本地工作站的内存中的数据帧中。

1. 将计算上下文重置为本地工作站。

    ```R
    rxSetComputeContext("local")
    ```

2. 如果 sqlQuery 参数中存在效的 SQL 语句，则创建新的 SQL Server 数据源对象。 此示例获取具有最高风险评分的观测值的子集。 这样一来，只有真正需要的数据才会放入本地内存。

    ```R
    sqlServerProbDS \<- RxSqlServerData(
        sqlQuery = paste("SELECT * FROM ccScoreOutput2",
        "WHERE (ccFraudProb > .99)"),
        connectionString = sqlConnString)
    ```

3. 调用函数[rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport)将数据读入本地 R 会话中的数据帧。

    ```R
    highRisk <- rxImport(sqlServerProbDS)
    ```

    如果操作成功, 你应该会看到如下所示的状态消息:"读取的行:35, 处理的总行数:35, 总区块时间:0.036 秒 "

4. 由于高风险观测值已在内存中数据帧中, 因此可以使用各种 R 函数来操作数据帧。 例如, 你可以按风险评分对客户排序, 并打印出风险最高的客户的列表。

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

不仅可以使用 rxImport 来移动数据，还可在读取它的过程中转换数据。 例如，可以为固定宽度的列指定字符数，提供变量的说明，设置因子列的级别，甚至还能创建可在导入后使用的新级别。

在导入过程中, **rxImport**函数将变量名称赋给列, 但可以使用*colInfo*参数指示新变量名称, 或使用*colClasses*参数更改数据类型。

通过在 *transforms* 参数中指定其他操作，可以对读取的每个数据区块执行基本处理。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [使用 rxDataStep 创建新的 SQL Server 表](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)