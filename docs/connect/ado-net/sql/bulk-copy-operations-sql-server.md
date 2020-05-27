---
title: SQL Server 中的大容量复制操作
description: 介绍适用于 SQL Server 的 .NET 数据提供程序的大容量复制功能。
ms.date: 09/30/2019
ms.assetid: 83a7a0d2-8018-4354-97b9-0b1d99f8342b
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: c827ae70d9aa344f52de1d76c482beaef90c09aa
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "78897027"
---
# <a name="bulk-copy-operations-in-sql-server"></a>SQL Server 中的大容量复制操作

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Microsoft SQL Server 包含一个名为 bcp 的受欢迎的命令行实用工具，以便将较大文件快速大容量复制到 SQL Server 数据库的表或视图中  。 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 类允许你编写可提供类似功能的托管代码解决方案。 还可通过其他方法将数据加载到 SQL Server 表（例如 INSERT 语句），但 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 可提供显著的性能优势。  
  
使用 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 类，你可以执行以下操作：  
  
- 单次大容量复制操作  
  
- 多次大容量复制操作  
  
- 事务中的大容量复制操作  
  
> [!NOTE]
>  在使用 .NET Framework 1.1 版或更低版本时（不支持 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 类），可以使用 <xref:Microsoft.Data.SqlClient.SqlCommand> 对象执行 SQL Server Transact-SQL BULK INSERT 语句。  
  
## <a name="in-this-section"></a>在本节中  
[大容量复制示例设置](bulk-copy-example-setup.md)  
介绍用于大容量复制示例的表，并提供用于在 AdventureWorks 数据库中创建表的 SQL 脚本。  
  
[单次大容量复制操作](single-bulk-copy-operations.md)  
介绍如何使用 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 类将单个大容量数据复制到 SQL Server 实例，以及如何使用 Transact-SQL 语句和 <xref:Microsoft.Data.SqlClient.SqlCommand> 类执行大容量复制操作。  
  
[多次大容量复制操作](multiple-bulk-copy-operations.md)  
介绍如何使用 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 类在 SQL Server 的实例中执行多次大容量复制操作。  
  
[事务和大容量复制操作](transaction-bulk-copy-operations.md)  
介绍了如何在事务中执行大容量复制操作，包括如何提交或回滚事务。  
  
## <a name="next-steps"></a>后续步骤
- [SQL Server 和 ADO.NET](index.md)
