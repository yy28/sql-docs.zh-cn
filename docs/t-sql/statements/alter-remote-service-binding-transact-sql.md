---
title: "ALTER 远程服务绑定 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER REMOTE SERVICE BINDING
- ALTER_REMOTE_SERVICE_BINDING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- remote service bindings [Service Broker], modifying
- ALTER REMOTE SERVICE BINDING statement
- modifying remote service bindings
ms.assetid: ee620b4a-9375-4eaa-a016-69916c9e1e68
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5352750b43775b53a508b42de17d33a792a40b1b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="alter-remote-service-binding-transact-sql"></a>ALTER REMOTE SERVICE BINDING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改与远程服务绑定相关联的用户，或更改绑定的匿名身份验证设置。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
ALTER REMOTE SERVICE BINDING binding_name   
   WITH [ USER = <user_name> ] [ , ANONYMOUS = { ON | OFF } ]   
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 *binding_name*  
 要更改的远程服务绑定的名称。 不能指定服务器、数据库和架构名称。  
  
 与用户 = \< *user_name >*  
 指定数据库用户，该用户持有与此绑定的远程服务相关联的证书。 此证书的公钥用于对与远程服务交换的消息进行加密和身份验证。  
  
 ANONYMOUS  
 指定在与远程服务进行通信时是否使用匿名身份验证。 如果 ANONYMOUS = ON，则使用匿名身份验证，且不会将本地用户的凭据传输给远程服务。 如果 ANONYMOUS = OFF，则传输用户凭据。 如果没有指定该子句，则默认为 OFF。  
  
## <a name="remarks"></a>注释  
 中与关联的证书的公钥*user_name*用于进行身份验证发送到远程服务的消息进行加密然后用于加密会话的会话密钥。 证书*user_name*必须对应于承载远程服务的数据库中具有登录名的证书。  
  
## <a name="permissions"></a>Permissions  
 更改远程服务绑定的权限默认为远程服务绑定的成员的所有者**db_owner**固定数据库角色和成员的**sysadmin**固定的服务器角色。  
  
 执行 ALTER REMOTE SERVICE BINDING 语句的用户必须具有该语句中所指定用户的模拟权限。  
  
 若要更改远程服务绑定的 AUTHORIZATION，请使用 ALTER AUTHORIZATION 语句。  
  
## <a name="examples"></a>示例  
 下面的示例使用帐户 `APBinding` 的证书将远程服务绑定 `SecurityAccount` 更改为加密消息。  
  
```  
ALTER REMOTE SERVICE BINDING APBinding  
    WITH USER = SecurityAccount ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE REMOTE SERVICE BINDING (Transact-SQL)](../../t-sql/statements/create-remote-service-binding-transact-sql.md)   
 [删除远程服务绑定 &#40;Transact SQL &#41;](../../t-sql/statements/drop-remote-service-binding-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

