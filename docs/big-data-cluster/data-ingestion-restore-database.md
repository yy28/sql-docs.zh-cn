---
title: 还原数据库
titleSuffix: SQL Server big data clusters
description: 本文介绍如何将数据库还原为 SQL Server 2019 大数据群集 （预览版） 的主实例。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1ad5ca749f3862f0d7df3411efd78104052dba91
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958627"
---
# <a name="restore-a-database-into-the-sql-server-big-data-cluster-master-instance"></a>将数据库还原为 SQL Server 大数据群集的主实例

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍如何将现有数据库还原到 SQL Server 2019 大数据群集 （预览版） 的主实例。 建议的方法是使用备份、 复制和还原方法。

## <a name="backup-your-existing-database"></a>备份您现有的数据库

首先，备份您现有的 SQL Server 数据库从 SQL Server 在 Windows 或 Linux。 使用 TRANSACT-SQL 或 SQL Server Management Studio (SSMS) 等工具，请使用标准的备份方法。

本文介绍如何还原 AdventureWorks 数据库中，但可以使用的任何数据库备份。 

> [!TIP]
> 您可以下载 AdventureWorks 备份[此处](https://www.microsoft.com/download/details.aspx?id=49502)。

## <a name="copy-the-backup-file"></a>将备份文件复制

将备份文件复制到 Kubernetes 群集的主实例 pod 中的 SQL Server 容器。

```bash
kubectl cp <path to .bak file> mssql-master-pool-0:/tmp -c mssql-server -n <name of your big data cluster>
```

例如：

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak mssql-master-pool-0:/tmp -c mssql-server -n clustertest
```

然后，验证备份文件已复制到 pod 容器。

```bash
kubectl exec -it mssql-master-pool-0 -n <name of your big data cluster> -c mssql-server -- bin/bash
cd /var/
ls /tmp
exit
```

例如：

```bash
kubectl exec -it mssql-master-pool-0 -n clustertest -c mssql-server -- bin/bash
ls /tmp
exit
```

## <a name="restore-the-backup-file"></a>将备份文件还原

接下来，将数据库备份还原到主实例 SQL Server。  如果要还原已在 Windows 创建的数据库备份，需要获取的文件的名称。  在 Azure Data Studio，连接到主实例并运行此 SQL 脚本：

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/<db file name>.bak'
```

例如：

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
```

![备份文件列表](media/restore-database/database-restore-file-list.png)

现在，还原数据库。 以下脚本是一个示例。 将为名称/路径根据需要根据你的数据库备份。

```sql
RESTORE DATABASE AdventureWorks2016CTP3
FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
WITH MOVE 'AdventureWorks2016CTP3_Data' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Data.mdf',
        MOVE 'AdventureWorks2016CTP3_Log' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Log.ldf',
        MOVE 'AdventureWorks2016CTP3_mod' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_mod'
```

## <a name="configure-data-pool-and-hdfs-access"></a>配置数据池和 HDFS 的访问

现在，对于访问数据池和 HDFS 到 SQL Server 主实例，运行数据池和存储池的存储过程。 对新还原的数据库运行以下 TRANSACT-SQL 脚本：

```sql
USE AdventureWorks2016CTP3
GO
-- Create the SqlDataPool data source:
IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
  CREATE EXTERNAL DATA SOURCE SqlDataPool
  WITH (LOCATION = 'sqldatapool://controller-svc/default');

-- Create the SqlStoragePool data source:
IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
   CREATE EXTERNAL DATA SOURCE SqlStoragePool
   WITH (LOCATION = 'sqlhdfs://controller-svc/default');
GO
```

> [!NOTE]
> 必须将通过仅从较旧版本的 SQL Server 还原的数据库的这些安装程序脚本运行。 SQL Server 主实例中创建新的数据库，如果已为你配置数据池和存储池存储过程。

## <a name="next-steps"></a>后续步骤

若要了解有关 SQL Server 大数据群集的详细信息，请参阅以下概述：

- [什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)
