---
title: "将 Excel 数据导入 SQL | Microsoft Docs"
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.assetid: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 70a1fd4dbec68d22187585de69a1d603c39e259e
ms.openlocfilehash: 3a978076b9776b57ffc996404c5f7773d7cf9094
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="import-data-from-excel-to-sql-server-or-azure-sql-database"></a>将 Excel 数据导入 SQL Server 或 Azure SQL 数据库
将 Excel 文件中的数据导入 SQL Server 或 Azure SQL 数据库的方法有多种。
-   可以使用 SQL Server 导入和导出向导、Integration Services (SSIS) 或 OPENROWSET 函数，直接将 Excel 数据导入 SQL。 
-   可以将 Excel 数据保存为文本，再使用 BULK INSERT 语句、BCP 或 Azure 数据工厂。 本文概述了这些选项，并通过链接来提供更多详细说明。

> [!NOTE]
> SSIS 或 Azure 数据工厂等复杂工具和服务的完整描述不属于本概述的范围。 若要详细了解感兴趣的解决方案，请单击所提供的链接，查看教程和详细信息。

## <a name="sql-server-import-and-export-wizard"></a>SQL Server 导入和导出向导

通过逐步执行向导各页面，直接从 Excel 文件导入数据。 根据需要，将导入/导出设置保存为可以自定义和重用的 SQL Server Integration Services (SSIS) 包。

![连接到 Excel 数据源](media/excel-connection.png)

有关使用向导将 Excel 导数据入 SQL Server 的示例，请参阅[从导入和导出向导的这个简单示例入手](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)。

## <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)

如果熟悉 SSIS，并且不想运行 SQL Server 导入和导出向导，请创建在数据流中使用 Excel 源和 SQL Server 目标的 SSIS 包。

![数据流中的组件](media/excel-to-sql-data-flow.png)

有关这些 SSIS 组件的详细信息，请参阅以下主题。
-   [Excel 源](../../integration-services/data-flow/excel-source.md)
-   [SQL Server 目标](../../integration-services/data-flow/sql-server-destination.md)

若要开始学习如何生成 SSIS 包，请参阅教程[如何创建 ETL 包](../../integration-services/ssis-how-to-create-an-etl-package.md)。

## <a name="openrowset-and-linked-servers"></a>OPENROWSET 和链接服务器
> [!NOTE]
> 连接到 Excel 文件的 ACE 提供程序（前身为 Jet 提供程序）旨在用于交互式客户端用途。 如果在服务器上使用 ACE 提供程序，尤其是在自动进程或并行运行的进程中，可能会发生意外结果。

使用 `OPENROWSET` 或 `OPENDATASOURCE` 函数直接从 Excel 文件导入数据。 这种用法称为“分布式查询”。

必须先启用 `ad hoc distributed queries` 服务器配置选项（如以下示例所示），然后才能运行分布式查询。 有关详细信息，请参阅[即席分布式查询服务器配置选项](../../database-engine/configure-windows/ad-hoc-distributed-queries-server-configuration-option.md)。

```sql
sp_configure 'show advanced options', 1;
RECONFIGURE;
GO
sp_configure 'Ad Hoc Distributed Queries', 1;
RECONFIGURE;
GO
```

下面的代码示例使用 `OPENROWSET`，将 Excel `Customers` 工作表中的数据导入新的 SQL Server 表。

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_dq
FROM OPENROWSET('Microsoft.ACE.OLEDB.12.0',
    'Excel 12.0; Database=D:\Desktop\Data.xlsx', [Data$]);
GO
```

下面的示例用途相同，区别在于使用的是 `OPENDATASOURCE`。

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_dq
FROM OPENDATASOURCE('Microsoft.ACE.OLEDB.12.0',
    'Data Source=D:\Desktop\Data.xlsx;Extended Properties=Excel 12.0')...[Data$];
GO
```

若要将导入的数据追加到现有表，而不是新建表，请使用 `INSERT INTO ... SELECT ... FROM ...` 语法，而不是上面示例中使用的 `SELECT ... INTO ... FROM ...` 语法。

若要查询（而不是导入）Excel 数据，只需使用 `SELECT ... FROM ...` 语法。

