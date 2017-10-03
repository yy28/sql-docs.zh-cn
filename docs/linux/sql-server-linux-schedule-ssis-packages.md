---
title: "计划在 Linux 上使用 cron 的 SSIS 包 |Microsoft 文档"
description: "这篇文章演示逼 cron 服务在 Linux 上的 SQL Server Integration Services 包。"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.date: 09/26/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: integration-services
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 31d5fb63a9c2a4d8825aa39c6fa7e3377ddc8d91
ms.contentlocale: zh-cn
ms.lasthandoff: 09/27/2017

---
# <a name="schedule-sql-server-integration-services-package-execution-on-linux-with-cron"></a>计划 SQL Server Integration Services 包执行在 Linux 上的使用 cron

当在 Windows 上运行的是 SQL Server Integration Services (SSIS) 和 SQL Server 时，你可以使用 SQL Server 代理自动 SSIS 包的执行。 当在 Linux 上运行的是 SQL Server 和 SSIS 时，但是，SQL Server 代理程序实用工具不可用来安排在 Linux 上的作业。 改为使用**Cron**广泛使用的 Linux 平台自动执行包的服务。

本文提供了演示如何自动执行 SSIS 包的示例。 示例是编写在 Red Hat Enterprise 上运行的。 代码将类似 Ubuntu 等其他 Linux 分发版。

## <a name="prerequisites"></a>先决条件

你可以使用 Cron 服务运行作业之前，你必须先检查 Cron 服务是否正在运行您的计算机上。

使用以下命令来检查 Cron 服务的状态。

`systemctl status crond.service`

如果服务处于不活动状态 （即，未运行），请查阅您的管理员设置和正确配置 Cron 服务。

## <a name="create-jobs"></a>创建作业

Cron 作业是可配置为按指定间隔定期运行的任务。 作业可以是简单，通常将直接在控制台中键入，或者以一个 shell 脚本运行的命令。

出于方便地管理和维护目的，建议你先将包执行命令放入具有描述性的名称的脚本。

下面是仅包含单个命令运行包的 shell 脚本的一个简单示例。 你可以根据需要添加命令的详细信息。

```
# A simple shell script that contains a simple package execution command
# Script name: SSISpackageName.daily

/opt/ssis/bin/dtexec /F yourSSISpackageName.dtsx >> $HOME/tmp/out 2>&1
```

## <a name="schedule-jobs-with-the-cron-service"></a>使用 Cron 服务计划作业

定义你的作业后，可以安排它们自动使用 Cron 服务运行。

若要添加为 Cron 运行你的作业，你需要添加中的作业`crontab`文件。 若要打开`crontab`文件在编辑器中，你可以添加或更新作业，请使用以下命令：

`crontab -e`

若要计划每日凌晨 2:10 运行前面所述的作业，添加以下行将对`crontab`文件：

```
# run SSIS package Name at 2:10AM every day
10 2 \* \* \* $/HOME/SSIS/jobs/SSISpackageName.daily
```

保存`crontab`文件并退出编辑器。

若要了解示例命令的格式，请查看下列部分中的信息。
 
## <a name="format-of-a-crontab-file"></a>Crontab 文件的格式

下图显示添加到作业行格式描述`crontab`文件。

![Crontab 文件中的条目的格式描述](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-job-definition.png)

若要获取更加详细的说明`crontab`文件格式，请使用以下命令：

`man 5 crontab`

下面是输出的部分示例，以帮助解释此文章中的示例：

![详细的部分 crontab 格式说明](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-crontab-format.png)

