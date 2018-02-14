---
title: "日志文件查看器 F1 帮助 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: logs
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- sql13.swb.configurelogs.errorlog.f1
helpviewer_keywords:
- Log File Viewer
ms.assetid: 2243845c-4880-4aa0-9ee8-0a97a128996b
caps.latest.revision: 
author: BYHAM
ms.author: rickbyh
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 63be87acc6f5ef1f550f7ec9d03cad7eab93e6a6
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2018
---
# <a name="log-file-viewer-f1-help"></a>日志文件查看器 F1 帮助
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
日志文件查看器显示来自许多不同组件的日志信息。 打开日志文件查看器后，请使用 **“选择日志”** 窗格选择要显示的日志。 每个日志显示适合于该类别日志的列。  
  
 日志是否可用取决于日志文件查看器的打开方式。 有关详细信息，请参阅 [打开日志文件查看器](../../relational-databases/logs/open-log-file-viewer.md)。  
  
 可以在“工具/选项”对话框的“SQL Server 对象资源管理器/命令”页上配置为审核日志显示的行数。 有关为审核日志显示的列的说明，请参阅 [sys.fn_get_audit_file (Transact-SQL)](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)。  
  
## <a name="options"></a>“常规”  
 **加载日志**  
 打开一个对话框，您可以在其中指定要加载的日志文件。  
  
 **导出**  
 打开一个对话框，你可以使用该对话框将“日志文件摘要”  网格中显示的信息导入到文本文件中。  
  
 **“刷新”**  
 刷新选定日志的视图。 在应用任何筛选器设置时， **“刷新”** 按钮重新从目标服务器中读取选定的日志。  
  
 **筛选**  
 打开一个对话框，你可以使用该对话框指定用于筛选日志文件的设置，例如“连接” 、“日期” 或其他“常规”  筛选条件。  
  
 **搜索**  
 在日志文件中搜索特定文本。 不支持在搜索中使用通配符。  
  
 **停止**  
 停止加载日志文件条目。 例如，如果远程或脱机日志文件需要较长时间才能加载，并且您只想查看最新的条目，则可以使用此选项。  
  
 **日志文件摘要**  
 此信息窗格显示日志文件筛选摘要。 如果未对文件进行筛选，您将看到以下文本： **“未应用任何筛选器”**。 如果对日志应用了筛选器，你将看到以下文本：**“基于以下条件筛选日志条目:**  \<筛选条件>”。  
  
 **所选行详细信息**  
 选择一行可以在页面底部显示有关所选事件行的其他详细信息。 在网格中，通过将列拖动到的新位置可以重新排列各列的顺序。 通过将网格标题中的列分隔条向左或向右拖动，可以调列的大小。 双击网格标题中的列分隔条，可以按内容宽度自动调整列的大小。  
  
 **实例**  
 发生事件的实例的名称。 这显示为：计算机名称\\实例名称。  
  
## <a name="frequently-displayed-columns"></a>经常显示的列  
 **日期**  
 显示事件的日期。  
  
 **数据源**  
 显示从其创建事件的源功能，例如服务的名称（如 MSSQLSERVER）。 并非对所有日志类型都显示此项。  
  
 **消息**  
 显示与事件相关联的任何消息。  
  
 **日志类型**  
 显示事件所属的日志类型。 所有选定的日志都显示在日志文件摘要窗口中。  
  
 **日志源**  
 显示在其中捕获事件的源日志的说明。  
  
## <a name="permissions"></a>权限  
 若要访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机实例的日志文件，你需要有 securityadmin 固定服务器角色的成员身份。  
  
 若要访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 脱机实例的日志文件，不仅必须具有 **Root\Microsoft\SqlServer\ComputerManagement10** WMI 命名空间的读取权限，还必须具有存储日志文件的文件夹的读取权限。 有关详细信息，请参阅 [查看脱机日志文件](../../relational-databases/logs/view-offline-log-files.md)主题的“安全性”部分。  
  
## <a name="see-also"></a>另请参阅  
 [日志文件查看器](../../relational-databases/logs/log-file-viewer.md)   
 [打开日志文件查看器](../../relational-databases/logs/open-log-file-viewer.md)   
 [查看脱机日志文件](../../relational-databases/logs/view-offline-log-files.md)  
  
  
