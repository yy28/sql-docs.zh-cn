---
title: sp_helplogreader_agent (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helplogreader_agent
- sp_helplogreader_agent_TSQL
helpviewer_keywords:
- sp_helplogreader_agent
ms.assetid: ff837209-e2b3-481a-a48f-8530bfe53d97
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 811a6c78400e0030d89067d2998ed8cc0ad32be2
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52789673"
---
# <a name="sphelplogreaderagent-transact-sql"></a>sp_helplogreader_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为发布数据库返回日志读取器代理作业属性。 在发布服务器上对发布数据库执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helplogreader_agent [ [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publisher**=] **'***发布服务器***’**  
 发布服务器的名称。 *发布服务器*是**sysname**，默认值为 NULL。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|代理的 ID。|  
|**名称**|**nvarchar(100)**|代理的名称。|  
|**publisher_security_mode**|**smallint**|代理在连接发布服务器时所使用的安全模式，可以是下列模式之一：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证<br /><br /> **1** = Windows 身份验证。|  
|**publisher_login**|**sysname**|连接到发布服务器时使用的登录名。|  
|**publisher_password**|**nvarchar(524)**|出于安全原因，值为 **\*\*\*\*\*\*\*\*\*\*** 始终返回。|  
|**job_id**|**uniqueidentifier**|代理作业的唯一 ID。|  
|**job_login**|**nvarchar(512)**|是运行日志读取器代理的 Windows 帐户的格式返回*域*\\*用户名*。|  
|**job_password**|**sysname**|出于安全原因，值为 **\*\*\*\*\*\*\*\*\*\*** 始终返回。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_helplogreader_agent**事务复制中使用。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色的发布服务器或成员**db_owner**上对发布数据库的固定的数据库角色可以执行**sp_helplogreader_agent**.  
  
## <a name="see-also"></a>请参阅  
 [查看和修改复制安全设置](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [sp_addlogreader_agent &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)   
 [sp_changelogreader_agent &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md)  
  
  
