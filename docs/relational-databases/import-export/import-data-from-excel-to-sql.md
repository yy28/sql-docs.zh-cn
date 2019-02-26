---
title: 将 Excel 数据导入 SQL | Microsoft Docs
ms.custom: ''
ms.date: 09/23/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cafc8346cbdd03c99f68ec879601689a7bf90781
ms.sourcegitcommit: a13256f484eee2f52c812646cc989eb0ce6cf6aa
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/25/2019
ms.locfileid: "56802214"
---
# <a name="import-data-from-excel-to-sql-server-or-azure-sql-database"></a>将 Excel 数据导入 SQL Server 或 Azure SQL 数据库
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

将 Excel 文件中的数据导入 SQL Server 或 Azure SQL 数据库的方法有多种。 某些方法允许你在单个步骤中从 Excel 文件直接导入数据，其他方法要求在导入数据前，必须将 Excel 数据先导出为文本。 本文总结了常用的方法，并提供有关更为详细的信息的链接。

## <a name="list-of-methods"></a>方法列表

-   可通过使用以下任一工具直接从 Excel 导入数据到 SQL：
    -   [SQL Server 导入和导出向导](#wiz)
    -   [SQL Server Integration Services (SSIS)](#ssis)
    -   [OPENROWSET](#openrowset) 函数
-   可分两步导入数据，将数据从 Excel 导出为文本，然后使用以下任一工具导入文本文件：
    -   [导入平面文件向导](#import-wiz)
    -   [BULK INSERT](#bulk-insert) 语句
    -   [BCP](#bcp)
    -   [复制向导（Azure 数据工厂）](#adf-wiz)
    -   [Azure 数据工厂](#adf)

如果要从 Excel 工作簿导入多个工作表，通常必须为每个工作表运行一次这些工具。

SSIS 或 Azure 数据工厂等复杂工具和服务的完整描述不属于本表的范围。 若要详细了解感兴趣的解决方案，请单击所提供的链接查看详细信息。

> [!IMPORTANT]
> 有关连接到 Excel 文件的详细信息，以及从 Excel 文件加载数据或将数据加载到 Excel 文件的限制和已知问题，请参阅[使用 SQL Server Integration Services (SSIS) 从 Excel 加载数据或将数据加载到 Excel 中](../../integration-services/load-data-to-from-excel-with-ssis.md)。

## <a name="wiz"></a>SQL Server 导入和导出向导

通过单步执行 SQL Server 导入和导出向导各页面，直接从 Excel 文件导入数据。 （可选）将设置保存为可以稍后自定义和重用的 SQL Server Integration Services (SSIS) 包。

要了解如何启动向导，请参阅[启动 SQL Server 导入和导出向导](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)。

有关使用向导将 Excel 导数据入 SQL Server 的示例，请参阅[从导入和导出向导的这个简单示例入手](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)。

![连接到 Excel 数据源](media/excel-connection.png)

## <a name="ssis"></a> SQL Server Integration Services (SSIS)

如果熟悉 SSIS，并且不想运行 SQL Server 导入和导出向导，请创建在数据流中使用 Excel 源和 SQL Server 目标的 SSIS 包。

有关这些 SSIS 组件的详细信息，请参阅以下主题：
-   [Excel 源](../../integration-services/data-flow/excel-source.md)
-   [SQL Server 目标](../../integration-services/data-flow/sql-server-destination.md)

若要开始学习如何生成 SSIS 包，请参阅教程[如何创建 ETL 包](../../integration-services/ssis-how-to-create-an-etl-package.md)。

![数据流中的组件](media/excel-to-sql-data-flow.png)

## <a name="openrowset"></a> OPENROWSET 和链接服务器

> [!NOTE]
> 在 Azure 中，OPENROWSET 和 OPENDATASOURCE 函数仅在 SQL 数据库托管实例上可用。

> [!NOTE]
> 连接到 Excel 数据源的 ACE 提供程序（前身为 Jet 提供程序）旨在用于交互式客户端用途。 如果在服务器上使用 ACE 提供程序，尤其是在自动进程或并行运行的进程中，可能会发生意外结果。

### <a name="distributed-queries"></a>分布式查询

使用 Transact-SQL `OPENROWSET` 或 `OPENDATASOURCE` 函数直接从 Excel 文件导入数据。 这种用法称为“分布式查询”。

必须先启用 `ad hoc distributed queries` 服务器配置选项（如以下示例所示），然后才能运行分布式查询。 有关详细信息，请参阅[即席分布式查询服务器配置选项](../../database-engine/configure-windows/ad-hoc-distributed-queries-server-configuration-option.md)。

```sql
sp_configure 'show advanced options', 1;
RECONFIGURE;
GO
sp_configure 'Ad Hoc Distributed Queries', 1;
RECONFIGURE;
GO
```

下面的代码示例使用 `OPENROWSET`，将 Excel `Data` 工作表中的数据导入新的数据库表。

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

若要查询（而不是导入）Excel 数据，只需使用标准 `SELECT ... FROM ...` 语法。

有关分布式查询的详细信息，请参阅以下主题：
-   [分布式查询](https://msdn.microsoft.com/library/ms188721(v=sql.105).aspx)。 （SQL Server 2016 仍支持分布式查询，但此功能的相关文档尚未更新。）
-   [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)
-   [OPENDATASOURCE](../../t-sql/functions/openquery-transact-sql.md)

### <a name="linked-servers"></a>链接服务器

还可以将与 Excel 文件的永久性连接配置为链接服务器。 下面的示例将现有 Excel 链接服务器 `EXCELLINK` 上的 `Data` 工作表数据导入名为 `Data_ls` 的新数据库表。

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

有关链接服务器的详细信息，请参阅以下主题：
-   [创建链接服务器](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md)
-   [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md)

有关链接服务器和分布式查询的更多示例和详细信息，请参阅以下主题：
-   [如何通过 SQL Server 链接服务器和分布式查询使用 Excel](https://support.microsoft.com/help/306397/how-to-use-excel-with-sql-server-linked-servers-and-distributed-queries)
-   [如何将 Excel 数据导入 SQL Server](https://support.microsoft.com/help/321686/how-to-import-data-from-excel-to-sql-server)

## <a name="prereq"></a>先决条件 - 将 Excel 数据保存为文本
若要使用本页上的其他方法（BULK INSERT 语句、BCP 工具或 Azure 数据工厂），必须先将 Excel 数据导出到文本文件中。

在 Excel 中，依次选择“文件”|“另存为”，再选择“文本文件(制表符分隔)(\*.txt)”或“CSV (逗号分隔)(\*.csv)”作为目标文件类型。

如果要从工作簿中导出多个工作表，请选择每个工作表，然后重复此过程。 “另存为”命令仅导出活动工作表。

> [!TIP]
> 为在使用数据导入工具时获得最佳结果，保存仅包含列标题和数据行的工作表。 如果保存的数据包含页标题、空白行、注释等，稍后可能会在导入数据时发生意外结果。

## <a name="import-wiz"></a> 导入平面文件向导

通过单步执行导入平面文件向导各页面，导入保存为文本文件的数据。

如前面[先决条件](#prereq)部分中所述，必须先将 Excel 数据导出为文本，然后才能使用导入平面文件向导导入它。

有关导入平面文件向导的详细信息，请参阅[将平面文件导入到 SQL 向导](import-flat-file-wizard.md)。

## <a name="bulk-insert"></a> BULK INSERT 命令

`BULK INSERT` 是可以通过 SQL Server Management Studio 运行的 Transact-SQL 命令。 下面的示例将 `Data.csv` 逗号分隔文件中的数据加载到现有数据库表中。

如前面[先决条件](#prereq)部分中所述，必须先将 Excel 数据导出为文本，然后才能使用 BULK INSERT 导入它。 BULK INSERT 无法直接读取 Excel 文件。

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

有关详细信息，请参阅以下主题：
-   [使用 BULK INSERT 或 OPENROWSET(BULK...) 导入批量数据](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)
-   [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)

## <a name="bcp"></a> BCP 工具

BCP 是通过命令提示符运行的程序。 下面的示例将 `Data.csv` 逗号分隔文件中的数据加载到现有 `Data_bcp` 数据库表中。

如前面[先决条件](#prereq)部分中所述，必须先将 Excel 数据导出为文本，然后才能使用 BCP 导入它。 BCP 无法直接读取 Excel 文件。

```sql
bcp.exe ImportFromExcel..Data_bcp in "D:\Desktop\data.csv" -T -c -t ,
```

有关 BCP 的详细信息，请参阅以下主题：
-   [使用 bcp 实用工具导入和导出大容量数据](../../relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)
-   [bcp 实用工具](../../tools/bcp-utility.md)
-   [准备用于批量导出或导入的数据](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)

## <a name="adf-wiz"></a> 复制向导（Azure 数据工厂）
通过单步执行 Azure 数据工厂复制向导各页面，导入保存为文本文件的数据。

如前面[先决条件](#prereq)部分中所述，必须先将 Excel 数据导出为文本，然后才能使用 Azure 数据工厂导入它。 数据工厂无法直接读取 Excel 文件。

有关复制向导的详细信息，请参阅以下主题：
-   [数据工厂复制向导](https://docs.microsoft.com/azure/data-factory/data-factory-azure-copy-wizard)
-   [教程：使用数据工厂复制向导创建带有复制活动的管道](https://docs.microsoft.com/azure/data-factory/data-factory-copy-data-wizard-tutorial)。

## <a name="adf"></a> Azure 数据工厂
如果熟悉 Azure 数据工厂，并且不想运行复制向导，请创建带有复制活动的管道，用于将文本文件复制到 SQL Server 或 Azure SQL 数据库。

如前面[先决条件](#prereq)部分中所述，必须先将 Excel 数据导出为文本，然后才能使用 Azure 数据工厂导入它。 数据工厂无法直接读取 Excel 文件。

若要详细了解如何使用这些数据工厂源和接收器，请参阅以下主题：
-   [文件系统](https://docs.microsoft.com/azure/data-factory/data-factory-onprem-file-system-connector)
-   [SQL Server](https://docs.microsoft.com/azure/data-factory/data-factory-sqlserver-connector)
-   [Azure SQL 数据库](https://docs.microsoft.com/azure/data-factory/data-factory-azure-sql-connector)

若要开始学习如何使用 Azure 数据工厂复制数据，请参阅以下主题：
-   [使用复制活动移动数据](https://docs.microsoft.com/azure/data-factory/data-factory-data-movement-activities)
-   [教程：使用 Azure 门户创建带有复制活动的管道](https://docs.microsoft.com/azure/data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database)

## <a name="see-also"></a>另请参阅
[使用 SQL Server Integration Services (SSIS) 将数据导入 Excel 或从 Excel 导出数据](../../integration-services/load-data-to-from-excel-with-ssis.md)
