---
title: "sp_MSchange_distribution_agent_properties (Transact SQL) |Microsoft 文档"
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
- sp_MSchange_distribution_agent_properties
- sp_MSchange_distribution_agent_properties_TSQL
helpviewer_keywords:
- sp_MSchange_distribution_agent_properties
ms.assetid: 7dac5e68-bf84-433a-a531-66921f35126f
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0a08ef7bb0fbbfcdfffd676c63bc2f1396fed4e5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spmschangedistributionagentproperties-transact-sql"></a>sp_MSchange_distribution_agent_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改在运行的分发代理作业的属性[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]或更高版本分发服务器。 当发布服务器在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 实例上运行时，可使用此存储过程更改属性。 此存储过程在分发服务器上对分发数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_MSchange_distribution_agent_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @subscriber = ] 'subscriber'   
        , [ @subscriber_db = ] 'subscriber_db'   
        , [ @property = ] 'property'   
        , [ @value = ] 'value' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@publisher**  =] *发布服务器*  
 发布服务器的名称。 *发布服务器*是**sysname**，无默认值。  
  
 [  **@publisher_db=** ] *publisher_db*  
 发布数据库的名称。 *publisher_db*是**sysname**，无默认值。  
  
 [  **@publication =** ] *发布*  
 发布的名称。 *发布*是**sysname**，无默认值。  
  
 [  **@subscriber=** ] *订阅服务器*  
 订阅服务器的名称。 *订阅服务器*是**sysname**，无默认值。  
  
 [  **@subscriber_db=** ] *subscriber_db*  
 是订阅数据库的名称。 *subscriber_db*是**sysname**，无默认值。  
  
 [  **@property =** ] *属性*  
 要更改的发布属性。 *属性*是**sysname**，无默认值。  
  
 [  **@value =** ] *值*  
 新属性值。 *值*是**nvarchar(524)**，默认值为 NULL。  
  
 下表说明了可以更改的分发服务器代理作业的属性，以及对这些属性值的限制。  
  
|属性|值|Description|  
|--------------|-----------|-----------------|  
|**distrib_job_login**||用来运行代理的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帐户的登录名。|  
|**distrib_job_password**||用来运行代理作业的 Windows 帐户的密码。|  
|**subscriber_catalog**||在与 OLE DB 访问接口建立连接时要使用的目录。 *此属性才是有效的非*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *订阅服务器。*|  
|**subscriber_datasource**||OLE DB 访问接口识别的数据源的名称。 *此属性才是有效的非*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *订阅服务器。*|  
|**subscriber_location**||OLE DB 访问接口识别的数据库的位置。 *此属性才是有效的非*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *订阅服务器。*|  
|**subscriber_login**||在连接到订阅服务器以同步订阅时使用的登录名。|  
|**subscriber_password**||订阅服务器密码。<br /><br /> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]|  
|**subscriber_provider**||唯一编程标识符 (PROGID)，用于注册非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据源的 OLE DB 访问接口。 *此属性才是有效的非*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *订阅服务器。*|  
|**subscriber_providerstring**||OLE DB 访问接口特定的连接字符串，用于标识数据源。 *此属性才是有效的非 SQL Server 订阅服务器。*|  
|**subscriber_security_mode**|**1**|Windows 身份验证。<br /><br /> [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]|  
||**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证。|  
|**subscriber_type**|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]订阅服务器|  
||**1**|ODBC 数据源服务器|  
||**3**|OLE DB 访问接口|  
|**订阅流**||指示每个分发代理允许的连接数，用于将更改批并行应用于订阅服务器。 *不支持非*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *订阅服务器，Oracle 发布服务器或对等订阅。*|  
  
> [!NOTE]  
>  更改代理登录名或密码之后，必须先停止并重新启动代理，然后更改才能生效。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_MSchange_distribution_agent_properties**快照复制和事务复制中使用。  
  
 发布服务器实例上的运行时[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]或更高版本，则应使用[sp_changesubscription](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md)若要更改同步运行于分发服务器的推送订阅的合并代理作业的属性。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**分发服务器上的固定的服务器角色可以执行**sp_MSchange_distribution_agent_properties**。  
  
## <a name="see-also"></a>另请参阅  
 [sp_addpushsubscription_agent &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)   
 [sp_addsubscription &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)  
  
  
