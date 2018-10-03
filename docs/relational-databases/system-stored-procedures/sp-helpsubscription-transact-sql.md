---
title: sp_helpsubscription (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_helpsubscription_TSQL
- sp_helpsubscription
helpviewer_keywords:
- sp_helpsubscription
ms.assetid: ff96bcbf-e2b9-4da8-8515-d80d4ce86c16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 41a23e9885a2d5bd49d074dc72699601eb08a6d9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47850555"
---
# <a name="sphelpsubscription-transact-sql"></a>sp_helpsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出与特定的发布、项目、订阅服务器或订阅集关联的订阅信息。 此存储过程在发布服务器上对发布数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpsubscription [ [ @publication = ] 'publication' ]   
    [ , [ @article = ] 'article' ]  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @destination_db = ] 'destination_db' ]   
    [ , [ @found=] found OUTPUT ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publication =** ] **'***publication***'**  
 关联的发布的名称。 *发布*是**sysname**，默认值为**%**，这会返回此服务器的所有订阅信息。  
  
 [  **@article=** ] **'***文章*****  
 项目的名称。 *文章*是**sysname**，默认值为**%**，表示返回所选的发布和订阅服务器的所有订阅信息。 如果**所有**，只有一个条目时返回的完整订阅发布。  
  
 [  **@subscriber=** ] **'***订阅服务器*****  
 要在其上获取订阅信息的订阅服务器的名称。 *订阅服务器上*是**sysname**，默认值为**%**，表示返回所选的发布和项目的所有订阅信息。  
  
 [  **@destination_db=** ] **'***destination_db*****  
 目标数据库的名称。 *destination_db*是**sysname**，默认值为**%**。  
  
 [  **@found=** ] **'***找到***** 输出  
 指示返回行的标志。 *找到*是**int**而且是 OUTPUT 参数，默认值为 23456。  
  
 **1**指示已找到发布。  
  
 **0**指示找不到该发布。  
  
 [ **@publisher**=] **'***发布服务器*****  
 发布服务器的名称。 *发布服务器*是**sysname**，默认值为当前服务器的名称。  
  
> [!NOTE]  
>  *发布服务器*应未指定，除非它是 Oracle 发布服务器。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**订阅服务器**|**sysname**|订阅服务器的名称。|  
|**发布**|**sysname**|发布的名称。|  
|**article**|**sysname**|项目的名称。|  
|**目标数据库**|**sysname**|用于存放复制数据的目标数据库的名称。|  
|**订阅状态**|**tinyint**|订阅状态：<br /><br /> **0** = 非活动状态<br /><br /> **1** = 订阅<br /><br /> **2** = 活动|  
|**同步类型**|**tinyint**|订阅同步类型：<br /><br /> **1** = 自动<br /><br /> **2** = 无|  
|**订阅类型**|**int**|订阅的类型：<br /><br /> **0** = 推送<br /><br /> **1** = 请求<br /><br /> **2** = 匿名|  
|**完整订阅**|**bit**|指示是否订阅发布中的所有项目：<br /><br /> 0 = 否<br /><br /> 1 = 是|  
|**订阅名称**|**nvarchar(255)**|订阅的名称。|  
|**更新模式**|**int**|**0** = 只读<br /><br /> **1** = 立即更新订阅|  
|**分发作业 id**|**binary(16)**|分发代理的作业 ID。|  
|**loopback_detection**|**bit**|环回检测将确定分发代理是否将在订阅服务器上发起的事务发送回订阅服务器：<br /><br /> **0** = 发送回。<br /><br /> **1** = 不发回。<br /><br /> 与双向事务复制一起使用。 有关详细信息，请参阅 [Bidirectional Transactional Replication](../../relational-databases/replication/transactional/bidirectional-transactional-replication.md)。|  
|**offload_enabled**|**bit**|指定复制代理的卸载执行是否已设置为在订阅服务器上运行。<br /><br /> 如果**0**，代理运行在发布服务器。<br /><br /> 如果**1**，代理在订阅服务器上运行。|  
|**offload_server**|**sysname**|启用了远程代理激活的服务器的名称。 如果为 NULL，则当前 offload_server 列入[MSdistribution_agents](../../relational-databases/system-tables/msdistribution-agents-transact-sql.md) ，可以使用表。|  
|**dts_package_name**|**sysname**|指定 Data Transformation Services (DTS) 包的名称。|  
|**dts_package_location**|**int**|为订阅分配了一个 DTS 包时，此包的位置。 如果包中，值为**0**指定的包位置**分发服务器**。 值为**1**指定**订阅服务器**。|  
|**subscriber_security_mode**|**smallint**|安全模式在订阅服务器上，其中**1**表示 Windows 身份验证，并**0**意味着[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。|  
|**subscriber_login**|**sysname**|在订阅服务器上的登录名。|  
|**subscriber_password**||永远不会返回实际的订阅服务器密码。 通过屏蔽结果"**\*\*\*\*\*\***"字符串。|  
|**job_login**|**sysname**|分发代理运行时所用的 Windows 帐户的名称。|  
|**job_password**||从不返回实际的作业密码。 通过屏蔽结果"**\*\*\*\*\*\***"字符串。|  
|**distrib_agent_name**|**nvarchar(100)**|同步订阅的代理作业的名称。|  
|**subscriber_type**|**tinyint**|订阅服务器的类型，可以是下列类型之一：<br /><br /> **0** = SQL Server 订阅服务器<br /><br /> **1** = ODBC 数据源服务器<br /><br /> **2** = Microsoft JET 数据库 （不推荐使用）<br /><br /> **3** = OLE DB 访问接口|  
|**subscriber_provider**|**sysname**|非 SQL Server 数据源的 OLE DB 访问接口用于注册的唯一编程标识符 (PROGID)。|  
|**subscriber_datasource**|**nvarchar(4000)**|OLE DB 访问接口识别的数据源的名称。|  
|**subscriber_providerstring**|**nvarchar(4000)**|OLE DB 访问接口特定的连接字符串，用于标识数据源。|  
|**subscriber_location**|**nvarchar(4000)**|OLE DB 访问接口所了解的数据库的位置|  
|**subscriber_catalog**|**sysname**|在与 OLE DB 访问接口建立连接时要使用的目录。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_helpsubscription**快照和事务复制中使用。  
  
## <a name="permissions"></a>Permissions  
 执行权限默认授予**公共**角色。 只为用户返回他们创建的订阅的信息。 有关所有订阅的信息返回到的成员**sysadmin**固定的服务器角色的发布服务器或成员**db_owner**上对发布数据库的固定的数据库角色。  
  
## <a name="see-also"></a>请参阅  
 [sp_addsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_changesubstatus &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubstatus-transact-sql.md)   
 [sp_dropsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
