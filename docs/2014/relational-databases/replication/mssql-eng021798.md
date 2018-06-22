---
title: MSSQL_ENG021798 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG021798 error
ms.assetid: 596f5092-75ab-4a19-8582-588687c7b089
caps.latest.revision: 15
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 7a6e96a8dfe1bca20b1be549a180def3e9286056
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014504"
---
# <a name="mssqleng021798"></a>MSSQL_ENG021798
    
## <a name="message-details"></a>消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|21798|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|在继续操作之前，必须通过 '%s' 添加 '%s' 代理作业。 请参阅 '%s' 的文档。|  
  
## <a name="explanation"></a>解释  
 要创建发布，您必须是发布服务器上的 **sysadmin** 固定服务器角色的成员或者发布数据库中的 **db_owner** 固定数据库角色的成员。 如果您是 **db_owner** 角色的成员，则发生以下情况将会引发此错误：  
  
-   从 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]运行脚本。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]中的安全模式已更改，因此必须更新这些脚本。  
  
-   存储过程 **sp_addpublication** 在执行 [sp_addlogreader_agent (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql) 之前执行。 这适用于所有的事务发布。  
  
-   存储过程 **sp_addpublication** 在执行 [sp_addqreader_agent (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql) 之前执行。 这适用于为排队更新订阅启用的事务发布（ **@allow_queued_tran** 的 **sp_addpublication**参数值为 TRUE）。  
  
 存储过程 **sp_addlogreader_agent** 和 **sp_addqreader_agent** 各创建一个代理作业并允许您指定运行代理的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帐户。 对于 **sysadmin** 角色中的用户，如果未执行 **sp_addlogreader_agent** 和 **sp_addqreader_agent** ，则将隐式创建代理作业；代理在分发服务器上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务帐户的上下文中运行。 尽管 **sp_addlogreader_agent** 和 **sp_addqreader_agent** 对于 **sysadmin** 角色中的用户不是必须的，但是为了安全起见，最好为代理指定单独的帐户。 有关详细信息，请参阅 [复制代理安全模式](security/replication-agent-security-model.md)。  
  
## <a name="user-action"></a>用户操作  
 请确保按正确的顺序执行过程。 有关详细信息，请参阅[创建发布](publish/create-a-publication.md)，更新这些脚本以包括存储的过程和所需的参数[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]及更高版本。 有关详细信息，请参阅[升级复制脚本（复制 Transact-SQL 编程）](administration/upgrade-replication-scripts-replication-transact-sql-programming.md)。  
  
## <a name="see-also"></a>请参阅  
 [错误和事件参考（复制）](errors-and-events-reference-replication.md)  
  
  
