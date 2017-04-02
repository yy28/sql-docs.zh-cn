---
title: "与 SQL Server 数据一起使用的 scaleR 函数 | Microsoft Docs"
ms.custom: ""
ms.date: "01/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 5f3c9864-9c75-4688-947d-0940045b2671
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 7
---
# 与 SQL Server 数据一起使用的 scaleR 函数
本主题提供对其语法的注释以及与 SQL Server 一起使用的主要 ScaleR 功能概述。

ScaleR 函数以及如何使用它们的完整列表，请参阅 [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/index#) MSDN 库中的参考。 

## 使用 SQL Server 数据源的函数
以下函数，您可以定义 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 数据源。 数据源对象是指定的连接字符串以及您要定义为表、 视图或查询的数据集的容器。 不支持存储的过程调用。  

除了定义数据源，您可以从 R、 执行 DDL 语句只有实例和数据库的必要权限。 
+ [RxSqlServerData](https://msdn.microsoft.com/microsoft-r/scaler/RxSqlServerData) -定义 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 数据源对象
+ [rxSqlServerDropTable](https://msdn.microsoft.com/microsoft-r/scaler/rxSqlServerDropTable) -删除 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 表
+ [rxSqlServerTableExists](https://msdn.microsoft.com/microsoft-r/scaler/rxSqlServerTableExists) -检查是否存在的数据库表或对象
+ [rxExecuteSQLDDL](https://msdn.microsoft.com/microsoft-r/scaler/rxExecuteSQLDDL) -执行命令来定义、 操作或控制 SQL 数据，但不是会返回数据  

## 用于定义或管理计算上下文函数
以下函数，您可以定义新的计算上下文、 切换计算上下文，或确定当前的计算上下文。
+ [RxComputeContext](https://msdn.microsoft.com/microsoft-r/scaler/RxComputeContext) -创建一个计算上下文。 
+ [rxInSqlServer](https://msdn.microsoft.com/microsoft-r/scaler/rxInSqlServer) -生成 SQL Server 计算上下文，使 **ScaleR** 函数在 SQL Server R 服务中运行。
+ [rxGetComputeContext](https://msdn.microsoft.com/microsoft-r/scaler/rxGetComputeContext) -获取当前的计算上下文。 
+ [rxSetComputeContext](https://msdn.microsoft.com/microsoft-r/scaler/rxSetComputeContext) -指定哪一个计算要使用的上下文。 

## 用于将数据源使用函数
创建数据源对象之后，可以打开它，以获得数据，或向其写入新数据。 根据源中的数据的大小，您还可以作为数据源的一部分定义的批大小，然后在块中移动数据。 
+ [rxIsOpen](https://msdn.microsoft.com/microsoft-r/scaler/rxIsOpen) -检查数据源是否可用
+ [rxOpen](https://msdn.microsoft.com/microsoft-r/scaler/rxOpen) -打开以进行读取的数据源
+ [rxReadNext](https://msdn.microsoft.com/microsoft-r/scaler/rxReadNext) -从源读取数据
+ [rxWriteNext](https://msdn.microsoft.com/microsoft-r/scaler/rxWriteNext) -将数据写入到目标
+ [rxClose](https://msdn.microsoft.com/microsoft-r/scaler/rxclose) -关闭数据源

有关使用这些 ScaleR 函数的详细信息，这可以使用数据源之外 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], ，请参阅 [ Microsoft R Server-入门](http://msdn.microsoft.com/microsoft-r/rserver/rserver-getting-started)。

## 使用 XDF 文件的函数
可以使用以下函数以 XDF 格式创建的本地数据缓存。 在使用数据超过了可以从一个批处理中的数据库传输或更多的数据不能容纳在内存中时，此文件可以是非常有用。

如果您定期大量的数据将从数据库移到本地工作站，而不是查询每个 R 操作中，重复的数据库可用 XDF 文件来保存数据保存在本地，然后使用它在 R 工作区中，通过将 XDF 文件用作缓存。

+ `rxImport` 将数据从 ODBC 源移动到 XDF 文件
+ `RxXdfData` -创建 XDF 数据对象
+ `RxDataStep` -从读取数据 XDF int 数据帧
+ `rxXdfToDataFrame` 数据从读入 XDF 数据帧
+ `rxReadXdf` -将数据从 XDF 读入数据帧

有关如何使用 XDF 文件的示例，请参阅本教程︰  [数据科学深入探讨-使用 ScaleR 函数](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)

有关这些 ScaleR 函数，它可以用于将数据从许多不同的源传输，请参阅[ Microsoft R Server-入门](http://msdn.microsoft.com/microsoft-r/rserver/rserver-getting-started)。

## 另请参阅
[基本 R 和 ScaleR 函数的比较](https://msdn.microsoft.com/microsoft-r/scaler/compare-base-r-scaler-functions)
