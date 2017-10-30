---
title: "创建远程服务绑定 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE REMOTE SERVICE BINDING
- SERVICE_BINDING_TSQL
- CREATE REMOTE SERVICE
- REMOTE_TSQL
- CREATE_REMOTE_SERVICE_BINDING_TSQL
- CREATE_REMOTE_SERVICE_TSQL
- BINDING
- SERVICE BINDING
- BINDING_TSQL
- CREATE_REMOTE_TSQL
- REMOTE_SERVICE_TSQL
- CREATE REMOTE
- REMOTE SERVICE
- REMOTE_SERVICE_BINDING_TSQL
- REMOTE
- REMOTE SERVICE BINDING
dev_langs:
- TSQL
helpviewer_keywords:
- binding remote service [Service Broker]
- dialog security [Service Broker]
- end-to-end security [Service Broker]
- security [Service Broker], remote service bindings
- CREATE REMOTE SERVICE BINDING statement
- conversation security [Service Broker]
- remote service bindings [Service Broker], creating
ms.assetid: 4165c404-4d50-4063-9a6e-6e267d309376
caps.latest.revision: 46
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a4083cb617d76084719450a6abc49fd76345cc7a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-remote-service-binding-transact-sql"></a>CREATE REMOTE SERVICE BINDING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  创建一个绑定，以用于定义在启动与远程服务的会话时要使用的安全凭据。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
CREATE REMOTE SERVICE BINDING binding_name   
   [ AUTHORIZATION owner_name ]   
   TO SERVICE 'service_name'   
   WITH  USER = user_name [ , ANONYMOUS = { ON | OFF } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 *binding_name*  
 要创建的远程服务绑定的名称。 不能指定服务器、数据库和架构名称。 *Binding_name*必须为有效**sysname**。  
  
 授权*owner_name*  
 将绑定的所有者设置为指定的数据库用户或角色。 当前用户的工作时**dbo**或**sa**， *owner_name*可以是任何有效的用户或角色的名称。 否则为*owner_name*必须是当前用户的名称、 当前用户具有 IMPERSONATE 权限的用户的名称或当前用户所属角色的名称。  
  
 到服务*service_name*  
 指定要绑定到在 WITH USER 子句中标识的用户的远程服务。  
  
 用户 = *user_name*  
 指定拥有与 TO SERVICE 子句所标识远程服务关联的证书的数据库主体。 使用该证书对与远程服务交换的消息进行加密和身份验证。  
  
 ANONYMOUS  
 指定在与远程服务进行通信时是否使用匿名身份验证。 如果匿名 = ON，则使用匿名身份验证和远程数据库中的操作将作为的成员**公共**固定的数据库角色。 如果 ANONYMOUS 为 OFF，则作为该数据库中的特定用户执行远程数据库中的操作。 如果没有指定该子句，则默认为 OFF。  
  
## <a name="remarks"></a>注释  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 使用远程服务绑定来定位要用于新会话的证书。 中与关联的证书的公钥*user_name*用于进行身份验证发送到远程服务的消息进行加密然后用于加密会话的会话密钥。 证书*user_name*必须对应于承载远程服务数据库中的用户的证书。  
  
 只有在启动与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例以外的目标服务通信的服务时，才需要远程服务绑定。 承载启动服务的数据库必须包含可用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例以外的任何目标服务的远程服务绑定。 承载目标服务的数据库不需要包含用于与目标服务通信的启动服务的远程服务绑定。 当发起方服务与目标服务位于相同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中时，无需远程服务绑定。 但是，如果远程服务绑定是，存在 where *service_name*指定到服务与本地服务的名称匹配[!INCLUDE[ssSB](../../includes/sssb-md.md)]会使用绑定。  
  
 当匿名 = ON，将连接到目标服务的启动服务的成员作为**公共**固定的数据库角色。 默认情况下，该角色的成员无权连接到数据库。 若要成功发送一条消息，目标数据库必须授予**公共**角色的数据库的连接权限和目标服务的发送权限。  
  
 如果用户拥有多个证书，则 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 将从当前有效的并标记为 AVAILABLE FOR BEGIN_DIALOG 的证书中选择过期日期最晚的证书。  
  
## <a name="permissions"></a>Permissions  
 权限用于创建远程服务绑定到名为在用户子句中，成员的用户的默认**db_owner**固定的数据库角色，成员的**db_ddladmin**固定数据库角色和成员**sysadmin**固定的服务器角色。  
  
 执行 CREATE REMOTE SERVICE BINDING 语句的用户必须对该语句中指定的主体数据库拥有模拟权限。  
  
 远程服务绑定可能不是临时对象。 远程服务绑定名称开头 **#** 可以，但是永久的对象。  
  
## <a name="examples"></a>示例  
  
### <a name="a-creating-a-remote-service-binding"></a>A. 创建远程服务绑定  
 下面的示例为服务 `//Adventure-Works.com/services/AccountsPayable` 创建了绑定。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 使用 `APUser` 数据库主体所拥有的证书向远程服务验证身份，并与远程服务交换会话加密密钥。  
  
```  
CREATE REMOTE SERVICE BINDING APBinding  
    TO SERVICE '//Adventure-Works.com/services/AccountsPayable'  
    WITH USER = APUser ;  
```  
  
### <a name="b-creating-a-remote-service-binding-using-anonymous-authentication"></a>B. 使用匿名身份验证创建远程服务绑定  
 下面的示例为服务 `//Adventure-Works.com/services/AccountsPayable` 创建了绑定。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 使用 `APUser` 数据库主体所拥有的证书与远程服务交换会话加密密钥。 Broker 不向远程服务进行身份验证。 在数据库中承载的远程服务，消息都作为提供**来宾**用户。  
  
```  
CREATE REMOTE SERVICE BINDING APBinding  
    TO SERVICE '//Adventure-Works.com/services/AccountsPayable'  
    WITH USER = APUser, ANONYMOUS=ON ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER 远程服务绑定 &#40;Transact SQL &#41;](../../t-sql/statements/alter-remote-service-binding-transact-sql.md)   
 [删除远程服务绑定 &#40;Transact SQL &#41;](../../t-sql/statements/drop-remote-service-binding-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

