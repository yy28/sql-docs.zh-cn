---
title: "“收缩数据库”任务（维护计划）| Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- Shrink Database Task
- Shrink Database(s) Task
- sql13.swb.maint.shrink.f1
helpviewer_keywords: Shrink Database Task dialog box
ms.assetid: a9874cac-cded-4145-9c38-8aafd267dbee
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2dc6184a59756901c55bc15177914e9e08767da2
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="shrink-database-task-maintenance-plan"></a>“收缩数据库”任务（维护计划）
  使用 **“‘收缩数据库’任务”** 对话框可以创建一个任务，尝试减小所选数据库的大小。 使用下面的选项可以确定数据库收缩后在数据库中保留的未使用空间量（该百分比越大，数据库可收缩的量越小）。 该数值取决于数据库中实际数据的百分比。 例如，某个 100 MB 数据库包含 60 MB 的数据和 40 MB 的可用空间，当可用空间百分比为 50% 时，则将保留 60 MB 的数据和 30 MB 的可用空间（因为 60 MB 的 50% 是 30 MB）。 只会去除数据库中的多余空间。 有效值为 0 到 100。  
  
 收缩数据文件通过将数据页从文件末尾移动到更靠近文件开头的未占用的空间来恢复空间。 在文件末尾创建足够的可用空间后，可以取消对文件末尾的数据页的分配并将它们返回给文件系统。  
  
> [!WARNING]  
>  被移动用来收缩文件的数据可以分布到文件的任何可用位置。 这将导致索引碎片并使搜索索引范围的查询变慢。 若要消除碎片，请考虑在收缩后重新生成文件的索引。  
  
 此任务执行 DBCC SHRINKDATABASE 语句。  
  
## <a name="options"></a>选项  
 **连接**  
 选择执行此任务时使用的服务器连接。  
  
 **新建**  
 创建一个新的服务器连接，在执行此任务时使用。 下面对 **“新建连接”** 对话框进行了介绍。  
  
 **“数据库”**  
 指定受此任务影响的数据库。  
  
-   **所有数据库**  
  
     生成的维护计划将对除 tempdb 之外的所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库运行维护任务。  
  
-   **所有系统数据库**  
  
     生成的维护计划将对除 tempdb 之外的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统数据库运行维护任务。 对用户创建的数据库不运行维护任务。  
  
-   **所有用户数据库**  
  
     生成的维护计划将对用户创建的所有数据库运行维护任务。 但不会对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统数据库运行任何维护任务。  
  
-   **以下数据库**  
  
     生成的维护计划将只对所选数据库运行维护任务。 如果选择此选项，则必须至少在列表中选择一个数据库。  
  
    > [!NOTE]  
    >  只能对兼容级别被设置为 80 或更高的数据库运行维护计划。 不显示兼容级别设置为 70 或更低的数据库。  
  
 **当数据库大小超过指定值时收缩数据库**  
 指定引发此任务的数据库大小 (MB)。  
  
 **收缩后保留的可用空间**  
 当数据库文件中的可用空间达到此值时停止收缩。  
  
 **查看 T-SQL**  
 根据所选选项，查看针对此任务的服务器执行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。  
  
> [!NOTE]  
>  当受影响的对象很多时，可能需要相当长的时间才可显示。  
  
## <a name="new-connection-dialog-box"></a>“新建连接”对话框  
 **连接名称**  
 输入新连接的名称。  
  
 **选择或输入服务器名称**  
 选择执行此任务时所要连接的服务器。  
  
 **刷新**  
 刷新可用服务器的列表。  
  
 **输入登录服务器所需的信息**  
 指定如何对服务器进行身份验证。  
  
 **使用 Windows NT 集成安全性**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 的实例。  
  
 **使用特定用户名和密码**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例。 此选项不可用。  
  
 **用户名**  
 提供一个在进行身份验证时要使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 此选项不可用。  
  
 **密码**  
 提供一个在进行身份验证时要使用的密码。 此选项不可用。  
  
## <a name="see-also"></a>另请参阅  
 [DBCC SHRINKDATABASE (Transact-SQL)](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)  
  
  
