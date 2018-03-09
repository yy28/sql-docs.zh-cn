---
title: "sp_helpdistpublisher (Transact SQL) |Microsoft 文档"
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
applies_to:
- SQL Server
f1_keywords:
- sp_helpdistpublisher_TSQL
- sp_helpdistpublisher
helpviewer_keywords:
- sp_helpdistpublisher
ms.assetid: f207c22d-8fb2-4756-8a9d-6c51d6cd3470
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e01aca1558894f52f575aba642cd4079c22f21f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpdistpublisher-transact-sql"></a>sp_helpdistpublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回使用分发服务器的发布服务器的属性。 此存储过程在分发服务器上的任何数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpdistpublisher [ [ @publisher=] 'publisher']   
    [ , [ @check_user = ] check_user  
```  
  
## <a name="arguments"></a>参数  
 [  **@publisher=** ] *发布服务器*  
 为其返回属性的发布服务器的名称。 *发布服务器*是**sysname**，默认值为 **%** 。  
  
 [  **@check_user=** ] *check_user*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|发布服务器的名称。|  
|**distribution_db**|**sysname**|指定的发布服务器的分发数据库。|  
|**security_mode**|**int**|复制代理连接到发布服务器进行排队更新订阅时所用的安全模式，或者用于非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器的安全模式。<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证<br /><br /> **1** = Windows 身份验证|  
|**登录名**|**sysname**|复制代理连接到发布服务器进行排队更新订阅时的登录名，或者用于非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器的登录名。|  
|**密码**|**nvarchar(524)**|返回的密码（采用简单加密格式）。 密码的用户为 NULL 以外**sysadmin**。|  
|**活动**|**bit**|指示远程发布服务器是否将本地服务器用作分发服务器：<br /><br /> **0** = 否<br /><br /> **1** = yes|  
|**working_directory**|**nvarchar(255)**|工作目录的名称。|  
|**受信任**|**bit**|指示发布服务器连接到分发服务器时是否需要密码。 有关[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]和更高版本，这应始终会返回**0**，这意味着所需的密码。|  
|**thirdparty_flag**|**bit**|指示发布是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 启用还是由第三方应用程序启用：<br /><br /> **0** = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，oracle 或 Oracle 网关发布服务器。<br /><br /> **1** = 发布服务器已集成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用第三方应用程序。|  
|**publisher_type**|**sysname**|发布服务器的类型；可以为下列值之一：<br /><br /> **MSSQLSERVER**<br /><br /> **ORACLE**<br /><br /> **ORACLE 网关**|  
|**publisher_data_source**|**nvarchar(4000)**|发布服务器中 OLE DB 数据源的名称。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_helpdistpublisher**在所有类型的复制中使用。  
  
 **sp_helpdistpublisher**将不会显示发布服务器登录名或密码在结果集用于非**sysadmin**登录名。  
  
## <a name="permissions"></a>Permissions  
 成员**sysadmin**固定的服务器角色可能会执行**sp_helpdistpublisher**的任何发布服务器使用本地服务器作为分发服务器。 成员**db_owner**固定的数据库角色或**replmonitor**分发数据库中的角色可能会执行**sp_helpdistpublisher**的使用的任何发布服务器分发数据库。 为在指定发布中的用户发布访问列表*发布服务器*可能执行**sp_helpdistpublisher**。 如果*发布服务器*未指定，则信息返回服务器的所有发布用户具有访问权限。  
  
## <a name="see-also"></a>另请参阅  
 [查看和修改分发服务器和发布服务器属性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)  
  
  
