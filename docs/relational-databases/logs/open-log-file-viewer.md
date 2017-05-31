---
title: "打开日志文件查看器 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Log File Viewer, opening
ms.assetid: a86b89cb-0432-4648-895a-05ecc5450e45
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 902e26657bb71799af5e006c9a1842edda4f783d
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="open-log-file-viewer"></a>打开日志文件查看器
  可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的日志文件查看器来访问有关在以下日志中捕获的错误和事件的信息：  
  
-   审核集合  
  
-   数据收集  
  
-   数据库邮件  
  
-   作业历史记录  
  
-   SQL Server  
  
-   SQL Server 代理  
  
-   Windows 事件（这些 Windows 事件还可以从事件查看器进行访问。）  
  
 从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]开始，您可以使用已注册的服务器从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本地或远程实例查看 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]日志文件。 通过使用已注册的服务器，无论实例处于联机还是脱机状态，您都可以查看日志文件。 有关联机访问的详细信息，请参阅本主题后面的“从已注册的服务器查看联机日志文件”过程。 有关如何访问脱机 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日志文件的详细信息，请参阅 [查看脱机日志文件](../../relational-databases/logs/view-offline-log-files.md)。  
  
 可以通过多种方法打开日志文件查看器，具体情况取决于您要查看的信息。  
  
##  <a name="BeforeYouBegin"></a> 权限  
 若要访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机实例的日志文件，你需要有 securityadmin 固定服务器角色的成员身份。  
  
 若要访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 脱机实例的日志文件，不仅必须具有 **Root\Microsoft\SqlServer\ComputerManagement10** WMI 命名空间的读取权限，还必须具有存储日志文件的文件夹的读取权限。 有关详细信息，请参阅 [查看脱机日志文件](../../relational-databases/logs/view-offline-log-files.md)主题的“安全性”部分。  
  
### <a name="security"></a>安全性  
 要求具有 securityadmin 固定服务器角色的成员身份。  
  
### <a name="view-log-files"></a>查看日志文件  
  
##### <a name="to-view-logs-that-are-related-to-general-sql-server-activity"></a>查看与常规 SQL Server 活动相关的日志  
  
1.  在对象资源管理器中，展开 **“管理”**。  
  
2.  执行下列任一操作：  
  
    -   右键单击“SQL Server 日志”，指向“查看”，然后单击“SQL Server 日志”或“SQL Server 和 Windows 日志”。  
  
    -   展开“SQL Server 日志”，右键单击任何日志文件，然后单击“查看 SQL Server 日志”。 还可以双击任何日志文件。  
  
     这些日志包括 **“数据库邮件”**、 **“SQL Server”**、 **“SQL Server 代理”**和 **“Windows NT”**。  
  
##### <a name="to-view-logs-that-are-related-to-jobs"></a>查看与作业相关的日志  
  
-   在对象资源管理器中，展开“SQL Server 代理”，右键单击“作业”，然后单击“查看历史记录”。  
  
     这些日志包括 **“数据库邮件”**、 **“作业历史记录”**和 **“SQL Server 代理”**。  
  
##### <a name="to-view-logs-that-are-related-to-maintenance-plans"></a>查看与维护计划相关的日志  
  
-   在对象资源管理器中，展开“管理”，右键单击“维护计划”，然后单击“查看历史记录”。  
  
     这些日志包括 **“数据库邮件”**、 **“作业历史记录”**、 **“维护计划”**、 **“远程维护计划”**和 **“SQL Server 代理”**。  
  
##### <a name="to-view-logs-that-are-related-to-data-collection"></a>查看与数据收集相关的日志  
  
-   在对象资源管理器中，展开“管理”，右键单击“数据收集”，然后单击“查看日志”。  
  
     这些日志包括 **“数据收集”**、 **“作业历史记录”**和 **“SQL Server 代理”**。  
  
##### <a name="to-view-logs-that-are-related-to-database-mail"></a>查看与数据库邮件相关的日志  
  
-   在对象资源管理器中，展开“管理”，右键单击“数据库邮件”，然后单击“查看数据库邮件日志”。  
  
     这些日志包括 **“数据库邮件”**、“作业历史记录”、 **“维护计划”**、 **“远程维护计划”**、 **“SQL Server”**、 **“SQL Server 代理”**和 **“Windows NT”**。  
  
##### <a name="to-view-logs-that-are-related-to-audits-collections"></a>查看与审核集合相关的日志  
  
-   在对象资源管理器中，依次展开“安全性”和“审核”，右键单击一个审核，然后单击“查看审核日志”。  
  
     这些日志包括 **“审核集合”** 和 **“Windows NT”**。  
  
##### <a name="to-view-logs-that-are-related-to-audits-collections"></a>查看与审核集合相关的日志  
  
-   在对象资源管理器中，依次展开“安全性”和“审核”，右键单击一个审核，然后单击“查看审核日志”。  
  
     这些日志包括 **“审核集合”** 和 **“Windows NT”**。  
  
## <a name="see-also"></a>另请参阅  
 [日志文件查看器](../../relational-databases/logs/log-file-viewer.md)   
 [SQL Server Audit（数据库引擎）](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)   
 [查看脱机日志文件](../../relational-databases/logs/view-offline-log-files.md)  
  
  
