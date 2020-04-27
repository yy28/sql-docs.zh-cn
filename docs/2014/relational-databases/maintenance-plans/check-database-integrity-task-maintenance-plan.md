---
title: “检查数据库完整性”任务（维护计划）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.maintplanproperties.integrity.f1
- sql12.swb.maint.integrity.f1
helpviewer_keywords:
- Check Database Integrity Task dialog box
ms.assetid: 3534494a-5dfe-4738-b49a-e7fabd731c47
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 42fa69e6456b23f95d6a203062b580bd04f443fa
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63144672"
---
# <a name="check-database-integrity-task-maintenance-plan"></a>“检查数据库完整性”任务（维护计划）
  通过运行  语句，使用`DBCC CHECKDB`[!INCLUDE[tsql](../../includes/tsql-md.md)]“检查数据库完整性任务”对话框可以检查数据库中的用户和系统表以及索引的分配和结构完整性。 运行 `DBCC` 确保数据库中的任何完整性问题均能得到报告，以便系统管理员或数据库所有者在以后加以解决。  
  
## <a name="options"></a>选项  
 **Connection**  
 选择执行此任务时使用的服务器连接。  
  
 **新建**  
 创建一个新的服务器连接，在执行此任务时使用。 下面对 **“新建连接”** 对话框进行了介绍。  
  
 **数据库**  
 指定受此任务影响的数据库。  
  
-   **“所有数据库”**  
  
     生成的维护计划将对除 tempdb 之外的所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库运行维护任务  。  
  
-   **所有系统数据库**  
  
     生成的维护计划将对除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tempdb **之外的所有**系统数据库运行维护任务。 对用户创建的数据库不运行维护任务。  
  
-   **所有用户数据库**  
  
     生成的维护计划将对用户创建的所有数据库运行维护任务。 但不会对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统数据库运行任何维护任务。  
  
-   **特定数据库**  
  
     生成的维护计划将只对所选数据库运行维护任务。 如果选择此选项，则必须至少在列表中选择一个数据库。  
  
    > [!NOTE]  
    >  只能对兼容级别被设置为 80 或更高的数据库运行维护计划。 不显示兼容级别设置为 70 或更低的数据库。  
  
 **包括索引**  
 检查所有索引页以及表数据页的完整性。  
  
 **查看 T-SQL**  
 根据所选选项，查看针对此任务的服务器执行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。  
  
> [!NOTE]  
>  当受影响的对象很多时，可能需要相当长的时间才可显示。  
  
## <a name="new-connection-dialog-box"></a>“新建连接”对话框  
 **连接名称**  
 输入新连接的名称。  
  
 **选择或输入服务器名称**  
 选择执行此任务时所要连接的服务器。  
  
 **全部**  
 刷新可用服务器的列表。  
  
 **输入登录服务器所需的信息**  
 指定如何对服务器进行身份验证。  
  
 **使用 Windows 集成安全性**  
 使用 Windows 身份验证连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
 **使用特定用户名和密码**  
 使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证连接到的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。 此选项不可用。  
  
 **用户名**  
 提供一个在进行身份验证时要使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 此选项不可用。  
  
 **密码**  
 提供一个在进行身份验证时要使用的密码。 此选项不可用。  
  
## <a name="see-also"></a>另请参阅  
 [DBCC CHECKDB (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)  
  
  
