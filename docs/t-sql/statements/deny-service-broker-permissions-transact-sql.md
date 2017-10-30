---
title: "拒绝 Service Broker 权限 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- denying permissions [Service Broker]
- routes [Service Broker], permissions
- Service Broker, permissions
- DENY statement, Service Broker
- remote service bindings [Service Broker], permissions
- permissions [Service Broker]
- message types [Service Broker], permissions
- denying permissions [SQL Server], Service Broker
- contracts [Service Broker], permissions
- services [Service Broker], permissions
ms.assetid: 7c6de71b-865c-41db-9413-ad9b3562e579
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ed0ab0e375ecddbf9086647adce744a8ef4cb53d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="deny-service-broker-permissions-transact-sql"></a>DENY Service Broker 权限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  拒绝授予 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 约定、消息类型、远程服务绑定、路由或服务的权限。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
DENY permission  [ ,...n ] ON  
    {    
       [ CONTRACT :: contract_name ]   
       | [ MESSAGE TYPE :: message_type_name ]    
       | [ REMOTE SERVICE BINDING :: remote_binding_name ]    
       | [ ROUTE :: route_name ]   
       | [ SERVICE :: service_name ]      
        }  
    TO database_principal [ ,...n ]   
    [ CASCADE ]  
        [ AS denying_principal ]  
```  
  
## <a name="arguments"></a>参数  
 *权限*  
 指定可拒绝授予 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 安全对象的权限。 有关权限的列表，请参阅本主题后面的“备注”部分。  
  
 协定**::***contract_name*  
 指定拒绝将其权限授权他人的约定。 作用域限定符**::**是必需的。  
  
 消息类型**::***message_type_name*  
 指定拒绝将其权限授予他人的消息类型。 作用域限定符**::**是必需的。  
  
 远程服务绑定**::***remote_binding_name*  
 指定拒绝将其权限授予他人的远程服务绑定。 作用域限定符**::**是必需的。  
  
 路由**::***route_name*  
 指定拒绝将其权限授予他人的路由。 作用域限定符**::**是必需的。  
  
 服务**::***message_type_name*  
 指定拒绝将其权限授予他人的服务。 作用域限定符**::**是必需的。  
  
 *database_principal*  
 指定要对其拒绝权限的主体。 可以是以下类型之一：  
  
-   数据库用户  
-   数据库角色  
-   应用程序角色  
-   映射到 Windows 登录名的数据库用户  
-   映射到 Windows 组的数据库用户  
-   映射到证书的数据库用户  
-   映射到非对称密钥的数据库用户  
-   未映射到服务器主体的数据库用户  
  
CASCADE  
 指示要拒绝的权限也会被对此主体授予该权限的其他主体拒绝。  
  
*denying_principal*  
 指定一个主体，执行该查询的主体从该主体获得拒绝授予该权限的权利。 可以是以下类型之一：  
  
-   数据库用户  
-   数据库角色  
-   应用程序角色  
-   映射到 Windows 登录名的数据库用户  
-   映射到 Windows 组的数据库用户  
-   映射到证书的数据库用户  
-   映射到非对称密钥的数据库用户  
-   未映射到服务器主体的数据库用户  
  
## <a name="remarks"></a>注释  
  
## <a name="service-broker-contracts"></a>Service Broker 约定  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 约定是权限层次结构中其父级数据库包含的数据库级安全对象。 最特定和受限的权限可能会遭到拒绝[!INCLUDE[ssSB](../../includes/sssb-md.md)]协定列出以下表，以及将其包含是通过默示的更多常规权限中。  
  
|Service Broker 约定权限|Service Broker 约定权限隐含的权限|数据库权限隐含的权限|  
|----------------------------------------|---------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY CONTRACT|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-message-types"></a>Service Broker 消息类型  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 消息类型是权限层次结构中其父级数据库包含的数据库级安全对象。 下表列出了可拒绝授予 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 消息类型的最特定和最受限的权限，以及隐含这些权限的更常用权限。  
  
|Service Broker 消息类型权限|Service Broker 消息类型权限隐含的权限|数据库权限隐含的权限|  
|--------------------------------------------|-------------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY MESSAGE TYPE|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-remote-service-bindings"></a>Service Broker 远程服务绑定  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 远程服务绑定是权限层次结构中其父级数据库包含的数据库级安全对象。 下表列出了可拒绝授予 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 远程服务绑定的最特定和最受限的权限，以及隐含这些权限的更常用权限。  
  
|Service Broker 远程服务绑定权限|Service Broker 远程服务绑定权限隐含的权限|数据库权限隐含的权限|  
|------------------------------------------------------|-----------------------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY REMOTE SERVICE BINDING|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-routes"></a>Service Broker 路由  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 路由是权限层次结构中其父级数据库包含的数据库级安全对象。 最特定和受限的权限可能会遭到拒绝[!INCLUDE[ssSB](../../includes/sssb-md.md)]路由列示在以下表中，以及将其包含是通过默示的更多常规权限。  
  
|Service Broker 路由权限|Service Broker 路由权限隐含的权限|数据库权限隐含的权限|  
|-------------------------------------|------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ROUTE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
### <a name="service-broker-services"></a>Service Broker 服务  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 服务是权限层次结构中其父级数据库包含的数据库级安全对象。 最特定和受限的权限可能会遭到拒绝[!INCLUDE[ssSB](../../includes/sssb-md.md)]服务将在下表中，以及将其包含是通过默示的更多常规权限中列出。  
  
|Service Broker 服务权限|Service Broker 服务权限隐含的权限|数据库权限隐含的权限|  
|---------------------------------------|--------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|SEND|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY SERVICE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 需要对 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 约定、消息类型、远程服务绑定、路由或服务具有 CONTROL 权限。 如果使用 AS 子句，那么指定主体必须拥有其权限被拒绝授予的安全对象。  
  
## <a name="see-also"></a>另请参阅  
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [REVOKE Service Broker 权限 &#40;Transact SQL &#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)   
 [DENY (Transact-SQL)](../../t-sql/statements/deny-transact-sql.md)   
 [权限 &#40; 数据库引擎 &#41;](../../relational-databases/security/permissions-database-engine.md)  
  
  

