---
title: "“通知操作员”任务（维护计划）| Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: maintenance-plans
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.maint.notifyoperator.f1
helpviewer_keywords:
- Notify Operator Task dialog box
ms.assetid: 39c0797c-ad2b-4591-85c9-a23a7f902895
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b272b5d52fc3bcfadfee095f03b061c436f4508d
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="notify-operator-task-maintenance-plan"></a>“通知操作员”任务（维护计划）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]使用“通知操作员任务”对话框可以向此维护计划中添加自动通知。 若要使用此任务，必须启用数据库邮件并将 MSDB 正确配置为邮件主机数据库，而且还要具有一个带有有效电子邮件地址的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理操作员。  
  
 此任务使用 sp_notify_operator 存储过程。  
  
## <a name="options"></a>“常规”  
 **“连接”**  
 选择执行此任务时使用的服务器连接。  
  
 **新建**  
 创建一个新的服务器连接，在执行此任务时使用。 下面对 **“新建连接”** 对话框进行了介绍。  
  
 **要通知的操作员**  
 指定电子邮件的收件人。  
  
 **通知消息主题**  
 指定要在通知消息主题行中包括的文本。  
  
 **通知消息正文**  
 指定要在通知消息正文中包括的文本。  
  
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
 [数据库邮件](../../relational-databases/database-mail/database-mail.md)   
 [sp_notify_operator (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-notify-operator-transact-sql.md)  
  
  
