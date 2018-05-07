---
title: 计划在 Linux 上使用 cron 的 SSIS 包 |Microsoft 文档
description: 本文介绍 逼 ﹚ 与 cron 服务在 Linux 上的 SQL Server Integration Services (SSIS) 包。
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.openlocfilehash: 0ef397f966196de6e47737f30d10cbf4d6f39eb4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="schedule-sql-server-integration-services-package-execution-on-linux-with-cron"></a>计划 SQL Server Integration Services 包执行在 Linux 上的使用 cron

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

当在 Windows 上运行的是 SQL Server Integration Services (SSIS) 和 SQL Server 时，你可以使用 SQL Server 代理自动 SSIS 包的执行。 当在 Linux 上运行的是 SQL Server 和 SSIS 时，但是，SQL Server 代理程序实用工具不可用来安排在 Linux 上的作业。 相反，你使用 cron 服务，广泛用于 Linux 平台自动执行包。

本文提供了演示如何自动执行 SSIS 包的示例。 编写示例是在 Red Hat Enterprise 上运行。 此代码是类似的其他 Linux 发行版，如 Ubuntu。

## <a name="prerequisites"></a>必要條件

Cron 服务用于运行作业之前，请检查以查看是否它在你的计算机上运行。

若要检查 cron 服务的状态，请使用以下命令： `systemctl status crond.service`。

如果服务处于非活动状态 （即，它未运行），请咨询管理员设置和正确配置 cron 服务。

## <a name="create-jobs"></a>创建作业

Cron 作业是可配置为按指定间隔定期运行的任务。 作业可以是简单，通常将直接在控制台中键入，或者以一个 shell 脚本运行的命令。

出于方便地管理和维护目的，我们建议您将包执行命令放在脚本，其中包含的描述性名称。

下面是有关运行包的简单的 shell 脚本的示例。 它包含只能有一个命令，但你可以根据需要添加命令的详细信息。

```bash
# A simple shell script that contains a simple package execution command
# Script name: SSISpackageName.daily

/opt/ssis/bin/dtexec /F yourSSISpackageName.dtsx >> $HOME/tmp/out 2>&1
```

## <a name="schedule-jobs-with-the-cron-service"></a>使用 cron 服务计划作业

定义你的作业后，可以安排它们自动使用 cron 服务运行。

若要添加为 cron 运行你的作业，请将作业添加 crontab 文件中。 若要在其中你可以添加或更新作业的编辑器中打开 crontab 文件，请使用以下命令： `crontab -e`。

若要计划每日在凌晨 2:10 运行前面所述的作业，请将以下行添加到 crontab 文件：

```
# run <SSIS package name> at 2:10 AM every day
10 2 \* \* \* $/HOME/SSIS/jobs/SSISpackageName.daily
```

保存 crontab 文件，然后退出编辑器。

若要了解示例命令的格式，请查看下列部分中的信息。
 
## <a name="format-of-a-crontab-file"></a>Crontab 文件的格式

下图显示添加到 crontab 文件作业行的格式描述。

![Crontab 文件中的条目的格式描述](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-job-definition.png)

若要获取的 crontab 文件格式的更详细的说明，请使用以下命令： `man 5 crontab`。

下面是输出的部分示例，以帮助解释此文章中的示例：

![详细的部分 crontab 格式说明](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-crontab-format.png)

## <a name="related-content-about-ssis-on-linux"></a>有关在 Linux 上的 SSIS 的相关的内容
-   [提取、 转换和加载使用 SSIS 的 Linux 上的数据](sql-server-linux-migrate-ssis.md)
-   [在 Linux 上安装 SQL Server Integration Services (SSIS)](sql-server-linux-setup-ssis.md)
-   [使用 ssis conf 在 Linux 上配置 SQL Server Integration Services](sql-server-linux-configure-ssis.md)
-   [限制和 Linux 上的 SSIS 的已知的问题](sql-server-linux-ssis-known-issues.md)
