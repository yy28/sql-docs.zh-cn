---
title: 计划在 Linux 上使用 cron 的 SSIS 包 |Microsoft Docs
description: 本文介绍如何安排与 cron 服务在 Linux 上的 SQL Server Integration Services (SSIS) 包。
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 6d78190f5c6acf1f5dc8bfaccbf072a290faa908
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66705312"
---
# <a name="schedule-sql-server-integration-services-package-execution-on-linux-with-cron"></a>计划 SQL Server Integration Services 包在 Linux 上的使用 cron 执行

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

当您在 Windows 上运行 SQL Server Integration Services (SSIS) 和 SQL Server 时，可以通过使用 SQL Server 代理自动执行 SSIS 包。 在 Linux 上运行 SQL Server 和 SSIS，但是，SQL Server 代理程序实用程序不可用来计划在 Linux 上的作业。 相反，您使用 cron 服务，这广泛用于在 Linux 平台上自动执行包。

本文提供了示例，演示如何自动执行 SSIS 包的执行。 编写示例是在 Red Hat Enterprise 上运行。 代码是针对其他 Linux 发行版，例如 Ubuntu 类似。

## <a name="prerequisites"></a>先决条件

使用 cron 服务运行作业之前，检查它您的计算机上运行。

若要检查 cron 服务的状态，请使用以下命令： `systemctl status crond.service`。

如果该服务未处于活动状态 （即，它未运行），请查阅您的管理员安装并正确配置 cron 服务。

## <a name="create-jobs"></a>创建作业

Cron 作业是可配置为按指定时间间隔定期运行的任务。 作业可以是简单，通常会在控制台中直接键入，或运行方式的 shell 脚本的命令。

轻松管理和维护目的，我们建议您将在包执行的命令放在脚本中包含的描述性名称。

下面是有关运行包的简单的 shell 脚本的示例。 它包含只能有一个命令，但可以根据需要添加更多命令。

```bash
# A simple shell script that contains a simple package execution command
# Script name: SSISpackageName.daily

/opt/ssis/bin/dtexec /F yourSSISpackageName.dtsx >> $HOME/tmp/out 2>&1
```

## <a name="schedule-jobs-with-the-cron-service"></a>使用 cron 服务计划作业

定义你的作业后，您可以将它们自动运行使用 cron 服务计划。

若要添加的 cron 运行作业，请从 crontab 文件中添加作业。 若要在其中可以添加或更新作业的编辑器中打开 crontab 文件，请使用以下命令： `crontab -e`。

若要计划每日凌晨 2:10 运行前面所述的作业，请将以下行添加到 crontab 文件：

```
# run <SSIS package name> at 2:10 AM every day
10 2 \* \* \* $/HOME/SSIS/jobs/SSISpackageName.daily
```

保存 crontab 文件，然后退出编辑器。

若要了解示例命令的格式，请查看以下部分中的信息。
 
## <a name="format-of-a-crontab-file"></a>从 crontab 文件的格式

下图显示了添加到 crontab 文件的作业行的格式说明。

![从 crontab 文件中的条目的格式描述](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-job-definition.png)

若要获取 crontab 文件格式的更详细的说明，请使用以下命令： `man 5 crontab`。

下面是输出，以帮助说明本文中的示例的部分示例：

![从 crontab 格式的详细部分的说明](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-crontab-format.png)

## <a name="related-content-about-ssis-on-linux"></a>有关在 Linux 上的 SSIS 的相关的内容
-   [提取、 转换和加载使用 SSIS 的 Linux 上的数据](sql-server-linux-migrate-ssis.md)
-   [在 Linux 上安装 SQL Server Integration Services (SSIS)](sql-server-linux-setup-ssis.md)
-   [使用 ssis conf 配置 Linux 上的 SQL Server Integration Services](sql-server-linux-configure-ssis.md)
-   [限制和 Linux 上的 SSIS 的已知的问题](sql-server-linux-ssis-known-issues.md)
