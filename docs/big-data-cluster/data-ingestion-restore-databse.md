---
title: 将数据库还原到 SQL Server 大数据群集 |Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 04514fb0184fa28e0ba959f3dd33cb2e1ec945cb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48795932"
---
# <a name="restore-a-database-into-the-sql-server-big-data-cluster-master-instance"></a>将数据库还原为 SQL Server 大数据群集的主实例

若要将现有的 SQL Server 数据库引入主实例，我们建议使用备份、 复制和还原方法。  在此示例中，我们将演示如何还原 AdventureWorks 数据库中，但可以使用任何你拥有的数据库备份。  您可以下载 AdventureWorks 备份[此处](https://www.microsoft.com/en-us/download/details.aspx?id=49502)。

首先，备份在 Windows 上 SQL Server 或 Linux 使用任何一种常用方法创建的数据库备份的现有 SQL Server 数据库。

将备份文件复制到 Kubernetes 群集的主实例 pod 中的 SQL Server 容器。

```bash
kubectl cp <path to .bak file> mssql-data-pool-master-0:/tmp/ -c mssql-data-pool-data -n <name of your cluster>
```

例如：

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak mssql-data-pool-master-0:/tmp/ -c mssql-data-pool-data -n clustertest
```

然后，验证备份文件已复制到 pod 容器。

```bash
kubectl exec -it mssql-data-pool-master-0 -n <name of your cluster> -c mssql-data-pool-data -- bin/bash
root@mssql-data-pool-master-0:/# ls /tmp
root@mssql-data-pool-master-0:/# exit
```

例如：

```bash
kubectl exec -it mssql-data-pool-master-0 -n clustertest -c mssql-data-pool-data -- bin/bash
root@mssql-data-pool-master-0:/# ls /tmp
```

接下来，将数据库备份还原到主实例 SQL Server。  如果要还原已在 Windows 创建的数据库备份，需要获取的文件的名称。  Ops Studio 连接到主实例中运行此 SQL 脚本：

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/<db file name>.bak'
```

例如：

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
```

![备份文件列表](media/restore-database/database-restore-file-list.png)

现在，使用还原数据库类似，下面的脚本替换为根据需要根据你数据库的备份名称/路径。

```sql
RESTORE DATABASE AdventureWorks2016CTP3
FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
WITH MOVE 'AdventureWorks2016CTP3_Data' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Data.mdf',
        MOVE 'AdventureWorks2016CTP3_Log' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Log.ldf',
        MOVE 'AdventureWorks2016CTP3_mod' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_mod'
```

现在，如果你想要具有高价值数据库能够访问数据池，你将需要安装程序数据池通过打开并运行这些脚本从 GitHub 存储库的存储过程。

执行**高值 db configuration\data_pool_ddl_install。SQL**脚本。

- 安装程序可支持性存储过程

执行**高值 db configuration\supportability。SQL**脚本。
