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
ms.openlocfilehash: 107603c3c6f15ea06ffcb8b273a5f7480ae93b86
ms.sourcegitcommit: 41979c9d511b3eeb45134d30ccb0dbc6bba70f1a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/01/2018
ms.locfileid: "50757972"
---
# <a name="use-the-data-external-table-wizard-with-external-tables"></a>对外部表使用数据外部表向导

SQL Server 2019 CTP 2.0 的重要方案之一是能够虚拟化数据。 此过程允许将数据保留在其原始位置。 可以虚拟化 SQL Server 实例中的数据，以便可以对这些数据进行查询，如同 SQL Server 中的任何其他表一样。 此过程可以最大限度地减少对 ETL 进程的需求。 此过程可通过使用 PolyBase 连接器来实现。 有关数据虚拟化的详细信息，请参阅 [PolyBase 入门](polybase-guide.md)。

## <a name="start-the-external-table-wizard"></a>启动外部表向导

使用在部署脚本末尾获得的 IP 地址/端口号 (31433) 连接到主实例。 在对象资源管理器中展开数据库节点。 然后从现有 SQL Server 实例中选择一个要虚拟化数据的数据库。 右键单击该数据库，并选择“创建外部表”以启动虚拟化数据向导。 还可以从命令面板启动虚拟化数据向导。 在 Windows 中使用 Ctrl+Shift+P，或在 Mac 中使用 Cmd+Shift+P。

![虚拟化数据向导](media/data-virtualization/virtualize-data-wizard.png)
## <a name="select-a-data-source"></a>选择数据源

如果从一个数据库中启动向导，目标下拉列表框将自动填充。 也可以选择在此页面上输入或更改目标数据库。 该向导支持的外部数据源类型为 SQL Server 和 Oracle。

> [!NOTE]
>默认情况下将突出显示 SQL Server。


![选择数据源](media/data-virtualization/select-data-source.png)

选择“下一步”继续。

## <a name="create-a-database-master-key"></a>创建数据库主密钥

在此步骤中，创建数据库主密钥。 必需创建主密钥。 主密匙可以保护外部数据源所使用的凭据。 请为主密钥选择一个强密码。 此外，通过使用“BACKUP MASTER KEY”来备份主密匙。 将备份存储在另外一个安全的位置。

![创建数据库主密钥](media/data-virtualization/virtualize-data-master-key.png)

> [!IMPORTANT]
> 如果已有数据库主密钥，输入字段将受限并且你可以跳过此步骤。 选择“下一步”继续。

> [!NOTE]
> 如果不选择强密码，向导会在最后一步执行此操作。 这是一个已知问题。

## <a name="enter-external-data-source-credentials"></a>输入外部数据源凭据

在此步骤中，输入外部数据源和凭据详细信息以创建外部数据源对象。 凭据用于使数据库对象连接到数据源。 输入外部数据源的名称。 示例为 Test。 提供外部数据源 SQL Server 连接详细信息。 输入希望在其中创建外部数据源的“服务器名称”和“数据库名称”。

下一步是配置凭据。 输入凭据的名称。 此名称是数据库作用域凭据，用于安全地存储创建的外部数据源的登录信息。 示例为 TestCred。 输入用户名和密码以连接到数据源。

![外部数据源凭据](media/data-virtualization/data-source-credentials.png)

## <a name="external-data-table-mapping"></a>外部数据表映射

在下一页上，选择想为其创建外部视图的表。 选择父级数据库时，子表也包括在其中。 选择表后，映射表将显示在右侧。 可在此处更改类型。 此外，也可以更改所选外部表本身的名称。

![外部数据源凭据](media/data-virtualization/data-table-mapping.png)

> [!NOTE]
>若要更改映射视图，可双击另一个所选表。

> [!IMPORTANT]
>外部表工具不支持照片类型。 如果创建的外部视图中包含照片类型，则创建表后会出现错误。 但仍将创建此表。

## <a name="summary"></a>“摘要”

此步骤显示所选对象的摘要。 它提供数据库作用域凭据的名称以及在目标数据库中创建的外部数据源对象。 选择“生成脚本”以在 T-SQL 中编写用于创建外部数据源的语法。 选择“创建”，创建外部数据源对象。

![“摘要”屏幕](media/data-virtualization/virtualize-data-summary.png)

如果选择“创建”，可看到目标数据库中创建的外部数据源对象。

![外部数据源](media/data-virtualization/external-data-sources.png)

如果选择“生成脚本”，可看到为创建外部数据源对象生成的 T-SQL 查询。

![生成脚本](media/data-virtualization/generated-script.png)

> [!NOTE]
> “生成脚本”应仅在向导的最后一页中显示。 目前它显示在所有页面中。

## <a name="next-steps"></a>后续步骤

有关 SQL Server 大数据群集和相关方案的详细信息，请参阅[什么是 SQL Server 大数据群集？](../../big-data-cluster/big-data-cluster-overview.md)。
