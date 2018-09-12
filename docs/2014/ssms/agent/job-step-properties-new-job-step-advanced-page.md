---
title: 作业步骤属性： 新建作业步骤 （高级页） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.ag.job.stepadvanced.f1
ms.assetid: bdecfd4f-bcd8-4ba2-8ada-fbb636314f40
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0d34c76e71afd7a40eccfd37c6dc52131d24b409
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43811883"
---
# <a name="job-step-properties-new-job-step-advanced-page"></a>作业步骤属性：新建作业步骤（“高级”页）
  使用此页可以查看和更改 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业步骤的属性。  
  
## <a name="options"></a>选项  
 **成功时要执行的操作**  
 设置作业步骤成功时 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理应执行的操作。  
  
 **重试次数**  
 设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理对失败的作业步骤的重试次数。  
  
 **重试间隔（分钟）**  
 设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理在重试操作之间等待的时间。  
  
 **失败时要执行的操作**  
 设置作业步骤失败时 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理应执行的操作。  
  
## <a name="options-for-transact-sql-job-steps"></a>Transact-SQL 作业步骤的选项  
 **输出文件**  
 设置用于作业步骤输出的文件。 此选项仅对 **sysadmin** 固定服务器角色的成员可用。  
  
 **...**  
 浏览至用于作业步骤输出的文件。  
  
 **“视图”**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]禁止通过此按钮查看输出文件。 相反，请使用记事本查看作业步骤输出文件。  
  
 **将输出追加到现有文件**  
 将输出追加到文件的现有内容后面。 否则，每次作业步骤运行时都将覆盖以前的文件内容。  
  
 **记录到表**  
 将作业步骤的输出记录到 **msdb** 数据库的 **sysjobstepslogs** 表中。  
  
 **“视图”**  
 在作业步骤至少运行一次后，单击“查看”即可在该表中查看输出。  
  
 **将输出追加到表中的现有条目**  
 将输出追加到表的现有内容后面。 否则，每次作业步骤运行时都将覆盖以前的表内容。  
  
 **在历史记录中包含步骤输出**  
 选择此选项将在作业历史记录中包含作业步骤的输出。  
  
 **作为以下用户运行**  
 如果你是 **sysadmin** 固定服务器角色的成员，则可选择另一个 SQL 登录名运行此作业步骤。  
  
## <a name="options-for-operating-system-cmdexec-job-steps"></a>操作系统 (CmdExec) 作业步骤的选项  
 **输出文件**  
 设置用于作业步骤输出的文件。  
  
 **...**  
 浏览至用于作业步骤输出的文件。  
  
 **“视图”**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]禁止通过此按钮查看输出文件。 相反，请使用记事本查看作业步骤输出文件。  
  
 **将输出追加到现有文件**  
 每次运行时将作业步骤输出追加到之前的文件内容后面。  
  
 **记录到表**  
 将作业步骤的输出记录到 **msdb** 数据库的 **sysjobstepslogs** 表中。  
  
 **“视图”**  
 在作业步骤至少运行一次后，单击“查看”即可在该表中查看输出。  
  
 **将输出追加到表中的现有条目**  
 将输出追加到表的现有内容后面。 否则，每次作业步骤运行时都将覆盖以前的表内容。  
  
 **在历史记录中包含步骤输出**  
 选择此选项将在作业历史记录中包含作业步骤的输出。  
  
## <a name="options-for-powershell-job-steps"></a>PowerShell 作业步骤的选项  
 **输出文件**  
 设置用于作业步骤输出的文件。  
  
 **...**  
 浏览至用于作业步骤输出的文件。  
  
 **“视图”**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]禁止通过此按钮查看输出文件。 相反，请使用记事本查看作业步骤输出文件。  
  
 **将输出追加到现有文件**  
 每次运行时将作业步骤输出追加到之前的文件内容后面。  
  
 **记录到表**  
 将作业步骤的输出记录到 **msdb** 数据库的 **sysjobstepslogs** 表中。  
  
 **“视图”**  
 在作业步骤至少运行一次后，单击“查看”即可在该表中查看输出。  
  
 **将输出追加到表中的现有条目**  
 将输出追加到表的现有内容后面。 否则，每次作业步骤运行时都将覆盖以前的表内容。  
  
 **在历史记录中包含步骤输出**  
 选择此选项将在作业历史记录中包含作业步骤的输出。  
  
## <a name="options-for-replication-queue-reader-job-steps"></a>复制队列读取器作业步骤的选项  
 **Server**  
 设置服务器用于复制队列读取器作业步骤。  
  
 **“数据库”**  
 设置数据库用于复制队列读取器作业步骤。  
  
## <a name="options-for-sql-server-analysis-services-job-steps"></a>SQL Server Analysis Services 作业步骤的选项。  
 **输出文件**  
 设置用于作业步骤输出的文件。 此选项仅对 **sysadmin** 固定服务器角色的成员可用。  
  
 **...**  
 浏览至用于作业步骤输出的文件。  
  
 **视图**  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]禁止通过此按钮查看输出文件。 相反，请使用记事本查看作业步骤输出文件。  
  
 **将输出追加到现有文件**  
 将输出追加到文件的现有内容后面。 否则，每次作业步骤运行时都将覆盖以前的文件内容。  
  
 **记录到表**  
 将作业步骤的输出记录到 **msdb** 数据库的 **sysjobstepslogs** 表中。  
  
 **“视图”**  
 在作业步骤至少运行一次后，单击“查看”即可在该表中查看输出。  
  
 **将输出追加到表中的现有条目**  
 将输出追加到表的现有内容后面。 否则，每次作业步骤运行时都将覆盖以前的表内容。  
  
 **在历史记录中包含步骤输出**  
 选择此选项将在作业历史记录中包含作业步骤的输出。  
  
## <a name="see-also"></a>请参阅  
 [管理作业步骤](manage-job-steps.md)  
  
  
