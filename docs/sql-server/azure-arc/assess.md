---
title: 为启用了 Azure Arc 的 SQL Server 配置 SQL 评估
titleSuffix: ''
description: 为启用了 Azure Arc 的 SQL Server 实例配置按需评估
author: anosov1960
ms.author: sashan
ms.reviewer: mikeray
ms.date: 09/10/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 59a6ff65e25878aefe08cfd87bf1f9e36da7366b
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "90942461"
---
# <a name="configure-on-demand-sql-assessment-for-azure-arc-enabled-sql-server-instance"></a>为启用了 Azure Arc 的 SQL Server 实例配置按需 SQL 评估

可以按照以下步骤为 SQL Server 实例启用 SQL 评估。

## <a name="prerequisites"></a>必备知识

* SQL Server 实例已连接到 Azure Arc。按照以下说明[将 SQL Server 实例载入已启用 Arc 的 SQL Server](connect.md)。

* 在计算机上安装和配置 MMA 扩展。 按照以下说明[安装 Microsoft Monitoring Agent (MMA)](configure-advanced-data-security.md#install-microsoft-monitoring-agent-mma)。 有关详细信息，请参阅 [Log Analytics 代理](https://docs.microsoft.com/azure/azure-monitor/platform/log-analytics-agent)。

* 你的 SQL Server 启用了 [TCP/IP 协议](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)。

* 如果你正在操作 SQL Server 的命名实例，则 [SQL Server 浏览器](../../tools/configuration-manager/sql-server-browser-service.md)正在运行。

* 你已查看[服务中心按需评估先决条件](https://docs.microsoft.com/services-hub/health/assessment-prereq-docs#on-demand-assessment-prerequisite-documents)处的 SQL Server 文档。

## <a name="enable-on-demand-sql-assessment"></a>启用按需 SQL 评估

1. 打开你的 SQL Server – Azure Arc 资源并在左侧菜单中选择“环境运行状况”。

   ![SQL 评估选择](media/assess/sql-assessment-heading-sql-server-arc.png)

1. 在数据收集计算机上指定工作目录。 在收集和分析期间，数据临时存储在该文件夹下。 如果该文件夹不存在，将自动创建它。

1. 单击“下载配置脚本”并将下载的脚本复制到目标计算机。

1. 启动 powershell.exe 的管理员实例，并执行以下操作之一： 
   * 如果你使用域帐户，请运行以下命令。 系统会提示你输入用户帐户和密码。 

      ```powershell
      Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
      & '.\AddSqlAssessment.ps1'
      ```

    * 如果你使用 MSA 帐户，请运行以下命令。

      ```powershell
      Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
      & '.\AddSqlAssessment.ps1' -ManagedServiceAccountName <MSA account name>
      ```

   > [!NOTE]
   > 该脚本会计划名为 SQLAssessment 的任务，使其在运行上一个脚本后一小时内运行，然后每 7 天运行一次。 可以从任务计划程序库 >“Microsoft”>“Operations Management Suite”>“AOI”*** >“评估”>“SQLAssessment”修改任务，使其在其他日期和时间运行，甚至强制其立即运行。 此任务会触发数据收集。

## <a name="view-the-assessment-results"></a>查看评估结果

Log Analytics 中结果准备就绪之前，“环境运行状况”边栏选项卡上的“查看 SQL 评估结果”按钮处于禁用状态。 激活该按钮后，可以单击它来查看结果。 在目标计算机上处理数据文件后，最多可能需要 2 小时才能在 Log Analytics 中看到结果。

![SQ：评估结果](media/assess/sql-assessment-results.png)

通过检查工作文件夹中的文件，可以在收集计算机上查看数据处理状态。 计划的任务完成后，应会看在工作目录中看到几个具有 new. 前缀的文件：

![数据文件已就绪](media/assess/sql-assessment-data-files-ready.png)

Microsoft Monitoring Agent 每 15 分钟扫描一次工作文件夹，查找 new.* 文件，然后将数据发送到 Log Analytics 工作区。 上传文件后，前缀将从 new. 变为 processed.：

![已处理数据文件](media/assess/sql-assessment-data-files-processed.png)

## <a name="next-steps"></a>后续步骤

查看[服务中心按需评估先决条件](https://docs.microsoft.com/services-hub/health/assessment-prereq-docs#on-demand-assessment-prerequisite-documents)处的 SQL Server 文档，以了解详细信息。
