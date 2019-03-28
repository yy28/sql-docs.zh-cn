---
title: sp_changesubscription (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- changesubscription
- sp_changesubscription
- changesubscription_TSQL
- sp_changesubscription_TSQL
helpviewer_keywords:
- sp_changesubscription
ms.assetid: f9d91fe3-47cf-4915-b6bf-14c9c3d8a029
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c81843220b9613bfc59f03d197f369e77a850f84
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58534039"
---
# <a name="spchangesubscription-transact-sql"></a>sp_changesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  对于排队更新事务复制所涉及的快照或者事务推送订阅，或所涉及的请求订阅，更改其属性。 若要更改的所有其他类型的请求订阅属性，请使用[sp_change_subscription_properties &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)。 **sp_changesubscription**在发布服务器上对发布数据库执行。  
  
> [!IMPORTANT]  
>  使用远程分发服务器配置发布服务器时，为所有参数提供的值（包括 *job_login* 和 *job_password*）都会以纯文本方式发送到该分发服务器。 在执行此存储过程之前，应该对发布服务器及其远程分发服务器之间的连接进行加密。 有关详细信息，请参阅[启用数据库引擎的加密连接（SQL Server 配置管理器）](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_changesubscription [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
        , [ @subscriber = ] 'subscriber'  
        , [ @destination_db = ] 'destination_db'  
        , [ @property = ] 'property'  
        , [ @value = ] 'value'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @publication = ] 'publication'` 是要更改的名称。 *发布*是**sysname**，无默认值  
  
`[ @article = ] 'article'` 是要更改的名称。 *文章*是**sysname**，无默认值。  
  
`[ @subscriber = ] 'subscriber'` 是订阅服务器的名称。 *订阅服务器上*是**sysname**，无默认值。  
  
`[ @destination_db = ] 'destination_db'` 是订阅数据库的名称。 *destination_db*是**sysname**，无默认值。  
  
`[ @property = ] 'property'` 是要更改给定订阅的属性。 *属性*是**nvarchar(30)**，可以是表中的值之一。  
  
`[ @value = ] 'value'` 为指定的新值*属性*。 *值*是**nvarchar(4000)**，可以是表中的值之一。  
  
|属性|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**distrib_job_login**||用来运行代理的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帐户的登录名。|  
|**distrib_job_password**||用来运行代理的 Windows 帐户的密码。|  
|**subscriber_catalog**||在与 OLE DB 访问接口建立连接时要使用的目录。 此属性才是有效的非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]订阅服务器。|  
|**subscriber_datasource**||OLE DB 访问接口识别的数据源的名称。 *此属性才是有效的非*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *订阅服务器。*|  
|**subscriber_location**||OLE DB 访问接口识别的数据库的位置。 *此属性才是有效的非*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *订阅服务器。*|  
|**subscriber_login**||在订阅服务器上的登录名。|  
|**subscriber_password**||提供的登录名的强密码。|  
|**subscriber_security_mode**|**1**|连接订阅服务器时，使用 Windows 身份验证。|  
||**0**|连接订阅服务器时，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证。|  
|**subscriber_provider**||唯一编程标识符 (PROGID)，用于注册非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据源的 OLE DB 访问接口。 *此属性才是有效的非*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *订阅服务器。*|  
|**subscriber_providerstring**||OLE DB 访问接口特定的连接字符串，用于标识数据源。 *此属性才是有效的非*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *订阅服务器。*|  
|**subscriptionstreams**||每个分发代理所允许的向订阅服务器并行应用批量更改的连接数。 值范围**1**到**64**支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 此属性必须是**0**为非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]订阅服务器，Oracle 发布服务器或对等订阅。|  
|**subscriber_type**|**1**|ODBC 数据源服务器|  
||**3**|OLE DB 访问接口|  
|**memory_optimized**|**bit**|指示订阅支持内存优化表。 *memory_optimized*是**位**，1 为 true （订阅支持内存优化表）。|  
  
`[ @publisher = ] 'publisher'` 指定一个非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 *发布服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  *发布服务器*不能为指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_changesubscription**快照和事务复制中使用。  
  
 **sp_changesubscription**可仅用于修改推送订阅的属性或请求订阅参与排队更新事务复制。 若要更改的所有其他类型的请求订阅属性，请使用[sp_change_subscription_properties &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)。  
  
 更改代理登录名或密码之后，必须先停止并重新启动代理，然后更改才能生效。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_changesubscription**。  
  
## <a name="see-also"></a>请参阅  
 [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)  
  
  
