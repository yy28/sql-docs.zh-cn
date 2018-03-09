---
title: "sp_helplogreader_agent (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_helplogreader_agent
- sp_helplogreader_agent_TSQL
helpviewer_keywords:
- sp_helplogreader_agent
ms.assetid: ff837209-e2b3-481a-a48f-8530bfe53d97
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ee9020dff1819069c3449bd85cbbf61d440acd91
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="sphelplogreaderagent-transact-sql"></a>sp_helplogreader_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为发布数据库返回日志读取器代理作业属性。 在发布服务器的发布数据库上执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helplogreader_agent [ [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@publisher** =] *发布服务器*  
 发布服务器的名称。 *发布服务器*是**sysname**，默认值为 NULL。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|代理程序的 ID。|  
|**名称**|**nvarchar(100)**|代理的名称。|  
|**publisher_security_mode**|**int**|代理在连接发布服务器时所使用的安全模式，可以是下列模式之一：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证<br /><br /> **1** = Windows 身份验证。|  
|**publisher_login**|**sysname**|连接到发布服务器时使用的登录名。|  
|**publisher_password**|**nvarchar(524)**|出于安全原因，值为 **\* \* \* \* \* \* \* \* \* \*** 始终返回。|  
|**job_id**|**uniqueidentifier**|代理作业的唯一 ID。|  
|**job_login**|**nvarchar(512)**|是以格式返回的 Windows 帐户运行日志读取器代理*域*\\*用户名*。|  
|**job_password**|**sysname**|出于安全原因，值为 **\* \* \* \* \* \* \* \* \* \*** 始终返回。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_helplogreader_agent**事务复制中使用。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色在发布服务器或成员的**db_owner**发布数据库上的固定的数据库角色可以执行**sp_helplogreader_agent**.  
  
## <a name="see-also"></a>另请参阅  
 [查看和修改复制安全设置](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [sp_addlogreader_agent &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)   
 [sp_changelogreader_agent &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md)  
  
  
