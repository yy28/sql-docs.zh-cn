---
title: SQL Server 升级为在数据库实验助手中创建分析报表
description: 在数据库实验助手中创建分析报表
ms.custom: ''
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
ms.openlocfilehash: d53d8734e0c01fa2056b9d560f3bc65b7f64d9a9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68058976"
---
# <a name="create-analysis-reports-in-database-experimentation-assistant"></a>在数据库实验助手中创建分析报表

重播源跟踪在这两个目标服务器上的后，可以生成分析报告，在数据库实验助手 (DEA)。 分析报表帮助您深入了解建议的更改的性能影响。

## <a name="create-an-analysis-report"></a>创建分析报表

在 DEA，选择菜单图标。 在展开的菜单中，选择**分析报表**清单图标的旁边。

![分析菜单](./media/database-experimentation-assistant-create-report/dea-create-reports-menu.png)

下**分析报表**，选择**新分析报告**。

![新的分析报告菜单](./media/database-experimentation-assistant-create-report/dea-create-reports-new-report.png)

输入或选择以下信息：

- **报表名称**:输入您的报表的名称。 使用报表名称同时 a 和 B 数据库。 例如：*A （或 B）*  + *报表名称* + *唯一标识符*。 
- **服务器名称**：输入想要包括在 A，在服务器计算机的名称 B 和分析数据库。
- **SQL Server 实例名称**:输入要用于报表的 SQL Server 实例的名称。
- **对于源服务器的跟踪**:输入 SQL Server (2008 R2) 的第一个跟踪 (.trc) 文件。
- **目标服务器的跟踪**:输入目标 SQL Server (2014) 第一个.trc 文件。

![新的分析报表页](./media/database-experimentation-assistant-create-report/dea-create-reports-inputs.png)

## <a name="generate-a-report"></a>生成报告

输入或选择所需的信息后**新的分析报表**页上，选择**启动**开始创建报表。 如果您输入的信息是有效的会创建分析报表。 否则，具有无效的信息的文本框将用红色突出显示。 请确保已输入正确的值，然后选择**启动**。 

生成新的分析报告。 分析数据库遵循的命名方案分析 +*用户指定报表名称* + *唯一标识符*。

## <a name="frequently-asked-questions-about-analysis-reports"></a>分析报表有关的常见问题

### <a name="what-does-my-analysis-report-tell-me"></a>我的分析报表会告诉什么内容我？
    
DEA 使用的统计测试来分析你的工作负荷，确定如何每个查询已运行目标 1 中的目标 2。 它提供用于每个查询的性能详细信息。 了解有关在 DEA[开始](database-experimentation-assistant-get-started.md)。
    
### <a name="can-i-create-a-new-analysis-report-while-another-report-is-being-generated"></a>生成另一个报表时是否可以创建新的分析报告？
    
否。  目前，每次以防止冲突，可以生成只有一个报告。 但是，可以运行多个对应一个捕获和重播在相同的时间。

### <a name="i-upgraded-dea-to-version-20-can-i-still-view-and-use-my-old-reports"></a>DEA 升级到版本 2.0。 我仍查看和使用我的旧报表？
    
