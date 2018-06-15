---
title: 配置设置 (SQL Server 数据 Migration Assistant) |Microsoft 文档
ms.custom: ''
ms.date: 08/31/2017
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: 4b42f816755b312f95609bd25ac6122b8fbf321c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32867202"
---
# <a name="configuration-settings-for-data-migration-assistant"></a>数据迁移助手配置设置

你可以微调数据迁移助手 dma.exe.config 文件中使用配置值的某些的行为。 本指南介绍了密钥配置值。

你可以查找 dma.exe.config 文件数据迁移助手的桌面应用程序和命令行实用工具，您的计算机上的以下文件夹中。

- 桌面应用程序

  %Programfiles%\\Microsoft 数据迁移助手\\dma.exe.config

- 命令行实用工具

  %Programfiles%\\Microsoft 数据迁移助手\\dmacmd.exe.config 

请确保在进行任何修改之前保存原始配置文件的副本。 进行更改后，重新启动数据迁移助手将新的配置值才能生效。

## <a name="number-of-databases-to-assess-in-parallel"></a>若要评估并行中的数据库数目

数据迁移助手评估并行的多个数据库。 在评估期间数据迁移助手中提取数据层应用程序 (dacpac) 以了解数据库架构。 此操作可能会超时，如果在同一服务器上的多个数据库评估并行。 

从开始数据迁移助手 2.0 版，你可以 controll 这通过设置 parallelDatabases 配置值。 默认值为 8。

```
<advisorGroup>

<workflowSettings>

<assessment parallelDatabases="8" />

</workflowSettings>

</advisorGroup>
```




## <a name="number-of-databases-to-migrate-in-parallel"></a>若要并行迁移的数据库数

数据迁移助手将迁移并行，多个数据库之前迁移的登录名。 在迁移期间，数据迁移助手将源数据库的备份、 （可选） 将备份、 复制，然后将其还原到目标服务器。 在为迁移选择多个数据库，可能会遇到超时失败。 

从开始数据迁移助手 v2.0，如果遇到此问题，你可以减少 parallelDatabases 配置值。 你可以增加要减少总体迁移时间的值。

```
<advisorGroup>

<workflowSettings>

<migration parallelDatabases=”8″ />

</workflowSettings>

</advisorGroup>
```


## <a name="dacfx-settings"></a>DacFX 设置

在评估期间数据迁移助手中提取数据层应用程序 (dacpac) 以了解数据库架构。 此操作会失败，且超时对于极大型数据库，或如果服务器负载。 从开始数据迁移 v1.0，你可以修改以下的配置值，若要避免错误。 

> [!NOTE]
> 整个&lt;dacfx&gt;默认情况下注释条目。 移除注释，然后根据需要修改值。

- CommandTimeout

   这会设置 IDbCommand.CommandTimeout 属性中*秒*。 (默认值 = 60)

- databaseLockTimeout

   这相当于[设置锁\_超时超时\_段](../t-sql/statements/set-lock-timeout-transact-sql.md)中*毫秒*。 (默认 = 5000)

- maxDataReaderDegreeOfParallelism

   要使用的 SQL 连接池连接的数目。 (默认值 = 8)

```
<advisorGroup>

<advisorSettings>

<dacFx  commandTimeout="60" databaseLockTimeout="5000"
maxDataReaderDegreeOfParallelism="8"/>

</advisorSettings>

</advisorGroup>
```


## <a name="stretch-database-recommendation-threshold"></a>Stretch Database： 建议阈值

与[SQL Server Stretch Database](https://docs.microsoft.com/sql/sql-server/stretch-database/stretch-database)，您可以动态将延长，冷、 暖事务性数据从 Microsoft SQL Server 2016 到 Azure。 Stretch Database 针对包含大量冷数据的事务数据库。 Stretch Database 建议，在存储功能建议首先标识表它认为将受益此功能，而它然后确定不需要进行若要启用此功能的表的更改。

从开始数据迁移助手 2.0 版，你可以控制此阈值，才能用于限定为 Stretch Database 功能使用 recommendedNumberOfRows 配置值的表。 默认值为 100,000 行。 如果你想要分析变得更小的表的拉伸功能，然后相应地降低值。

```
<advisorGroup>

<advisorSettings>

<stretchDBAdvisor  recommendedNumberOfRows="100000" />

</advisorSettings>

</advisorGroup>
```


## <a name="sql-connection-timeout"></a>SQL 连接超时

你可以控制[SQL 连接超时](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectiontimeout(v=vs.110).aspx)时通过将连接超时值设置为指定的秒数运行评估或迁移，源和目标实例。 默认值为 15 秒。

```
<appSettings>

<add key="ConnectionTimeout" value="15" />

</appSettings>
```


## <a name="see-also"></a>另请参阅

[数据迁移助手下载](https://www.microsoft.com/download/details.aspx?id=53595)
