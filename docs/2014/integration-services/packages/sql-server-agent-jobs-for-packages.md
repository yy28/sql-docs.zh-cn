---
title: 包的 SQL Server 代理作业 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- jobs [Integration Services]
- automatic package execution
- scheduling packages [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: ecf7a5f9-b8a7-47f1-9ac0-bac07cb89e31
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7a4b9cd5eaad7b51f7cc3d2a0c73bea3f23fd542
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62767169"
---
# <a name="sql-server-agent-jobs-for-packages"></a>包的 SQL Server 代理作业
  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理可以计划并且自动执行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。 您可以计划部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器的包，以及存储在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包存储区和文件系统中的包。  
  
## <a name="sections-in-this-topic"></a>本主题的内容  
 本主题包含以下各节：  
  
-   [在 SQL Server 代理中计划作业](#jobs)  
  
-   [计划 Integration Services 包](#packages)  
  
-   [对计划的包进行故障排除](#trouble)  
  
##  <a name="jobs"></a> Scheduling Jobs in SQL Server Agent  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装的服务，使您能够通过运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业自动执行任务和计划任务的执行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务必须处于运行状态，作业才能自动运行。 有关详细信息，请参阅 [Configure SQL Server Agent](../../ssms/agent/configure-sql-server-agent.md)。  
  
 在您连接到 **的实例时，** “SQL Server 代理” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 节点将出现在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的对象资源管理器中。  
  
 若要自动执行某一重复发生的任务，您可以通过使用 **“新建作业”** 对话框创建某个作业。 有关详细信息，请参阅 [执行作业](../../ssms/agent/implement-jobs.md)。  
  
 创建该作业后，必须至少添加一个步骤。 一个作业可以包括多个步骤，并且每个步骤可以执行不同的任务。 有关详细信息，请参阅 [Manage Job Steps](../../ssms/agent/manage-job-steps.md)。  
  
 在创建作业和作业步骤后，可以创建一个运行作业的计划。 不过，您还可以创建手动运行的无人参与的作业。 有关详细信息，请参阅 [创建计划并将计划附加到作业](../../ssms/agent/create-and-attach-schedules-to-jobs.md)。  
  
 可以通过设置通知选项来增强作业，如指定在作业完成时向某个操作员发送电子邮件或添加警报。 有关详细信息，请参阅 [“警报”](../../ssms/agent/alerts.md)。  
  
##  <a name="packages"></a> Scheduling Integration Services Packages  
 在您创建一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业以便计划 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包后，必须至少添加一个步骤，并将该步骤的类型设置为 **“SQL Server Integration Services 包”**。 一个作业可以包括多个步骤，并且每个步骤可以运行不同的包。  
  
 从作业步骤中运行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包类似于使用 **dtexec**(dtexec.exe) 和 **DTExecUI**(dtexecui.exe) 实用工具运行包。 可以在“新建作业步骤”对话框中设置运行时选项，而不是使用命令行选项或“执行包实用工具”对话框来设置包的运行时选项。 有关运行包的选项的详细信息，请参阅 [dtexec Utility](dtexec-utility.md)。  
  
 有关详细信息，请参阅 [使用 SQL Server 代理计划包](../schedule-a-package-by-using-sql-server-agent.md)。  
  
 有关演示如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理来运行包的视频，请观看 MSDN 库中的视频主页[操作说明：使用 SQL Server 代理自动执行包（SQL Server 视频）](https://go.microsoft.com/fwlink/?LinkId=141771)。  
  
##  <a name="trouble"></a> 故障排除  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业步骤可能无法启动某个包，即便该包可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中以及从命令行成功运行。 该问题有一些常见的原因和一些推荐的解决方法。 有关详细信息，请参阅下列资源。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 知识库文章： [当从 SQL Server 代理作业步骤调用 SSIS 包时 SSIS 包不运行](https://support.microsoft.com/kb/918760)  
  
-   MSDN 库中的视频[排除故障：使用 SQL Server 代理执行包（SQL Server 视频）](https://go.microsoft.com/fwlink/?LinkId=141772)。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业步骤启动某个包后，该包可能无法执行，或者包可能成功运行但出现意外结果。 可以使用下列工具来解决这些问题。  
  
-   对于存储在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] MSDB 数据库、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包存储区或本地计算机上的文件夹中的包，可以使用 **“日志文件查看器”** 以及在包执行期间生成的任何日志和调试转储文件。  
  
     **若要使用日志文件查看器，请执行下列操作。**  
  
    1.  右键单击对象资源管理器中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业，然后单击“查看历史记录”。  
  
    2.  在 **“日志文件摘要”** 框中，找到 **“消息”** 列中标有 **“作业失败”** 消息的作业执行。  
  
    3.  展开该作业节点，然后单击作业步骤查看 **“日志文件摘要”** 框下方区域中的消息的详细信息。  
  
-   对于存储在 SSISDB 数据库中的包，也可以使用 **“日志文件查看器”** 以及在包执行期间生成的任何日志和调试转储文件。 此外，还可以使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器的报告。  
  
     **若要查找报告中与作业执行关联的包执行的信息，请执行以下操作。**  
  
    1.  按照如上步骤查看作业步骤消息的详细信息。  
  
    2.  找到消息中列出的执行 ID。  
  
    3.  在对象资源管理器中，展开“Integration Services 目录”节点。  
  
    4.  右键单击 SSISDB，依次指向“报表”和“标准报表”，然后单击“所有执行”。  
  
    5.  在 **“所有执行”** 报告的 **ID** 列中，找到该执行 ID。 单击 **“概述”**、 **“所有消息”** 或 **“执行性能”** ，查看有关此包执行的信息。  
  
         有关“概述”、“所有消息”和“执行性能”报告的详细信息，请参阅 [Reports for the Integration Services Server](../reports-for-the-integration-services-server.md)。  
  
## <a name="external-resources"></a>外部资源  
  
-   [网站上的知识库文章：](https://support.microsoft.com/kb/918760)当从 SQL Server 代理作业步骤调用 SSIS 包时 SSIS 包不运行 [!INCLUDE[msCoName](../../includes/msconame-md.md)]  
  
-   MSDN 库中的视频[排除故障：使用 SQL Server 代理执行包（SQL Server 视频）](https://go.microsoft.com/fwlink/?LinkId=141772)  
  
-   MSDN 库中的视频[操作说明：使用 SQL Server 代理自动执行包（SQL Server 视频）](https://go.microsoft.com/fwlink/?LinkId=141771)  
  
-   mssqltips.com 上的技术文章 [Checking SQL Server Agent jobs using Windows PowerShell](https://go.microsoft.com/fwlink/?LinkId=165675)（使用 Windows PowerShell 检查 SQL Server 代理作业）  
  
-   mssqltips.com 上的技术文章 [Auto alert for SQL Agent jobs when they are enabled or disabled](https://go.microsoft.com/fwlink/?LinkId=165676)（在 SQL 代理作业启用或禁用时针对它们的自动警报）  
  
-   mssqltips.com 上的博客文章 [配置 SQL 代理作业以便写入 Windows 事件日志](https://go.microsoft.com/fwlink/?LinkId=220745)。  
  
  
