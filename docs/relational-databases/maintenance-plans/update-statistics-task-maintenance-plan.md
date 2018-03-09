---
title: "“更新统计信息”任务（维护计划）| Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: maintenance-plans
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.maint.statistics.f1
helpviewer_keywords: Updates Statistics Task dialog box
ms.assetid: 22902fd0-eb39-4f18-af94-3fcb69d2a3a4
caps.latest.revision: "25"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 77bdf027ea3354d11c9877f03f20f2ebfe92afba
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="update-statistics-task-maintenance-plan"></a>“更新统计信息”任务（维护计划）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]使用“更新统计信息任务”对话框可以更新与表和索引中的数据有关的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 信息。 此任务实现对数据库中的用户表创建的每个索引的分发统计信息进行重新抽样。 分发统计信息由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用，以便在处理 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句期间优化在各表之间的导航。 为了自动生成分布统计信息， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定期从每个索引所对应的表中抽样数据。 此样本的大小取决于表中的行数和数据修改的频率。 使用此选项可以利用表中指定的数据百分比执行另一次抽样。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用此信息来创建更好的查询计划。  
  
 此任务执行 UPDATE STATISTICS 语句。  
  
## <a name="options"></a>“常规”  
 **“连接”**  
 选择执行此任务时使用的服务器连接。  
  
 **新建**  
 创建一个新的服务器连接，在执行此任务时使用。 下面对 **“新建连接”** 对话框进行了介绍。  
  
 **“数据库”**  
 指定受此任务影响的数据库。  
  
-   **“所有数据库”**  
  
     生成的维护计划将对除 tempdb 之外的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库运行维护任务。  
  
-   **所有系统数据库**  
  
     生成的维护计划将对除 tempdb 之外的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统数据库运行维护任务。 对用户创建的数据库不运行维护任务。  
  
-   **所有用户数据库**  
  
     生成的维护计划将对用户创建的所有数据库运行维护任务。 但不会对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统数据库运行任何维护任务。  
  
-   **特定数据库**  
  
     生成的维护计划将只对所选数据库运行维护任务。 如果选择此选项，则必须至少在列表中选择一个数据库。  
  
 **注意** 只能对兼容级别设置为 80 或更高的数据库运行维护计划。 不显示兼容级别设置为 70 或更低的数据库。  
  
 **对象**  
 将“选择”网格限制为显示表、显示视图或同时显示两者。  
  
 **选择**  
 指定受此任务影响的表或索引。 在“对象”框中选择 **“表和视图”** 时不可用。  
  
 **所有现有统计信息**  
 同时更新列和索引的统计信息。  
  
 **仅限列统计信息**  
 仅更新列统计信息。  
  
 **仅限索引统计信息**  
 仅更新索引统计信息。  
  
 **扫描类型**  
 用于收集已更新统计信息的扫描的类型。  
  
 **完全扫描**  
 读取表或视图中的所有行来收集统计信息。  
  
 **抽样依据**  
 指定在收集较大型的表或视图的统计信息时要抽样的表或索引视图的百分比或者行数。  
  
 **查看 T-SQL**  
 根据所选选项，查看针对此任务的服务器执行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。  
  
> [!NOTE]  
>  当受影响的对象很多时，可能需要相当长的时间才可显示。  
  
## <a name="new-connection-dialog-box"></a>“新建连接”对话框  
 **连接名称**  
 输入新连接的名称。  
  
 **选择或输入服务器名称**  
 选择执行此任务时所要连接的服务器。  
  
 **“刷新”**  
 刷新可用服务器的列表。  
  
 **输入登录服务器所需的信息**  
 指定如何对服务器进行身份验证。  
  
 **使用 Windows 集成安全性**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 的实例。  
  
 **使用特定用户名和密码**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例。 此选项不可用。  
  
 **User name**  
 提供一个在进行身份验证时要使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 此选项不可用。  
  
 **密码**  
 提供一个在进行身份验证时要使用的密码。 此选项不可用。  
  
## <a name="see-also"></a>另请参阅  
 [更新统计信息 (Transact-SQL)](../../t-sql/statements/update-statistics-transact-sql.md)  
  
  
