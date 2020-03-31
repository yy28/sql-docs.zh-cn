---
title: 创建分析报告
description: 在数据库实验助手中创建分析报告
ms.date: 01/24/2020
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
ms.openlocfilehash: f82aba87632abea4ac5fbc8b54daa6dfd0eb5b4a
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79289835"
---
# <a name="create-analysis-reports-in-database-experimentation-assistant-sql-server"></a>在数据库实验助手（SQL Server） 中创建分析报告

在两个目标服务器上重播源跟踪后，可以在数据库实验助手 （DEA） 中生成分析报告。 分析报告可帮助您深入了解建议的更改对性能的影响。

## <a name="create-an-analysis-report"></a>创建分析报告

1. 在 DEA 中，选择列表图标，指定服务器名称和身份验证类型，选择或取消选择适合您的方案的**加密连接****和信任服务器证书**复选框，然后选择"**连接**"。

   ![使用跟踪文件连接到服务器](./media/database-experimentation-assistant-create-report/dea-connect-to-server-with-trace-files.png)

2. 在**分析报告**屏幕上，选择 **"新建分析报告**"。

   ![创建新的分析报告](./media/database-experimentation-assistant-create-report/dea-create-an-analysis-report.png)

3. 在 **"新建分析报告"** 屏幕上，指定报表的名称、目标 1 和目标 2 跟踪文件的存储位置和路径，然后选择"**开始**"。

   ![指定新的分析报告详细信息](./media/database-experimentation-assistant-create-report/dea-new-analysis-report-details.png)

   如果输入的信息有效，则创建分析报告。

   ![新创建的分析报告](./media/database-experimentation-assistant-create-report/dea-newly-created-analysis-report.png)

      > [!NOTE]
      > 如果输入的任何信息无效，则包含错误信息的文本框将突出显示为红色。 进行任何必要的更正，然后再次选择 **"开始**"。

## <a name="frequently-asked-questions-about-analysis-reports"></a>有关分析报告的常见问题

**问：我的分析报告告诉我什么？**

DEA 使用统计测试来分析工作负荷并确定每个查询如何从目标 1 运行到目标 2。 它为每个查询提供性能详细信息。 在 入门 中了解有关 DEA[的更多](database-experimentation-assistant-get-started.md)详细信息。

**问：在生成另一个报表时，是否可以创建新的分析报告？**

不是。  目前，一次只能生成一个报告，以防止冲突。 但是，您可以同时运行多个捕获和重播。

**问：是否可以使用命令提示生成分析报告？**

是的。 您可以在命令提示符处生成分析报告。 然后，您可以在 UI 中查看报表。 有关详细信息，请参阅[在命令提示符下运行](database-experimentation-assistant-run-command-prompt.md)。

## <a name="troubleshoot-analysis-reports"></a>故障排除分析报告

**问：在服务器上生成和查看分析报告需要哪些安全权限？**

登录到 DEA 的用户必须在分析服务器上具有系统管理员权限。 如果用户是组的一部分，请确保该组具有系统管理员权限。

|可能的错误|解决方案|  
|---|---|  
|无法连接到数据库。 请确保您具有分析和查看报表的系统管理员权限。|您可能对服务器或数据库没有访问权限或系统管理员权限。 确认您的登录权限，然后重试。|  
|无法在**服务器名称**上生成**报表名称**。 有关详细信息，请查看**报表名称**报表。|您可能没有生成新报表所需的系统管理员权限。 要查看详细错误，请选择错误报告，并检查 %temp% DEA 中的\\日志。|  
|当前用户没有运行该操作所需的权限。 请确保您具有执行跟踪和分析报表的系统管理员权限。|您没有生成新报表所需的系统管理员权限。|  

**问：无法连接到运行 SQL Server 的计算机**

- 确认运行 SQL Server 的计算机的名称是否有效。 要确认，请尝试使用 SQL 服务器管理工作室 （SSMS） 连接到服务器。
- 确认防火墙配置不会阻止与运行 SQL Server 的计算机的连接。
- 确认用户具有所需的用户权限。

