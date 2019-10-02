---
title: 在 SSMS 中使用自定义报表监视 Python 和 R 脚本执行
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/17/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 549cdcd35b939b2247b14817271e3d1063fab1e0
ms.sourcegitcommit: fd3e81c55745da5497858abccf8e1f26e3a7ea7d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2019
ms.locfileid: "71714391"
---
# <a name="monitor-python-and-r-script-execution-using-custom-reports-in-sql-server-management-studio"></a>使用 SQL Server Management Studio 中的自定义报表监视 Python 和 R 脚本执行
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

使用 SQL Server Management Studio （SSMS）中的自定义报表来监视外部脚本（Python 和 R）的执行情况、使用的资源、诊断问题，以及 SQL Server 机器学习服务优化性能。

在这些报表中, 可以查看详细信息, 例如:

- 活动 Python 或 R 会话
- 实例的配置设置
- 机器学习作业的执行统计信息
- R Services 的扩展事件
- 当前实例上安装的 Python 或 R 包

本文介绍如何安装和使用为 SQL Server 机器学习服务提供的自定义报表。

有关 SQL Server Management Studio 中的报表的详细信息，请参阅[Management Studio 中的自定义报表](../../ssms/object/custom-reports-in-management-studio.md)。

## <a name="how-to-install-the-reports"></a>如何安装报表

报表使用 SQL Server Reporting Services 进行设计，但可以直接从 SQL Server Management Studio 使用。 无需在 SQL Server 实例上安装 Reporting Services。

若要使用这些报告，请执行以下步骤：

1. 从 GitHub 下载适用于 SQL Server 机器学习服务的[SSMS 自定义报表](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports)。

2. 将报表复制到 Management Studio

    1. 找到 SQL Server Management Studio 使用的自定义报表文件夹。 默认情况下，自定义报表存储在此文件夹中 **（其中，用户名为**Windows 用户名）：

        `C:\Users\user_name\Documents\SQL Server Management Studio\Custom Reports`

       还可以指定其他文件夹，或创建子文件夹。

    2. 复制 *。已下载到 "自定义报表" 文件夹的 RDL 文件。

3. 在 Management Studio 中运行报表

    1. 在 Management Studio 中，右键单击要在其中运行报表的示例的“数据库” 节点。

    2. 单击“报表”，然后单击“自定义报表”。

    3. 在“打开文件” 对话框中，找到自定义报表文件夹。

    4. 选择某个下载的 RDL 文件，然后单击“打开”。

## <a name="reports"></a>报表

[GitHub 中的 SSMS 自定义报告存储库](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports)包含以下报表：

| 报告 | 描述 |
|-|-|
| 活动会话 | 当前连接到 SQL Server 实例并运行 Python 或 R 脚本的用户。 |
| 配置 | Python 或 R 运行时机器学习服务和属性的安装设置。 |
| 配置实例 | 配置机器学习服务。 |
| 执行统计信息 | 机器学习 services 的执行统计信息。 例如，你可以获取外部脚本执行的总数和并行执行数。 |
| 扩展事件 | 可用于更深入地了解外部脚本执行的扩展事件。 |
| 包 | 列出 SQL Server 实例上安装的 R 或 Python 包及其属性，如版本和名称。 |
| 资源使用情况 | 查看 SQL Server 和外部脚本执行的 CPU、内存、IO 使用情况。 还可以查看外部资源池的内存设置。 |

## <a name="next-steps"></a>后续步骤

- [使用动态管理视图（Dmv）监视 SQL Server 机器学习服务](monitor-sql-server-machine-learning-services-using-dynamic-management-views.md)
- [R Services 的扩展事件](../r/extended-events-for-sql-server-r-services.md)
