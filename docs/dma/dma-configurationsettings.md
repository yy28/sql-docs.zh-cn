---
title: 为数据迁移助手配置设置 (SQL Server) |Microsoft Docs
description: 了解如何通过更新配置文件中的值来配置数据迁移助手的设置
ms.custom: ''
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: HJToland3
ms.author: rajpo
ms.openlocfilehash: e94760c23a0c8621ba1c50f34162466f21f833c0
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345237"
---
# <a name="configure-settings-for-data-migration-assistant"></a>为数据迁移助手配置设置

您可以通过在 cmd.exe .config 文件中设置配置值来微调数据迁移助手的某些行为。 本文介绍关键配置值。

你可以在计算机上的以下文件夹中找到数据迁移助手桌面应用程序和命令行实用工具的 cmd.exe .config 文件。

- 桌面应用程序

  % ProgramFiles%\\Microsoft 数据迁移助手\\

- 命令行实用工具

  % ProgramFiles%\\Microsoft 数据迁移助手\\dmacmd 

请确保在进行任何修改之前保存原始配置文件的副本。 进行更改后, 重新启动数据迁移助手, 以使新的配置值生效。

## <a name="number-of-databases-to-assess-in-parallel"></a>要并行评估的数据库数

数据迁移助手并行评估多个数据库。 在评估期间数据迁移助手提取数据层应用程序 (dacpac) 以了解数据库架构。 如果在同一台服务器上并行评估了多个数据库, 则此操作可能会超时。 

从数据迁移助手 v2.0 开始, 可以通过设置 parallelDatabases 配置值进行控制。 默认值为8。

```
<advisorGroup>

<workflowSettings>

<assessment parallelDatabases="8" />

</workflowSettings>

</advisorGroup>
```




## <a name="number-of-databases-to-migrate-in-parallel"></a>要并行迁移的数据库数

数据迁移助手在迁移登录名之前并行迁移多个数据库。 在迁移过程中, 数据迁移助手将备份源数据库, 还可以选择复制备份, 然后在目标服务器上还原备份。 选择多个数据库进行迁移时, 可能会遇到超时故障。 

从数据迁移助手 v2.0 开始, 如果你遇到此问题, 则可以减少 parallelDatabases 配置值。 可以增大此值, 以减少总体迁移时间。

```
<advisorGroup>

<workflowSettings>

<migration parallelDatabases="8″ />

</workflowSettings>

</advisorGroup>
```


## <a name="dacfx-settings"></a>DacFX 设置

在评估期间, 数据迁移助手提取数据层应用程序 (dacpac) 以了解数据库架构。 对于极大型数据库, 或如果服务器负载过大, 此操作可能会失败并出现超时。 从数据迁移 v1.0 开始, 可以修改以下配置值以避免错误。 

> [!NOTE]
> 默认情况&lt;下&gt; , 将对整个 dacfx 条目进行注释。 删除注释, 然后根据需要修改值。

- commandTimeout

   此参数设置 IDbCommand 属性, 以*秒为单位*。 (默认值 = 60)

- databaseLockTimeout

   此参数等效于[设置锁定\_超时\_超时期限](../t-sql/statements/set-lock-timeout-transact-sql.md)(以*毫秒为单位)* 。 (默认值 = 5000)

- maxDataReaderDegreeOfParallelism

  此参数设置要使用的 SQL 连接池连接的数量。 (默认值 = 8)

```
<advisorGroup>

<advisorSettings>

<dacFx  commandTimeout="60" databaseLockTimeout="5000"
maxDataReaderDegreeOfParallelism="8"/>

</advisorSettings>

</advisorGroup>
```

## <a name="stretch-database-recommendation-threshold"></a>Stretch Database:建议阈值

利用[SQL Server Stretch Database](https://docs.microsoft.com/sql/sql-server/stretch-database/stretch-database), 你可以将热和冷事务数据从 Microsoft SQL Server 2016 动态拉伸到 Azure。 Stretch Database 以包含大量冷数据的事务数据库为目标。 Stretch Database 建议: 在存储功能建议下, 首先识别它认为将从此功能中受益的表, 然后标识为启用此功能所需进行的更改。

从数据迁移助手 v2.0 开始, 你可以使用 recommendedNumberOfRows 配置值控制表的此阈值, 以便符合 Stretch Database 功能。 默认值为100000行。 如果要分析更小的表的拉伸功能, 请相应地减小值。

```
<advisorGroup>

<advisorSettings>

<stretchDBAdvisor  recommendedNumberOfRows="100000" />

</advisorSettings>

</advisorGroup>
```


## <a name="sql-connection-timeout"></a>SQL 连接超时

可以通过将连接超时值设置为指定的秒数, 在运行评估或迁移时控制源和目标实例的[SQL 连接](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectiontimeout(v=vs.110).aspx)超时。 默认值为 15 秒。

```
<appSettings>

<add key="ConnectionTimeout" value="15" />

</appSettings>
```

## <a name="ignore-error-codes"></a>忽略错误代码

每个规则的标题中都有错误代码。 如果不需要规则并想要忽略它们, 请使用 ignoreErrorCodes 属性。 可以指定忽略单个错误或多个错误。 若要忽略多个错误, 请使用分号, 例如, ignoreErrorCodes = "46010; 71501"。 默认值为 71501, 此值与对象引用系统对象 (如过程、视图等) 时标识的未解析引用关联。

```
<workflowSettings>

<assessment parallelDatabases="8" ignoreErrorCodes="71501" />

</workflowSettings>
```

## <a name="see-also"></a>请参阅

[数据迁移助手下载](https://www.microsoft.com/download/details.aspx?id=53595)
