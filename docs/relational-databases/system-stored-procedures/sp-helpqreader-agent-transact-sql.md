---
title: sp_helpqreader_agent (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helpqreader_agent_TSQL
- sp_helpqreader_agent
helpviewer_keywords:
- sp_helpqreader_agent
ms.assetid: 8e74e1aa-e95b-4183-8017-bf123439b08d
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: e6ed297a399f8559eff4eb21b251c4d8b30590bb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpqreaderagent-transact-sql"></a>sp_helpqreader_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回队列读取器代理的属性。 此存储过程在分发服务器的分发数据库或发布服务器的任意数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpqreader_agent [ [ @frompublisher = ] frompublisher ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@frompublisher=** ] *frompublisher*  
 指定是在发布服务器还是分发服务器上调用该存储过程。 *frompublisher*位，默认值为 0。 **1**意味着从发布服务器，调用存储的过程和**0**意味着从分发服务器调用存储的过程。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|代理程序的 ID。|  
|**名称**|**nvarchar(100)**|代理的名称。|  
|**job_id**|**uniqueidentifier**|代理作业的唯一 ID。|  
|**job_login**|**nvarchar(512)**|是以格式返回的 Windows 帐户运行分发代理*域*\\*用户名*。|  
|**job_password**|**sysname**|出于安全原因，值为**\* \* \* \* \* \* \* \* \* \*** 始终返回。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_helpqreader_agent**事务复制中使用。  
  
## <a name="permissions"></a>权限  
 时的值*frompublisher*是**1**，只有的成员**sysadmin**固定的服务器角色在发布服务器或成员的**db_owner**发布数据库上的固定的数据库角色可以执行**sp_helpqreader_agent**。 否则为只有的成员**sysadmin**固定的服务器角色在分发服务器或成员的**db_owner**在分发数据库上的固定的数据库角色可以执行**sp_helpqreader_代理**。  
  
## <a name="see-also"></a>另请参阅  
 [对事务发布启用更新订阅](../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
  