有关分布式查询的详细信息，请参阅以下主题。
-   [分布式查询](https://msdn.microsoft.com/library/ms188721(v=sql.105).aspx)。 （SQL Server 2016 仍支持分布式查询，但此功能的相关文档尚未更新。）
-   [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)
-   [OPENDATASOURCE](../../t-sql/functions/openquery-transact-sql.md)

还可以将与 Excel 文件的永久性连接配置为链接服务器。 下面的示例将现有 Excel 链接服务器 `EXCELLINK` 上的 `Data` 工作表数据导入名为 `Data_ls` 的新 SQL Server 表。

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_ls FROM EXCELLINK...[Data$];
GO
```

可以通过 SQL Server Management Studio 或运行系统存储过程 `sp_addlinkedserver`（如以下示例所示）创建链接服务器。

```sql
DECLARE @RC int

DECLARE @server     nvarchar(128)
DECLARE @srvproduct nvarchar(128)
DECLARE @provider   nvarchar(128)
DECLARE @datasrc    nvarchar(4000)
DECLARE @location   nvarchar(4000)
DECLARE @provstr    nvarchar(4000)
DECLARE @catalog    nvarchar(128)

-- Set parameter values
SET @server =     'EXCELLINK'
SET @srvproduct = 'Excel'
SET @provider =   'Microsoft.ACE.OLEDB.12.0'
SET @datasrc =    'D:\Desktop\Data.xlsx'
SET @provstr =    'Excel 12.0'

EXEC @RC = [master].[dbo].[sp_addlinkedserver] @server, @srvproduct, @provider,
@datasrc, @location, @provstr, @catalog
```

有关链接服务器的详细信息，请参阅以下主题。
-   [创建链接服务器](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md)
-   [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md)

有关链接服务器和分布式查询的更多示例和详细信息，请参阅以下主题。
-   [如何通过 SQL Server 链接服务器和分布式查询使用 Excel](https://support.microsoft.com/help/306397/how-to-use-excel-with-sql-server-linked-servers-and-distributed-queries)
-   [如何将 Excel 数据导入 SQL Server](https://support.microsoft.com/help/321686/how-to-import-data-from-excel-to-sql-server)

## <a name="prerequisite---save-excel-data-as-text"></a>先决条件 - 将 Excel 数据保存为文本
若要使用本页上的其他方法（BULK INSERT 语句、BCP 工具或 Azure 数据工厂），必须先将 Excel 数据导出到文本文件中。

在 Excel 中，依次选择“文件”|“另存为”，再选择“文本文件(制表符分隔)(\*.txt)”或“CSV (逗号分隔)(\*.csv)”作为目标文件类型。

> [!TIP]
> 为在使用数据导入工具时获得最佳结果，保存仅包含列标题和数据行的工作表。 如果保存的数据包含页标题、空白行、注释等，稍后可能会在导入数据时发生意外结果。

## <a name="bulk-insert-command"></a>BULK INSERT 命令

`BULK INSERT` 是可以通过 SQL Server Management Studio 运行的命令。 下面的示例将 `Data.csv` 逗号分隔文件中的数据加载到现有表中。

```sql
USE ImportFromExcel;
GO
BULK INSERT Data_bi FROM 'D:\Desktop\data.csv'
   WITH (
      FIELDTERMINATOR = ',',
      ROWTERMINATOR = '\n'
);
GO
```

有关详细信息，请参阅以下主题。
-   [使用 BULK INSERT 或 OPENROWSET(BULK...) 导入批量数据](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)
-   [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)

## <a name="bcp-tool"></a>BCP 工具

BCP 是通过命令提示符运行的 SQL Server。 下面的示例将 `Data.csv` CSV 文件中的数据加载到 SQL Server 的现有 `Data_bcp` 表中。

```sql
bcp.exe ImportFromExcel..Data_bcp in "D:\Desktop\data.csv" -T -c -t ,
```

有关详细信息，请参阅以下主题。
-   [使用 bcp 实用工具导入和导出大容量数据](../../relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)
-   [bcp 实用工具](../../tools/bcp-utility.md)
-   [准备用于批量导出或导入的数据](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)

## <a name="copy-wizard-azure-data-factory"></a>复制向导（Azure 数据工厂）
通过逐步执行向导各页面，导入保存为文本文件的数据。 有关复制向导的详细信息，请参阅以下主题。
-   [数据工厂复制向导](https://docs.microsoft.com/azure/data-factory/data-factory-azure-copy-wizard)
-   [教程：使用数据工厂复制向导创建带有复制活动的管道](https://docs.microsoft.com/azure/data-factory/data-factory-copy-data-wizard-tutorial)。

## <a name="azure-data-factory"></a>Azure 数据工厂
如果熟悉 Azure 数据工厂，并且不想运行 Azure 数据工厂复制向导，请创建带有复制活动的管道，用于将文件存储位置中的文本文件复制到 SQL Server 或 Azure SQL 数据库。

若要详细了解如何使用这些数据工厂源和接收器，请参阅以下主题。
-   [文件系统](https://docs.microsoft.com/azure/data-factory/data-factory-onprem-file-system-connector)
-   [SQL Server](https://docs.microsoft.com/azure/data-factory/data-factory-sqlserver-connector)
-   [Azure SQL 数据库](https://docs.microsoft.com/azure/data-factory/data-factory-azure-sql-connector)

若要开始学习如何使用 Azure 数据工厂复制数据，请参阅以下主题。
-   [使用复制活动移动数据](https://docs.microsoft.com/azure/data-factory/data-factory-data-movement-activities)
-   [教程：使用 Azure 门户创建带有复制活动的管道](https://docs.microsoft.com/azure/data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database)

