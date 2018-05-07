---
title: sysmail_start_sp (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysmail_start_sp
- sysmail_start_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_start_sp
ms.assetid: 25fd7bb6-cfdd-463f-bea8-c6fcb805d3f5
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9513e95d52aed4ee7fb525504dfb112092e1807d
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sysmailstartsp-transact-sql"></a>sysmail_start_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  通过启动外部程序使用的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 对象来启动数据库邮件。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sysmail_start_sp  
```  
  
## <a name="arguments"></a>参数  
 InclusionThresholdSetting  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>注释  
 数据库邮件未启用或在时才安装[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装。 使用数据库邮件配置向导可以启用并安装数据库邮件对象。  
  
 此存储的过程位于**msdb**数据库。 该存储过程将启动保存待发消息请求的数据库邮件队列，并对外部程序启用 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 激活。  
  
 此队列启动后，数据库邮件外部程序即可处理消息。 此过程允许你重启队列，队列都已停止使用后**sysmail_stop_sp**存储过程。  
  
> [!NOTE]  
>  此存储过程只启动数据库邮件的队列。 它不会激活数据库中的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 消息传递功能。  
  
## <a name="permissions"></a>权限  
 执行此过程默认为成员的权限**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
 下面的示例演示从数据库邮件**msdb**数据库。 该示例假设数据库邮件已启用。  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sysmail_start_sp ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据库邮件](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail XPs 服务器配置选项](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md)   
 [sysmail_stop_sp &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-stop-sp-transact-sql.md)   
 [数据库邮件存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