是。 若要查看以前生成的报告，必须更新报表的架构。 有关详细信息，请参阅[DEA 2.0:更新数据库架构中 DEA 分析报告的](https://blogs.msdn.microsoft.com/datamigration/2017/03/24/dea-2-0-updating-db-schema-for-analysis-report-in-the-database-experimentation-assistant/)。
    
### <a name="can-i-generate-an-analysis-report-by-using-the-command-prompt"></a>可以通过使用命令提示符生成分析报告？
    
是。 可以生成分析报告，在命令提示符处。 然后可以在 UI 中查看报表。 有关详细信息，请参阅[在命令提示符下运行](database-experimentation-assistant-run-command-prompt.md)。
    
## <a name="troubleshoot-analysis-reports"></a>分析报表故障排除

###  <a name="what-security-permissions-do-i-need-to-generate-and-view-an-analysis-report-on-my-server"></a>需要什么安全权限来生成和查看分析报告，在我的服务器上？
    
登录到 DEA 的用户必须在分析服务器上具有系统管理员权限。 如果用户是组的一部分，请确保组具有 sysadmin 权限。

|可能的错误|解决方案|  
|---|---|  
|无法连接到数据库。 请确保您具有分析和查看报表的 sysadmin 权限。|您可能不具有到服务器或数据库的访问或系统管理员权限。 确认登录权限，然后重试。|  
|无法生成**报表名称**服务器上**服务器名称**。 有关详细信息，请**报表名称**报表。|您可能没有生成新的报表所需的 sysadmin 权限。 若要查看详细的错误，请选择误码扩展报表并检查 %temp%中的日志\\DEA。|  
|当前用户不具有所需的权限运行此操作。 请确保具有执行跟踪和分析的报告的 sysadmin 权限。|无需生成新报告的 sysadmin 权限。|  

### <a name="i-cant-connect-to-the-computer-running-sql-server"></a>我无法连接到运行 SQL Server 的计算机
    
- 确认运行 SQL Server 的计算机的名称有效。 若要确认，请尝试使用 SQL Server Management Studio (SSMS) 连接到服务器。
- 确认你的防火墙配置不会阻止连接到运行 SQL Server 的计算机。
- 确认用户具有所需的用户权限。 

可以看到在 %temp%中的日志中的更多详细信息\\DEA。 如果问题仍然存在，请与产品团队联系。

### <a name="i-see-an-error-when-i-generate-an-analysis-report"></a>我看到错误时生成的分析报表
    
Internet 访问权限是必需安装 DEA 后生成分析报告，第一次。 下载所需的统计分析的包需要 Internet 访问权限。

如果创建报表时，将发生错误，进度页显示了无法分析生成的特定步骤。 可以看到在 %temp%中的日志中的更多详细信息\\DEA。 验证具有有效的连接到的服务器所需的用户权限，然后重试。 如果问题仍然存在，请与产品团队联系。

|可能的错误|解决方案|  
|---|---|  
|RInterop 命中启动时发生错误。 检查 RInterop 日志，然后重试。|DEA 需要 internet 访问权限才能下载 R 的依赖项包。 检查 %temp%中日志 RInterop\\RInterop 和 DEA 日志 %temp%中\\DEA。 如果 RInterop 未正确初始化或不正确的 R 包的情况下它初始化，可能会在 DEA 日志中 InitializeRInterop 步骤后看到"无法生成新的分析报告"的异常。<br><br>RInterop 日志也可能显示错误，类似于"没有任何 jsonlite 包可用。" 如果你的计算机没有 internet 访问权限，则可以手动下载所需的 jsonlite R 包：<br><br><li>转到 %userprofile%\\DEARPackages 计算机的文件系统上的文件夹。 此文件夹包含为 DEA R 使用的包。</li><br><li>如果已安装的包列表中缺少 jsonlite 文件夹，则需要具有访问 internet 以下载 jsonlite 的发行版本的计算机\_从 1.4.zip [ https://cran.r-project.org/web/packages/jsonlite/index.html ](https://cran.r-project.org/web/packages/jsonlite/index.html)。</li><br><li>将.zip 文件复制到正在运行 DEA 的计算机。  提取 jsonlite 文件夹，并将其复制到 %userprofile%\\DEARPackages。 此步骤将自动安装的 jsonlite 包该文件夹应命名**jsonlite**和内容应直接在文件夹中，未一个级别。</li><br><li>再次关闭 DEA，重新打开，并尝试分析。</li><br>此外可以使用 RGUI。 转到**包** > **从 zip 安装**。 请转到前面下载的程序包并安装。<br><br>如果 RInterop 已初始化并正确设置，你应看到"安装依赖 R 包 jsonlite"RInterop 日志中。|  
|无法连接到 SQL Server 实例，请确保服务器名称正确无误，并检查已登录的用户所需的权限。|您可能不具有访问权限，或对服务器或服务器名称的用户权限不正确。| 
|RInterop 进程超时。检查 DEA 和 RInterop 日志、 停止 RInterop 进程在任务管理器中，并再试一次。<br><br>或<br><br>RInterop 处于出错状态。 停止 RInterop 进程在任务管理器中，并再试一次。|检查 %temp%中日志\\RInterop 确认错误。 删除 RInterop 过程从任务管理器之前重试。 如果问题仍然存在，请与产品团队联系。| 

### <a name="the-report-is-generated-but-data-appears-to-be-missing"></a>生成报告，但数据看起来是缺失
    
检查正在运行 SQL Server 以确认数据存在分析计算机上的数据库。 检查 analysis 数据库存在，并检查其表。 例如，检查这些表：TblBatchesA、 TblBatchesB 和 TblSummaryStats。

如果不存在数据，数据可能不具有正确复制或数据库可能已损坏。 如果只缺失了某些数据，以捕获创建跟踪文件或重播可能不具有捕获你的工作负荷准确。 如果数据存在，请检查 %temp%中的日志文件\\DEA 若要查看已记录了任何错误。 然后，重试生成分析报表。

更多的问题或反馈？ 通过提交反馈 DEA 工具通过选择左下角的笑脸图标。  

## <a name="next-steps"></a>后续步骤

- 若要了解如何查看分析报告，请参阅[查看报表](database-experimentation-assistant-view-report.md)。

- DEA 和演示的 19 分钟介绍，请观看以下视频：

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
