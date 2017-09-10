---
title: "将数据加载到内存中用 rxImport |Microsoft 文档"
ms.custom: 
ms.date: 05/18/2017
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
ms.assetid: 47a42e9a-05a0-4a50-871d-de73253cf070
caps.latest.revision: 14
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bfea2db1797638da671cb59ffc4cd4954d145199
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="load-data-into-memory-using-rximport"></a>使用 rxImport 将数据加载到内存中

rxImport 函数可用于将数据从数据源移到 R 会话内存的数据框或磁盘中的 XDF 文件。 如果未指定某个文件作为目标，数据会作为数据框放入内存中。

在此步骤中，你将学习如何将数据从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，然后使用 rxImport 函数将感兴趣的数据放入本地文件。 这样一来，就可以在本地计算上下文中重复对数据进行分析，而无需重新查询数据库。

## <a name="extract-a-subset-of-data-from-sql-server-to-local-memory"></a>从 SQL Server 将数据子集提取到本地内存

你已决定仅详细检查高风险个体。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的源表很大，因此仅获取与高风险客户有关的信息，然后将这些信息加载到本地工作站的内存中的数据框内。

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

3. 使用函数 rxImport 可实际上将数据加载到本地 R 会话中的数据框。

    ```R
    highRisk <- rxImport(sqlServerProbDS)
    ```

    如果该操作成功，应看到一条状态消息：读取的行数：35，处理的总行数：35，区块总时间：0.036 秒

4. 现在，内存中的某个数据框内已拥有高风险观察数据，可使用各种 R 函数来操纵该数据框。 例如，可根据风险评分对客户排序，并打印存在最高风险的客户。

    ```R
    orderedHighRisk <- highRisk[order(-highRisk$ccFraudProb),]
    row.names(orderedHighRisk) <- NULL
    head(orderedHighRisk)
    ```

**结果**

*ccFraudLogitScore   state gender cardholder balance numTrans numIntlTrans creditLine ccFraudProb1*

*9.786345    SD   Male  Principal   23456       25            5 75   0.99994382*

*9.433040    FL Female  Principal   20629       24           28 75   0.99992003*

*8.556785    NY Female  Principal   19064       82           53 43   0.99980784*

*8.188668    AZ Female  Principal   19948       29            0 75   0.99972235*

*7.551699    NY Female  Principal   11051       95            0 75   0.99947516*

*7.335080    NV   Male  Principal   21566        4            6  75   0.9993482*

## <a name="more-about-rximport"></a>详细了解 rxImport

你可以使用 rxImport，而不仅仅是来移动数据，但以转换过程中读取的数据。 例如，可以为固定宽度的列指定字符数，提供变量的说明，设置因子列的级别，甚至还能创建可在导入后使用的新级别。

RxImport 函数导入过程中，将变量名分配到的列，但你可以通过使用来表示新变量名*colInfo*参数，并可更改数据类型使用*colClasses*参数。

通过在 *transforms* 参数中指定其他操作，可以对读取的每个数据区块执行基本处理。

## <a name="next-step"></a>下一步

[创建新的 SQL Server 表使用 rxDataStep](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)

## <a name="previous-step"></a>上一步

[转换数据使用 R](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)

## <a name="see-also"></a>另请参阅

[机器学习教程](../../advanced-analytics/tutorials/machine-learning-services-tutorials.md)


