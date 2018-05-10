---
title: MSSQL_ENG021797 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021797 error
ms.assetid: 54d83a1e-43fd-449c-a2b2-fdda2609a534
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0590d2fe828185cc0354c4b97b4c9f307f86d5de
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="mssqleng021797"></a>MSSQL_ENG021797
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|21797|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|'%s' 必须是有效的 Windows 登录名，且格式为: '计算机\登录名' 或 '域\登录名'。 请参阅 '%s' 的文档。|  
  
## <a name="explanation"></a>解释  
 如果为 **@job_login** 参数指定的值为空或无效，下列复制存储过程将引发此错误。 如果 **db_owner** 固定数据库角色的成员从早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中运行脚本时，将发生此错误。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]中的安全模式已更改，因此必须更新这些脚本。  
  
-   [sp_addlogreader_agent (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)  
  
-   [sp_addqreader_agent (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md)  
  
-   [sp_addpublication_snapshot (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)  
  
-   [sp_addpushsubscription_agent (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)  
  
-   [sp_addpullsubscription_agent (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)  
  
-   [sp_addmergepushsubscription_agent (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)  
  
-   [sp_addmergepullsubscription_agent (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)  
  
 这些存储过程可由相应服务器上 **sysadmin** 固定服务器角色的成员执行，或者相应数据库中 **db_owner** 固定数据库角色的成员执行。 每个存储过程都创建代理作业，并允许指定用于运行代理的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帐户。 对于 **sysadmin** 角色中的用户，即便未指定 Windows 帐户（如果指定帐户，则帐户必须有效），代理作业仍将隐式创建；代理运行于相应服务器的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务帐户的上下文中。 虽然帐户不是必需的，但为代理指定单独的帐户却是最佳安全方法。 有关详细信息，请参阅 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
## <a name="user-action"></a>用户操作  
 确保为每个过程的 **@job_login** 参数指定一个有效的 Windows 帐户。 如果您具有早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的复制脚本，请更新这些脚本以包括 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]所需的存储过程和参数。 有关详细信息，请参阅[升级复制脚本（复制 Transact-SQL 编程）](../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)。  
  
## <a name="see-also"></a>另请参阅  
 [错误和事件参考（复制）](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
