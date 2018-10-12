---
title: 虚拟化 SQL Server 2019 CTP 2.0 中的外部数据 | Microsoft Docs
description: ''
author: Abiola
ms.author: aboke
manager: craigg
ms.date: 09/24/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: polybase
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: dfd4460c51e4aeef8e9faff8479e7edf2678c35f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47627315"
---
# <a name="use-the-data-external-table-wizard-with-external-tables"></a>对外部表使用数据外部表向导

SQL Server 2019 CTP 2.0 的重要方案之一是能够虚拟化数据。  此过程允许将数据保留在其原始位置，但可以虚拟化 SQL Server 实例中的数据，以便可以对这些数据进行查询，如同 SQL Server 中的任何其他表一样。 这将最大限度地减少对 ETL 进程的需要。 可以使用 Polybase 连接器。 有关数据虚拟化的详细信息，请参阅 [PolyBase 入门](polybase-guide.md)文档。

## <a name="launch-the-external-table-wizard"></a>启动外部表向导

使用在部署脚本末尾获得的 IP 地址/端口号 (31433) 连接到主实例。 在对象资源管理器中展开数据库节点。 然后从现有 SQL Server 实例中选择要将数据虚拟化到的数据库之一。 右键单击“数据库”，然后从上下文菜单中选择“创建外部表”。 这将启动虚拟化数据向导。 也可以通过键入 Ctrl+Shift+P（在 Windows 中）和 Cmd+Shift+P（在 Mac 中），从命令面板启动虚拟化数据向导。

![虚拟化数据向导](media/data-virtualization/virtualize-data-wizard.png)
## <a name="select-a-data-source"></a>选择数据源

如果从其中一个数据库启动该向导，则可以看到目标下拉列表进行自动填充。 也可以选择在此屏幕上输入或更改目标数据库。 该向导支持的外部数据源类型为 SQL Server 和 Oracle。

> [!NOTE]
>默认情况下将突出显示 SQL Server


![选择数据源](media/data-virtualization/select-data-source.png)

单击“下一步”以继续执行向导中的下一步，即设置数据库主密钥。

## <a name="create-database-master-key"></a>创建数据库主密钥

在此步骤中，将要求你创建数据库主密钥。 创建主密钥是必需的，因为这样可以保护外部数据源所使用的凭据。 请为主密钥选择一个强密码。 你还应该使用 BACKUP MASTER KEY 备份主密钥，并将备份存储于另外一个安全的位置中。

![创建数据库主密钥](media/data-virtualization/virtualize-data-master-key.png)

> [!IMPORTANT]
> 如果已有数据库主密钥，则输入字段将受到限制，可能会跳过此步骤。你只需单击“下一步”即可转到向导中的下一页。

> [!NOTE]
> 如果不选择强密码，则该向导将返回上一步。 这是我们将在未来版本中修复的已知问题，因此更为直观。

## <a name="enter-the-external-data-source-credentials"></a>输入外部数据源凭据

在此步骤中，请输入外部数据源和凭据详细信息。 此步骤会创建外部数据源对象，然后使用数据库对象的凭据连接到数据源。 提供外部数据源的名称（示例：Test）并提供外部数据源 SQL Server 连接详细信息 - 要在该服务器上创建外部数据源所使用的服务器名称数据库名称。

下一步是配置凭据，因此，请提供凭据名称，这是数据库范围的凭据的名称（示例：TestCred），该凭据用于安全地存储正在创建的外部数据源的登录信息并提供用于连接到数据源的用户名和密码。

![外部数据源凭据](media/data-virtualization/data-source-credentials.png)

## <a name="external-data-table-mapping"></a>外部数据表映射

在下一个窗口中，你将能够选择想要创建外部视图的表。 选择父数据库也会包括所有子表。 选择表后，右侧将显示映射表。 此处，你可以进行任何“类型”更改或更改所选外部表本身的名称。

![外部数据源凭据](media/data-virtualization/data-table-mapping.png)

> [!NOTE]
>双击另一个所选表将更改映射视图。

> [!IMPORTANT]
>外部表工具尚不支持照片类型。 在该工具中创建照片类型的外部视图会在创建表后引发错误。 但仍会创建表。

## <a name="summary"></a>“摘要”

此步骤提供所选对象的摘要。 会提供数据库范围的凭据的名称以及将在目标数据库中创建的外部数据源对象。 在此步骤中，可以选择“生成脚本”（这会在 T-SQL 中编写语法脚本以创建外部数据源）或“创建”（这会创建外部数据源对象）。

![“摘要”屏幕](media/data-virtualization/virtualize-data-summary.png)

如果单击“创建”，你将能够看到目标数据库中创建的外部数据源对象。

![外部数据源](media/data-virtualization/external-data-sources.png)

如果单击“生成脚本”，你将看到为创建外部数据源对象生成的 T-SQL 查询。

![生成脚本](media/data-virtualization/generated-script.png)

> [!NOTE]
> “生成脚本”应仅在向导的最后一页中显示。 目前显示在所有页面中。

## <a name="next-steps"></a>后续步骤

有关 SQL Server 大数据群集和相关方案的详细信息，请参阅[什么是 SQL Server 大数据群集？](../../big-data-cluster/big-data-cluster-overview.md)。
