---
title: "查询和修改 SQL Server 数据 |Microsoft 文档"
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
ms.assetid: 8c7007a9-9a8f-4dcd-8068-40060d4f6444
caps.latest.revision: 17
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4970a681733d8920b9eef6b27023f9ae1c7ce981
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="query-and-modify-the-sql-server-data"></a>查询和修改 SQL Server 数据

数据现已加载到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，可以使用创建的数据源作为 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]中 R 函数的参数，来获取有关变量的基本信息，以及生成摘要和直方图。

在此步骤中，你将重新使用的数据源进行一些快速分析和然后增强数据。

## <a name="query-the-data"></a>查询数据

首先，获取列及其数据类型的列表。

1.  使用函数**rxGetVarInfo**并指定你想要分析的数据源。
  
    ```R
    rxGetVarInfo(data = sqlFraudDS)
    ```

    **结果**
    
    *Var 1: custID, Type: integer*
    
    *Var 2: gender, Type: integer*
    
    *Var 3: state, Type: integer*
    
    *Var 4: cardholder, Type: integer*
    
    *Var 5: balance, Type: integer*
    
    *Var 6: numTrans, Type: integer*
    
    *Var 7: numIntlTrans, Type: integer*
    
    *Var 8: creditLine, Type: integer*
    
    *Var 9: fraudRisk, Type: integer*


## <a name="modify-metadata"></a>修改元数据

所有变量都作为整数存储，但某些变量表示分类数据（在 R 中称为因子变量）。例如，“state”列包含用作 50 个州以及哥伦比亚特区的标识符的数字。  为了更加轻松地理解数据，可将数字替换为州名的缩写列表。

在此步骤中，要提供包含缩写的字符串矢量，然后将这些分类数据映射到原始整数标识符。 此变量准备就绪后，可将其用于 colInfo 参数，以指定将此列作为因子处理。 此后，每当分析或导入该数据时，都将使用这些缩写并将该列作为因子处理。

1. 从创建一个 R 变量 stateAbb 开始，并定义要添加到其中的字符串的矢量，如下所示：
  
    ```R
    stateAbb <- c("AK", "AL", "AR", "AZ", "CA", "CO", "CT", "DC",
        "DE", "FL", "GA", "HI","IA", "ID", "IL", "IN", "KS", "KY", "LA",
        "MA", "MD", "ME", "MI", "MN", "MO", "MS", "MT", "NB", "NC", "ND",
        "NH", "NJ", "NM", "NV", "NY", "OH", "OK", "OR", "PA", "RI","SC",
        "SD", "TN", "TX", "UT", "VA", "VT", "WA", "WI", "WV", "WY")
    ```

2. 接下来，创建名为 ccColInfo 的列信息对象，该对象指定现有整数值到分类级别（州名的缩写）的映射。
  
    此语句还为 gender 和 cardholder 创建因子变量。
  
    ```R
    ccColInfo <- list(
    gender = list(
              type = "factor",
              levels = c("1", "2"),
              newLevels = c("Male", "Female")
              ),
    cardholder = list(
                  type = "factor",
                  levels = c("1", "2"),
                  newLevels = c("Principal", "Secondary")
                   ),
    state = list(
             type = "factor",
             levels = as.character(1:51),
             newLevels = stateAbb
             ),
    balance = list(type = "numeric")
    )
    ```
  
3. 若要创建使用已更新数据的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据源，可像先前一样调用 RxSqlServerData 函数，但需添加 colInfo 参数。
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
    table = sqlFraudTable, colInfo = ccColInfo,
    rowsPerRead = sqlRowsPerRead)
    ```
  
    - 对于 table 参数，可传入变量 sqlFraudTable，其中包含之前创建的数据源。
    - 对于 colInfo 参数，可传入 ccColInfo 变量，其中包含列数据类型和因子级别。
    - 将列作为用作因子前将其映射到缩写也可真正提高性能。 有关详细信息，请参阅 [R 和数据优化](https://msdn.microsoft.com/library/mt723575.aspx)
  
4.  你现在可以使用函数 rxGetVarInfo 查看新的数据源中的变量。
  
    ```R
    rxGetVarInfo(data = sqlFraudDS)
    ```

    **结果**
    
    *Var 1: custID, Type: integer*
    
    *Var 2： 性别 2 因素级别： 男性女性*
    
    *Var 3： 状态 51 因素级别： AK AL AR AZ CA...VT WA WI WV WY*
    
    *Var 4： 持卡人 2 因素级别： 主体辅助数据库*
    
    *Var 5: balance, Type: integer*
    
    *Var 6: numTrans, Type: integer*
    
    *Var 7: numIntlTrans, Type: integer*
    
    *Var 8: creditLine, Type: integer*
    
    *Var 9: fraudRisk, Type: integer*

现在，指定的三个变量（_gender_、 _state_和 _cardholder_）将被视为因子。

## <a name="next-step"></a>下一步

[定义和使用计算上下文](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)

## <a name="previous-step"></a>上一步

[使用 RxSqlServerData 创建 SQL Server 数据对象](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)




