---
title: "用于处理 SQL Server 数据的 ScaleR 函数 | Microsoft Docs"
ms.custom: 
ms.date: 01/27/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 5f3c9864-9c75-4688-947d-0940045b2671
caps.latest.revision: 9
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0e1e202b85e8a8105e0222cfe015f2de8def5b91
ms.lasthandoff: 04/11/2017

---
# <a name="scaler-functions-for-working-with-sql-server-data"></a>用于处理 SQL Server 数据的 ScaleR 函数
本主题概述了用于 SQL Server 的主要 ScaleR 函数以及有关其语法的注释。

有关 ScaleR 函数的完整列表和关于如何使用它们的信息，请参阅 MSDN 库中的 [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/index#) 参考。 

## <a name="functions-for-working-with-sql-server-data-sources"></a>用于处理 SQL Server 数据源的函数
以下函数允许你定义 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 数据源。 数据源对象是一个容器，它指定了连接字符串以及你需要的以表、视图或查询格式定义的数据集。 不支持存储过程调用。  

除了定义数据源之外，如果你在实例和数据库上具有所需的权限，则还可以从 R 执行 DDL 语句。 
+ [RxSqlServerData](https://msdn.microsoft.com/microsoft-r/scaler/RxSqlServerData) - 定义 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 数据源对象
+ [rxSqlServerDropTable](https://msdn.microsoft.com/microsoft-r/scaler/rxSqlServerDropTable) - 删除 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 表
+ [rxSqlServerTableExists](https://msdn.microsoft.com/microsoft-r/scaler/rxSqlServerTableExists) - 检查是否存在某个数据库表或对象
+ [rxExecuteSQLDDL](https://msdn.microsoft.com/microsoft-r/scaler/rxExecuteSQLDDL) - 执行命令来定义、操作或控制 SQL 数据，但不返回数据  

## <a name="functions-for-defining-or-managing-a-compute-context"></a>用于定义或管理计算上下文的函数
以下函数允许你定义新的计算上下文、切换计算上下文或者标识当前计算上下文。
+ [RxComputeContext](https://msdn.microsoft.com/microsoft-r/scaler/RxComputeContext) - 创建计算上下文。 
+ [rxInSqlServer](https://msdn.microsoft.com/microsoft-r/scaler/rxInSqlServer) - 生成一个允许在 SQL Server R Services 中运行 **ScaleR** 函数的 SQL Server 计算上下文。 当前，只有 Windows 上的 SQL Server 实例支持此计算上下文。
+ [rxGetComputeContext](https://msdn.microsoft.com/microsoft-r/scaler/rxGetComputeContext) - 获取当前的计算上下文。 
+ [rxSetComputeContext](https://msdn.microsoft.com/microsoft-r/scaler/rxSetComputeContext) - 指定要使用的计算上下文。 

## <a name="functions-for-using-a-data-source"></a>用于使用数据源的函数
在创建数据源对象后，你可以打开它来获取数据，或者向其中写入新数据。 你还可以根据源中的数据大小将批大小定义为数据源的一部分，并成块移动数据。 
+ [rxIsOpen](https://msdn.microsoft.com/microsoft-r/scaler/rxIsOpen) - 检查数据源是否可用
+ [rxOpen](https://msdn.microsoft.com/microsoft-r/scaler/rxOpen) - 打开数据源进行读取
+ [rxReadNext](https://msdn.microsoft.com/microsoft-r/scaler/rxReadNext) - 从源中读取数据
+ [rxWriteNext](https://msdn.microsoft.com/microsoft-r/scaler/rxWriteNext) - 将数据写入到目标
+ [rxClose](https://msdn.microsoft.com/microsoft-r/scaler/rxclose) - 关闭数据源

有关使用这些 ScaleR 函数（它们可以用于除 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 之外的数据源）的详细信息，请参阅 [Microsoft R Server - 入门](https://msdn.microsoft.com/microsoft-r/rserver)。

## <a name="functions-that-work-with-xdf-files"></a>用于处理 XDF 文件的函数
以下函数可以用来创建 XDF 格式的本地数据缓存。 当处理的数据多于可以在一批中从数据库传输的数据时，或者数据多于内存中可以容纳的数据时，此文件可能比较有用。

如果你定期将大量数据从数据库移动到本地工作站，而非针对每个 R 操作重复查询数据库，则可以使用 XDF 文件将数据保存在本地，然后使用 XDF 文件作为缓存在你的 R 工作区中处理数据。

+ `rxImport` - 将数据从 ODBC 源移动到 XDF 文件
+ `RxXdfData` - 创建 XDF 数据对象
+ `RxDataStep` - 将数据从 XDF 读取到数据帧中
+ `rxXdfToDataFrame` - 将数据从 XDF 读取到数据帧中
+ `rxReadXdf` - 将数据从 XDF 读取到数据帧中

有关如何使用 XDF 文件的示例，请参阅以下教程：[对数据科学的深入探讨 - 使用 ScaleR 函数](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)

有关这些 ScaleR 函数（它们可以用来从许多源传输数据）的详细信息，请参阅 [ Microsoft R Server - 入门](http://msdn.microsoft.com/microsoft-r/rserver/rserver-getting-started)。

## <a name="see-also"></a>另请参阅
[Base R 函数和 ScaleR 函数之对比](https://msdn.microsoft.com/microsoft-r/scaler/compare-base-r-scaler-functions)


