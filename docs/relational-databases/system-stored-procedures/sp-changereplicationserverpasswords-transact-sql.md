---
title: "sp_changereplicationserverpasswords (Transact SQL) |Microsoft 文档"
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
- sp_changereplicationserverpasswords_TSQL
- sp_changereplicationserverpasswords
helpviewer_keywords:
- sp_changereplicationserverpasswords
ms.assetid: 9333da96-3a1c-4adb-9a74-5dac9ce596df
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fcd1cbfd5532703196e47d06f920ef7cfa81f019
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spchangereplicationserverpasswords-transact-sql"></a>sp_changereplicationserverpasswords (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改存储的密码[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 帐户或[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]复制代理连接到复制拓扑中的服务器时所使用的登录名。 一般情况下，必须更改服务器上运行的每个单独代理的密码，即使它们使用相同的登录名或帐户时也是如此。 使用此存储过程，可以更改服务器上运行的所有复制代理所用的给定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名或 Windows 帐户的所有实例的密码。 此存储过程在复制拓扑中的任意服务器上对主数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_changereplicationserverpasswords [ @login_type = ] login_type  
        , [ @login = ] 'login'   
        , [ @password = ] 'password'  
    [ , [ @server = ] 'server' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@login_type**  =] *login_type*  
 提供的凭据的身份验证类型。 *login_type*是**tinyint**，无默认值。  
  
 **1** = Windows 集成身份验证  
  
 **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证  
  
 [  **@login**  =] *登录*  
 要更改的 Windows 帐户或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录的名称。 *登录名*是**nvarchar(257)**，无默认值  
  
 [  **@password**  =] *密码*  
 是要存储的新密码指定*登录*。 *密码*是**sysname**，无默认值。  
  
> [!NOTE]  
>  更改复制密码后，必须停止并重新启动使用该密码的每个代理，这样代理的更改才能生效。  
  
 [  **@server**  =] *服务器*  
 要为其更改存储密码的服务器连接。 *服务器*是**sysname**，并且可以为这些值之一：  
  
|值|Description|  
|-----------|-----------------|  
|**分发服务器**|所有指向分发服务器的代理连接。|  
|**发布服务器**|所有指向发布服务器的代理连接。|  
|**订阅服务器**|所有指向订阅服务器的代理连接。|  
|**%**（默认值）|指向复制拓扑中所有服务器的代理连接。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_changereplicationserverpasswords**用于所有类型的复制。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_changereplicationserverpasswords**。  
  
## <a name="see-also"></a>另请参阅  
 [查看和修改复制安全设置](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
