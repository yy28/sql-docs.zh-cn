---
title: 配置设置的数据迁移助手 (SQL Server) |Microsoft Docs
description: 了解如何配置用于数据迁移助手的更新配置文件中的值设置
ms.custom: ''
ms.date: 10/20/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: pochiraju
ms.author: rajpo
manager: craigg
ms.openlocfilehash: 9801afda1a876f486e7b7042d3dad082c70c99fa
ms.sourcegitcommit: 38f35b2f7a226ded447edc6a36665eaa0376e06e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2018
ms.locfileid: "49643815"
---
# <a name="configure-settings-for-data-migration-assistant"></a>为数据迁移助手配置设置

可以通过 dma.exe.config 文件中设置配置值来微调特定的数据迁移助手的行为。 本指南介绍了关键的配置值。

您可以找到 dma.exe.config 文件数据迁移助手的桌面应用程序和命令行实用程序，在计算机上的以下文件夹中。

- 桌面应用程序

  %Programfiles%\\Microsoft 数据迁移助手\\dma.exe.config

- 命令行实用程序

  %Programfiles%\\Microsoft 数据迁移助手\\dmacmd.exe.config 

请务必进行任何修改之前保存一份原始配置文件。 进行更改后，重新启动数据迁移助手的新的配置值才会生效。

## <a name="number-of-databases-to-assess-in-parallel"></a>评估并行中的数据库数量

数据迁移助手来评估并行的多个数据库。 在评估期间数据迁移助手中提取数据层应用程序 (dacpac) 以了解数据库架构。 如果在同一服务器上的多个数据库评估并行，则此操作可能超时。 

从数据迁移助手的 2.0 版开始，你可以控制这通过设置 parallelDatabases 配置值。 默认值为 8。

```
<advisorGroup>

<workflowSettings>

<assessment parallelDatabases="8" />

</workflowSettings>

</advisorGroup>
```




## <a name="number-of-databases-to-migrate-in-parallel"></a>要并行迁移的数据库的数目

数据迁移助手迁移并行情况下，多个数据库之前迁移登录名。 在迁移期间，数据迁移助手将进行源数据库的备份，可以选择复制备份，然后将其还原到目标服务器。 选择用于迁移的多个数据库时，可能会遇到超时故障。 

从数据迁移助手版本 2.0 开始，如果遇到此问题可以减少 parallelDatabases 配置值。 可以增大该值以减少整体迁移时间。

```
<advisorGroup>

<workflowSettings>

<migration parallelDatabases=”8″ />

</workflowSettings>

</advisorGroup>
```


## <a name="dacfx-settings"></a>DacFX 设置

在评估期间数据迁移助手中提取数据层应用程序 (dacpac) 以了解数据库架构。 此操作可能会失败，具有超时值对于极大型数据库，或如果服务器负载。 从数据迁移 1.0 版开始，可以修改以下的配置值，以避免错误。 

> [!NOTE]
> 整个&lt;dacfx&gt;默认情况下注释条目。 删除注释，并根据需要修改值。

- commandTimeout

   此参数设置 IDbCommand.CommandTimeout 属性中*秒*。 (默认值 = 60)

- databaseLockTimeout

   此参数等效于[设置锁\_超时超时\_段](../t-sql/statements/set-lock-timeout-transact-sql.md)中*毫秒*。 (默认值 = 5000)

- maxDataReaderDegreeOfParallelism

  此参数设置使用 SQL 连接池连接的数量。 (默认值 = 8)

```
<advisorGroup>

<advisorSettings>

<dacFx  commandTimeout="60" databaseLockTimeout="5000"
maxDataReaderDegreeOfParallelism="8"/>

</advisorSettings>

</advisorGroup>
```

## <a name="stretch-database-recommendation-threshold"></a>Stretch Database： 建议阈值

与[SQL Server Stretch Database](https://docs.microsoft.com/sql/sql-server/stretch-database/stretch-database)，可以动态拉伸冷暖事务数据从 Microsoft SQL Server 2016 到 Azure。 Stretch Database 针对包含大量冷数据的事务数据库。 Stretch Database 建议，在存储功能建议，首先标识的表，它认为将受益于此功能，和它然后确定不需要进行若要启用此功能的表的更改。

从数据迁移助手的 2.0 版开始，可以控制此阈值，才能有资格获得使用 recommendedNumberOfRows 配置值的 Stretch Database 功能的表。 默认值为 10 万行。 如果你想要分析甚至较小的表的延伸功能，然后相应地减小的值。

```
<advisorGroup>

<advisorSettings>

<stretchDBAdvisor  recommendedNumberOfRows="100000" />

</advisorSettings>

</advisorGroup>
```


## <a name="sql-connection-timeout"></a>SQL 连接超时

您可以控制[SQL 连接超时](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectiontimeout(v=vs.110).aspx)源和目标实例时运行的评估或迁移，通过将连接超时值设置为指定的秒数。 默认值为 15 秒。

```
<appSettings>

<add key="ConnectionTimeout" value="15" />

</appSettings>
```


## <a name="see-also"></a>请参阅

[数据迁移助手下载](https://www.microsoft.com/download/details.aspx?id=53595)
