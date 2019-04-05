---
title: 虚拟化 SQL Server 2019 CTP 2.0 中的外部数据 | Microsoft Docs
description: 此页面详细介绍了为 CSV 文件使用“创建外部表”向导的步骤
author: Abiola
ms.author: aboke
ms.reviewer: jroth
manager: craigg
ms.date: 03/27/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: polybase
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: dae0692bafd8c4de295a914c9da0ead5c6e3980b
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58512954"
---
# <a name="use-the-external-table-wizard-with-csv-files"></a>将外部表向导与 CSV 文件一起使用

SQL Server 2019 还允许从 HDFS 中的 CSV 文件虚拟化数据。  此过程允许将数据保留在其原始位置，但可以虚拟化 SQL Server 实例中的数据，以便可以对这些数据进行查询，如同 SQL Server 中的任何其他表一样。 此功能将最大限度地减少对 ETL 进程的需要。 可以使用 Polybase 连接器。 有关数据虚拟化的详细信息，请参阅 [PolyBase 入门](polybase-guide.md)文档。

## <a name="prerequisite"></a>先决条件

自 CTP 2.4 起，数据池和存储池外部数据源默认不会再创建在大数据群集中。 在使用向导之前，请使用以下 Transact-SQL 查询在目标数据库中创建默认 SqlStoragePool 外部数据源。 请确保首先将查询的上下文更改为目标数据库。

```sql
IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
  BEGIN
    IF SERVERPROPERTY('ProductLevel') = 'CTP2.3'
      CREATE EXTERNAL DATA SOURCE SqlStoragePool
      WITH (LOCATION = 'sqlhdfs://service-mssql-controller:8080');
    ELSE IF SERVERPROPERTY('ProductLevel') = 'CTP2.4'
      CREATE EXTERNAL DATA SOURCE SqlStoragePool
      WITH (LOCATION = 'sqlhdfs://service-master-pool:50070');
  END
```

## <a name="launch-the-external-table-wizard"></a>启动外部表向导

使用 IP 地址连接到 HDFS 根。 在对象资源管理器中展开元素。 然后选择一个要将其中的数据虚拟化到现有 SQL Server 实例的 CSV。 右键单击文件，然后从上下文菜单中选择“从 CSV 文件中创建外部表”。 还可以从 HDFS 中的文件夹中的 CSV 文件创建外部表（如果文件夹下的这些文件遵循相同架构）。 这将允许在文件夹级别虚拟化数据，而无需处理单个文件，并获得组合数据的联接结果集。 这将启动虚拟化数据向导。 也可以通过键入 Ctrl+Shift+P（在 Windows 中）和 Cmd+Shift+P（在 Mac 中），从命令面板启动虚拟化数据向导。

![虚拟化数据向导](media/data-virtualization/csv-virtualize-data-wizard.png)

## <a name="connect-to-a-sql-server-master-instance"></a>连接到 SQL Server 主实例

可以在此处使用 IP、端口和凭据信息指定要连接到的 SQL 主实例。 可以通过“活动 SQL Server 连接”下拉框访问之前保存的连接。 
> [!NOTE]
>如果使用的是已保存的连接，则其他字段将被阻止


![选择数据源](media/data-virtualization/csv-connect-to-master.png)

单击“下一步”以继续执行向导中的下一步，即设置数据库主密钥。

## <a name="select-destination-database"></a>选择目标数据库

在此步骤中，将选择要将数据虚拟化到其中的目标数据库。 下拉字段将包含上一屏幕中指定的 SQL 主实例中的所有可接受的数据库。 在这里，还可以命名新的外部表并查看它将使用的架构。

![创建数据库主密钥](media/data-virtualization/csv-select-destination.png)


## <a name="preview-data"></a>预览数据

在此窗口中，你将能够查看以供验证的 CSV 文件的前 50 行的预览。

完成查看预览后，单击“下一步”继续

![外部数据源凭据](media/data-virtualization/csv-preview-data.png)

## <a name="modify-columns"></a>修改列

在下一个窗口中，你将能够修改要创建的外部表的列。 你将能够更改列名称、更改数据类型并允许可为 Null 的行。 

![外部数据源凭据](media/data-virtualization/csv-modify-columns.png)


## <a name="summary"></a>“摘要”

此步骤提供所选对象的摘要。 它提供 SQL 主实例和建议的外部表信息。 在此步骤中，可以选择“生成脚本”（这会在 T-SQL 中编写语法脚本以创建外部数据源）或“创建”（这会创建外部数据源对象）。

![“摘要”屏幕](media/data-virtualization/csv-virtualize-data-summary.png)

如果单击“创建”，你将能够看到目标数据库中创建的外部表。

![外部数据源](media/data-virtualization/csv-external-data-sources.png)

如果单击“生成脚本”，你将看到为创建外部数据源对象生成的 T-SQL 查询。

![生成脚本](media/data-virtualization/csv-generated-script.png)

> [!NOTE]
> “生成脚本”应仅在向导的最后一页中显示。 目前显示在所有页面中。

## <a name="next-steps"></a>后续步骤

有关 SQL Server 大数据群集和相关方案的详细信息，请参阅[什么是 SQL Server 大数据群集？](../../big-data-cluster/big-data-cluster-overview.md)。
