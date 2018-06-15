---
title: sp_changemergesubscription (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_changemergesubscription_TSQL
- sp_changemergesubscription
helpviewer_keywords:
- sp_changemergesubscription
ms.assetid: fd820f35-c189-4e2d-884d-b60c1c469f58
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2426efe2b47c5bdd6fbf952202d70dbc4fc5e365
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32991504"
---
# <a name="spchangemergesubscription-transact-sql"></a>sp_changemergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改合并推送订阅的选定属性。 在发布服务器的发布数据库上执行此存储的过程。  
  
> [!IMPORTANT]  
>  使用远程分发服务器配置发布服务器时，为所有参数提供的值（包括 *job_login* 和 *job_password*）都会以纯文本方式发送到该分发服务器。 在执行此存储过程之前，应该对发布服务器及其远程分发服务器之间的连接进行加密。 有关详细信息，请参阅[启用数据库引擎的加密连接（SQL Server 配置管理器）](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_changemergesubscription [ [ @publication= ] 'publication' ]  
    [ , [ @subscriber= ] 'subscriber'  
    [ , [ @subscriber_db= ] 'subscriber_db' ]  
    [ , [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publication=**] **'***publication***'**  
 要更改的发布的名称。 *发布*是**sysname**，默认值为 NULL。 此发布必须已经存在且必须符合标识符规则。  
  
 [  **@subscriber=**] *****订阅服务器*****  
 订阅服务器的名称。 *订阅服务器*是**sysname**，默认值为 NULL。  
  
 [  **@subscriber_db=**] *****subscriber_db*****  
 是订阅数据库的名称。 *subscriber_db*是**sysname**，默认值为 NULL。  
  
 [  **@property=**] *****属性*****  
 是要更改给定发布的属性。 *属性*是**sysname**，并且可以为表中的值之一。  
  
 [  **@value=**] *****值*****  
 是指定的新值*属性*。 *值*是**nvarchar （255)**，并且可以为表中的值之一。  
  
|属性|“值”|Description|  
|--------------|-----------|-----------------|  
|**说明**||对该合并订阅的说明。|  
|**priority**||子订阅的优先级。 在检测到冲突时，默认冲突解决程序将使用该优先级来选取入选方。|  
|**merge_job_login**||用来运行代理的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帐户的登录名。|  
|**merge_job_password**||用来运行代理的 Windows 帐户的密码。|  
|**publisher_security_mode**|**1**|连接发布服务器时，使用 Windows 身份验证。|  
||**0**|连接发布服务器时，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证。|  
|**publisher_login**||发布服务器上的登录名。|  
|**publisher_password**||提供的发布服务器登录的强密码。|  
|**subscriber_security_mode**|**1**|连接订阅服务器时，使用 Windows 身份验证。|  
||**0**|连接订阅服务器时，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证。|  
|**subscriber_login**||在订阅服务器上的登录名。|  
|**subscriber_password**||提供的订阅服务器登录的强密码。|  
|**sync_type**|**自动**|已发布表的架构和初始数据将首先传输到订阅服务器。|  
||**无**|订阅服务器已经具有已发布表的架构和初始数据；将始终传输系统表和数据。|  
|**use_interactive_resolver**|**true**|允许交互式地解决所有允许交互式解决的项目的冲突。|  
||**false**|使用默认解决程序或自定义解决程序自动解决冲突。|  
|NULL（默认值）|NULL（默认值）||  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_changemergesubscription**合并复制中使用。  
  
 更改代理登录名或密码之后，必须先停止并重新启动代理，然后更改才能生效。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_changemergesubscription**。  
  
## <a name="see-also"></a>另请参阅  
 [sp_addmergesubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [sp_helpmergesubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
