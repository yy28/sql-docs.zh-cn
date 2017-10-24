---
title: "保存和加载使用 ODBC 的 SQL Server 中的 R 对象 |Microsoft 文档"
ms.custom: 
ms.date: 08/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 6ac2e971-6b4f-4c73-ba57-29c716abd057
caps.latest.revision: 8
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e0fb31629dc6fd691fdac257a65cccc3728cc403
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="save-and-load-r-objects-from-sql-server-using-odbc"></a>保存和加载使用 ODBC 的 SQL Server 中的 R 对象

SQL Server R Services 可将序列化的 R 对象存储在表中，然后根据需要从表中加载对象，无需重新运行 R 代码或重新定型模型。 对于一些情况来说（例如，定型并保存模型，稍后用于评分或分析），将 R 对象保存到数据库这一功能十分关键。

为了提高此关键步骤的性能， **RevoScaleR** 包现在包括新的序列化和反序列化函数，可极大地改善性能，并且更简洁地存储对象。 本文介绍了这些函数以及如何使用它们。

## <a name="overview"></a>概述

**RevoScaleR** 包现在包括新函数，让它可更加轻松地将 R 对象保存到 SQL Server，然后从 SQL Server 表中读取对象。 通常情况下，每个函数调用使用简单的键值存储区，其中键是对象的名称，而与键关联的值是要移入或移出表的 varbinary R 对象。

若要直接从 R 环境将 R 对象保存到 SQL Server，你必须：

+ 建立与 SQL Server 使用的连接*RxOdbcData*数据源。
+ 新的函数调用通过 ODBC 连接
+ 或者，你可以指定不序列对象。 然后，选择新的压缩算法来代替默认的压缩算法。

默认情况下，从 R 调用以移动到 SQL Server 的任何对象都将进行序列化和压缩。 相反，从 SQL Server 表加载某对象以便在 R 代码中使用时，该对象将进行反序列化和解压。

## <a name="list-of-new-functions"></a>新的函数的列表

- `rxWriteObject` 使用 ODBC 数据源将 R 对象写入 SQL Server。

- `rxReadObject` 使用 ODBC 数据源从 SQL Server 数据库读取 R 对象

- `rxDeleteObject` 从 ODBC 数据源中指定的 SQL Server 数据库中删除 R 对象。 如果存在多个由键/版本组合标识的对象，则将删除所有对象。

- `rxListKeys` 以键/值对的方式列出所有可用对象。 这有助于确定 R 对象的名称和版本。

有关每个函数语法的详细帮助，请使用 R 帮助。 详细信息也会出现在[ScaleR 引用](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)。

## <a name="how-to-store-r-objects-in-sql-server-using-odbc"></a>如何使用 ODBC 在 SQL Server 中存储 R 对象

此过程说明如何使用新函数创建模型并将其保存到 SQL Server。

1. 为 SQL Server 设置连接字符串。
   ```R
   conStr <- 'Driver={SQL Server};Server=localhost;Database=storedb;Trusted_Connection=true'
   ```
2. 使用连接字符串在 R 中创建 *rxOdbcData* 数据源对象。
   ```R
   ds <- RxOdbcData(table="robjects", connectionString=conStr)
   ```

3. 如果已存在表，请将其删除，无需跟踪旧版本的对象。

   ```R
   if(rxSqlServerTableExists(ds@table, ds@connectionString)) {
       rxSqlServerDropTable(ds@table, ds@connectionString)
       }
   ```
   
4. 定义可用于存储二进制对象的表。

   ```R
   ddl <- paste(" CREATE TABLE [", ds@table, "] 
      (","  [id] varchar(200) NOT NULL,
       "," [value] varbinary(max),
       "," CONSTRAINT unique_id UNIQUE (id))", 
       sep = "") 
   ```
5. 打开 ODBC 连接以创建表，DDL 语句完成之后，关闭连接。

   ```R
    rxOpen(ds, "w") 
    rxExecuteSQLDDL(ds, ddl) 
    rxClose(ds)
    ```
6. 生成要存储的 R 对象。

   ```R
   infertLogit <- rxLogit(case ~ age + parity + education + spontaneous + induced, 
     data = infert)
   ```
6. 使用之前创建的 *RxOdbcData* 对象，将模型保存到数据库。

   ```R
   rxWriteObject(ds, "logit.model", infertLogit)
   ```

## <a name="how-to-read-r-objects-from-sql-server-using-odbc"></a>如何使用 ODBC 从 SQL Server 读取 R 对象

此过程说明如何使用新函数从 SQL Server 中加载模型。

1. 为 SQL Server 设置连接字符串。

   ```R
   conStr2 <- 'Driver={SQL Server};Server=localhost;Database=storedb;Trusted_Connection=true'
   ```
2. 使用连接字符串在 R 中创建 *rxOdbcData* 数据源对象。

   ```R
   ds <- RxOdbcData(table="robjects", connectionString=conStr2)
   ```
3. 通过指定模型的 R 对象名称，从表中读取模型。

   ```R
    infertLogit2 <- rxReadObject(ds, "logit.model")
   ```