您可以在日志中以 %临时%\\DEA 显示更多详细信息。 如果问题仍然存在，请与产品团队联系。

**问：生成分析报告时，我看到错误**

安装 DEA 后，首次生成分析报告时，需要进行 Internet 访问。 需要 Internet 访问才能下载统计分析所需的软件包。

如果在创建报表时发生错误，进度页将显示分析生成失败的特定步骤。 您可以在日志中以 %临时%\\DEA 显示更多详细信息。 验证您与具有所需用户权限的服务器的有效连接，然后重试。 如果问题仍然存在，请与产品团队联系。

|可能的错误|解决方案|  
|---|---|  
|RInterop 在启动时出现错误。 请检查 RInterop 日志，然后重试。|DEA 需要互联网接入才能下载相关的 R 包。 检查 RInterop 日志（以\\%temp% RInterop 和\\DEA 日志（以 %temp% DEA 表示）。 如果 RInterop 初始化不正确，或者在没有正确的 R 包的情况下初始化，您可能会在 DEA 日志中的初始化RInterop步骤之后看到异常"无法生成新的分析报告"。<br><br>RInterop 日志还可能显示类似于"没有可用的 jsonlite 包"的错误。 如果您的计算机没有 Internet 访问，您可以手动下载所需的 jonlite R 包：<br><br><li>转到计算机文件系统上的 %user\\配置文件%DEAR包文件夹。 此文件夹由 R 用于 DEA 的包组成。</li><br><li>如果已安装的软件包列表中缺少 jsonlite 文件夹，则需要一台具有 Internet 访问权限的计算机才能从\_[https://cran.r-project.org/web/packages/jsonlite/index.html](https://cran.r-project.org/web/packages/jsonlite/index.html)下载 jonlite 1.4.zip 的发布版本。</li><br><li>将 .zip 文件复制到运行 DEA 的计算机。  提取 jsonlite 文件夹并将其复制到 %userprofile%\\DEAR包。 此步骤会自动在 R 中安装 jsonlite 包。该文件夹应命名为**jsonlite，** 内容应直接位于文件夹内，而不是下面的一个级别。</li><br><li>关闭 DEA，重新打开，然后重试分析。</li><br>您还可以使用 RGUI。 转到**从 zip 安装的****软件包** > 。 转到您之前下载的包并安装。<br><br>如果 RInterop 已初始化并正确设置，则应在 RInterop 日志中看到"安装从属 R 包 jonlite"。|  
|无法连接到 SQL Server 实例，请确保服务器名称正确，并检查登录用户所需的访问权限。|您可能没有对服务器的访问权限或用户权限，或者服务器名称可能不正确。|
|RInterop 进程超时。检查 DEA 和 RInterop 日志，停止任务管理器中的 RInterop 进程，然后重试。<br><br>或<br><br>RInterop 处于故障状态。 停止任务管理器中的 RInterop 进程，然后重试。|检查 %临时%\\RInterop 中的日志以确认错误。 在重试之前，请从任务管理器中删除 RInterop 进程。 如果问题仍然存在，请与产品团队联系。|

**问：生成报告，但数据似乎丢失**

检查运行 SQL Server 的分析计算机上的数据库，以确认数据是否存在。 检查分析数据库是否存在并检查其表。 例如，检查这些表：TblBatchA、TblBatchB 和 TblSummaryStats。

如果数据不存在，则数据可能无法正确复制，或者数据库可能已损坏。 如果仅缺少某些数据，则在捕获或重播中创建的跟踪文件可能无法准确捕获您的工作负载。 如果数据存在，请检查以 %temp% DEA\\表示的日志文件，以查看是否记录了任何错误。 然后，请重试生成分析报告。

更多问题或反馈？ 通过 DEA 工具通过选择左下角的笑脸图标提交反馈。

## <a name="see-also"></a>请参阅

- 要了解如何查看分析报告，请参阅[查看报表](database-experimentation-assistant-view-report.md)。
