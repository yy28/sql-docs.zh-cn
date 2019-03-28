---
title: sp_changereplicationserverpasswords (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changereplicationserverpasswords_TSQL
- sp_changereplicationserverpasswords
helpviewer_keywords:
- sp_changereplicationserverpasswords
ms.assetid: 9333da96-3a1c-4adb-9a74-5dac9ce596df
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 6fa6606d7daf4a1b61ff986d1d7c5675b5ae5f1f
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58531809"
---
# <a name="spchangereplicationserverpasswords-transact-sql"></a>sp_changereplicationserverpasswords (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改存储的密码[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 帐户或[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]复制代理连接到复制拓扑中的服务器时使用的登录名。 一般情况下，必须更改服务器上运行的每个单独代理的密码，即使它们使用相同的登录名或帐户时也是如此。 使用此存储过程，可以更改服务器上运行的所有复制代理所用的给定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名或 Windows 帐户的所有实例的密码。 此存储过程在复制拓扑中的任意服务器上对主数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_changereplicationserverpasswords [ @login_type = ] login_type  
        , [ @login = ] 'login'   
        , [ @password = ] 'password'  
    [ , [ @server = ] 'server' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @login_type = ] login_type` 是针对提供的凭据的身份验证类型。 *login_type*是**tinyint**，无默认值。  
  
 **1** = Windows 集成身份验证  
  
 **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证  
  
`[ @login = ] 'login'` 是 Windows 帐户的名称或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]进行更改登录名。 *登录名*是**nvarchar(257)**，无默认值  
  
`[ @password = ] 'password'` 要存储的新密码为指定*登录名*。 *密码* 是 **sysname** ，无默认值。  
  
> [!NOTE]  
>  更改复制密码后，必须停止并重新启动使用该密码的每个代理，这样代理的更改才能生效。  
  
`[ @server = ] 'server'` 是为其更改存储的密码的服务器连接。 *服务器*是**sysname**，可以是下列值之一：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**distributor**|所有指向分发服务器的代理连接。|  
|**publisher**|所有指向发布服务器的代理连接。|  
|**订阅服务器**|所有指向订阅服务器的代理连接。|  
|**%** （默认值）|指向复制拓扑中所有服务器的代理连接。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_changereplicationserverpasswords**用于所有类型的复制。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_changereplicationserverpasswords**。  
  
## <a name="see-also"></a>请参阅  
 [查看和修改复制安全设置](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
