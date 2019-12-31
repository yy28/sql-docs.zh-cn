---
title: 创建分析报表
description: 在数据库实验助手中创建分析报表
ms.date: 11/21/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 4d3f057ffcfb1030b473b69f96b7204b3a975613
ms.sourcegitcommit: aaa42f26c68abc2de10eb58444fe6b490c174eab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74307977"
---
# <a name="create-analysis-reports-in-database-experimentation-assistant-sql-server"></a>在数据库实验助手（SQL Server）中创建分析报表

在这两个目标服务器上重播源跟踪后，可以在数据库实验助手（DEA）中生成分析报告。 分析报告可帮助你深入了解建议的更改的性能影响。

## <a name="create-an-analysis-report"></a>创建分析报告

在 DEA 中，选择菜单图标。 在展开的菜单中，选择 "清单" 图标旁边的 "**分析报表**"。

![分析菜单](./media/database-experimentation-assistant-create-report/dea-create-reports-menu.png)

在 "**分析报表**" 下，选择 "**新建分析报表**"。

![新建分析报表菜单](./media/database-experimentation-assistant-create-report/dea-create-reports-new-report.png)

输入或选择以下信息：

- **报表名称**：输入报表的名称。 报表名称用于 A 和 B 数据库。 示例： *A （或 B）* + *报表名称* + *唯一标识符*。
- **服务器名称**：输入要包含在、B 和分析数据库中的服务器计算机的名称。
- **SQL Server 实例名称**：输入要用于报表的 SQL Server 实例的名称。
- **源服务器跟踪**：输入 SQL Server （2008 R2）第一个 trace （. trace.dat.trc）文件。
- **目标服务器的跟踪**：在 trace.dat.trc 文件中输入目标 SQL Server （2014）。

![新建分析报表页](./media/database-experimentation-assistant-create-report/dea-create-reports-inputs.png)

## <a name="generate-a-report"></a>生成报告

在 "**新建分析报表**" 页上输入或选择所需信息后，请选择 "**开始**" 以开始创建报表。 如果输入的信息有效，则会创建分析报告。 否则，包含无效信息的文本框将突出显示为红色。 请确保输入正确的值，然后选择 "**启动**"。

将生成新的分析报告。 分析数据库遵循命名方案分析和*用户指定的报表名称* + *唯一标识符*。

## <a name="frequently-asked-questions-about-analysis-reports"></a>有关分析报表的常见问题

**问：我的分析报告会告诉我什么内容？**

DEA 使用统计测试来分析工作负荷，并确定每个查询从目标1到目标2的运行情况。 它提供每个查询的性能详细信息。 在[入门](database-experimentation-assistant-get-started.md)中了解有关 DEA 的详细信息。

**问：是否可以在生成另一个报表时创建新的分析报表？**

不能。  目前，一次只能生成一个报表以防止冲突。 但是，可以同时运行多个捕获和重播。

**问：我将 DEA 升级到了2.0 版。是否仍然可以查看和使用旧报表？**

