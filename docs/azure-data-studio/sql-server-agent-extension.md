---
title: SQL Server 代理扩展
titleSuffix: Azure Data Studio
description: 安装和使用 Azure Data Studio 的 SQL Server 代理扩展（预览版）
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 05356cc815fdba22d55ee339d60994f2c9423373
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "67959181"
---
# <a name="sql-server-agent-extension-preview"></a>SQL Server 代理扩展（预览版）

SQL Server 代理扩展（预览版）用于管理 SQL 代理作业和配置并对其进行故障排除。 此扩展当前处于预览状态。

关键操作包括：
- 列出 SQL Server 上配置的 SQL Server 代理作业
- 查看作业历史记录中的作业执行结果
- 用于启动和停止作业的基本作业控制

## <a name="install-the-sql-server-agent-extension"></a>安装 SQL Server 代理扩展

1. 若要打开扩展管理器并访问可用扩展，请选择扩展图标，或在“视图”菜单中选择“扩展”   。
2. 选择可用的扩展以查看其详细信息。

   ![安装代理](media/extensions/sql-server-agent-extension/install-sql-agent.png)

1. 选择所需的扩展并“安装”它  。
2. 选择“重新加载”以启用扩展（仅在第一次安装扩展时是必需的）  。
1. 右键单击服务器或数据库，然后选择“管理”，导航到管理仪表板  。
2. 已安装的扩展显示为管理仪表板上的选项卡：

   ![查看代理](media/extensions/sql-server-agent-extension/view-sql-agent.png)

## <a name="view-jobs"></a>查看作业

连接到 SQL Server 代理扩展时，首先看到的就是所有代理作业的列表。

   ![查看作业](media/extensions/sql-server-agent-extension/job-view.png)

## <a name="next-steps"></a>后续步骤

若要了解有关 SQL Server 代理的详细信息，请[查看我们的文档。](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent?view=sql-server-2017)