是的。 若要查看以前生成的报表，您必须更新报表的架构。 有关详细信息，请参阅[DEA 2.0：在 DEA 中更新用于分析的数据库架构报表](https://blogs.msdn.microsoft.com/datamigration/2017/03/24/dea-2-0-updating-db-schema-for-analysis-report-in-the-database-experimentation-assistant/)。

**问：我是否可以使用命令提示符生成分析报告？**

是的。 您可以在命令提示符下生成分析报告。 然后，可以在 UI 中查看报表。 有关详细信息，请参阅[在命令提示符下运行](database-experimentation-assistant-run-command-prompt.md)。

## <a name="troubleshoot-analysis-reports"></a>分析报告疑难解答

**问：我需要哪些安全权限才能在服务器上生成和查看分析报告？**

登录到 DEA 的用户必须具有对分析服务器的 sysadmin 权限。 如果用户是组的一部分，请确保该组具有 sysadmin 权限。

|可能的错误|解决方案|  
|---|---|  
|无法连接到数据库。 请确保您具有用于分析和查看报表的 sysadmin 权限。|您可能对服务器或数据库没有访问权限或 sysadmin 权限。 请确认登录权限，然后重试。|  
|无法在服务器**服务器名称**上生成**报表名称**。 有关详细信息，请检查**报表名称**报表。|您可能没有生成新报表所需的 sysadmin 权限。 若要查看详细的错误，请选择 "误码" 报告并查看% temp%\\DEA 中的日志。|  
|当前用户没有运行该操作所需的权限。 请确保您具有执行跟踪和分析报表的 sysadmin 权限。|你没有生成新报表所需的 sysadmin 权限。|  

**问：无法连接到运行 SQL Server 的计算机**

- 确认运行 SQL Server 的计算机的名称有效。 若要确认，请尝试使用 SQL Server Management Studio （SSMS）连接到服务器。
- 确认防火墙配置不会阻止与运行 SQL Server 的计算机的连接。
- 确认用户具有所需的用户权限。

可在% temp%\\DEA 中的日志中查看更多详细信息。 如果问题仍然存在，请与产品团队联系。

**问：我在生成分析报告时看到了一个错误**

安装 DEA 后首次生成分析报告时，需要访问 Internet。 需要 Internet 访问权限才能下载统计分析所需的包。

如果在创建报表时出现错误，"进度" 页将显示分析生成失败的特定步骤。 可在% temp%\\DEA 中的日志中查看更多详细信息。 请验证是否具有所需用户权限的到服务器的有效连接，然后重试。 如果问题仍然存在，请与产品团队联系。

|可能的错误|解决方案|  
|---|---|  
|RInterop 在启动时遇到错误。 请检查 RInterop 日志，然后重试。|DEA 需要 internet 访问权限才能下载相关的 R 包。 请检查% temp%\\\\DEA 中的 RInterop 日志和% temp% RInterop 中的 DEA 日志。 如果 RInterop 初始化不正确，或者未在没有正确 R 包的情况下初始化，则可能会在 DEA 日志中的 InitializeRInterop 步骤后看到 "生成新分析报表失败" 异常。<br><br>RInterop 日志还可能会显示类似于 "没有可用的 jsonlite 包" 的错误消息。 如果计算机无法访问 internet，则可以手动下载所需的 jsonlite R 包：<br><br><li>请在计算机的文件系统\\上，中转到% userprofile% DEARPackages 文件夹。 此文件夹由 R 用于 DEA 的包组成。</li><br><li>如果已安装的包列表中缺少 jsonlite 文件夹，则需要一台具有 internet 访问权限的计算机，以从\_ [https://cran.r-project.org/web/packages/jsonlite/index.html](https://cran.r-project.org/web/packages/jsonlite/index.html)下载 jsonlite 1.4。</li><br><li>将 .zip 文件复制到运行 DEA 的计算机。  提取 jsonlite 文件夹，并将其复制到% userprofile\\% DEARPackages。 此步骤会在 R 中自动安装 jsonlite 包。应将该文件夹命名为**jsonlite** ，并且内容应直接位于该文件夹内，而不是以下级别。</li><br><li>关闭 DEA，重新打开，然后再次尝试分析。</li><br>还可以使用 RGUI.EXE。 **从 zip**中转到**包** > 安装。 请先前往先前下载的包，然后再安装。<br><br>如果 RInterop 已初始化并正确设置，你应在 RInterop 日志中看到 "正在安装从属 R 包 jsonlite"。|  
|无法连接到 SQL Server 实例，请确保服务器名称正确，并检查登录用户所需的访问权限。|您可能没有对服务器的访问权限或用户权限，或者服务器名称可能不正确。|
|RInterop 进程超时。请检查 DEA 和 RInterop 日志，停止任务管理器中的 RInterop 进程，然后重试。<br><br>或<br><br>RInterop 处于出错状态。 请在任务管理器中停止 RInterop 进程，然后重试。|请检查% temp%\\RInterop 中的日志以确认错误。 请从任务管理器中删除 RInterop 进程，然后重试。 如果问题仍然存在，请与产品团队联系。|

**问：生成了报告，但数据似乎丢失**

检查运行 SQL Server 的分析计算机上的数据库，确认数据是否存在。 检查分析数据库是否存在并检查其表。 例如，检查以下表： TblBatchesA、TblBatchesB 和 TblSummaryStats。

如果数据不存在，则可能是数据没有正确复制，或者数据库可能已损坏。 如果仅缺少某些数据，则在捕获或重播中创建的跟踪文件可能未准确捕获工作负荷。 如果数据存在，请检查% temp%\\DEA 中的日志文件以查看是否记录了任何错误。 然后，再次尝试生成分析报告。

更多问题或反馈？ 选择左下角的笑脸图标，通过 DEA 工具提交反馈。 

## <a name="see-also"></a>另请参阅

- 若要了解如何查看分析报表，请参阅[查看报表](database-experimentation-assistant-view-report.md)。
