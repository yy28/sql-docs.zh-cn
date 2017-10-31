---
title: "GRANT 终结点权限 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/17/2017
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
- endpoints [SQL Server], permissions
- granting permissions [SQL Server], endpoints
- GRANT statement, endpoints
- permissions [SQL Server], endpoints
ms.assetid: 9eda885c-fc3a-4c9d-8de6-ce07fb35a934
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6f89febc7d63bcf36c947aacd90337e7f9478c96
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="grant-endpoint-permissions-transact-sql"></a>GRANT 端点权限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  授予对端点的权限。  

  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
GRANT permission  [ ,...n ] ON ENDPOINT :: endpoint_name  
        TO < server_principal >  [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
        SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey  
```  
  
## <a name="arguments"></a>参数  
 *权限*  
 指定可对端点授予的权限。 有关权限的列表，请参阅本主题后面的“备注”部分。  
  
 终结点上**::***endpoint_name*  
 指定要授予对其的权限的端点。 作用域限定符 (**::**) 是必需的。  
  
 到\<server_principal >  
 指定要对其授予权限的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。  
  
 *SQL_Server_login*  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录帐户的名称。  
  
 *SQL_Server_login_from_Windows_login*  
 指定通过 Windows 登录帐户创建的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录帐户的名称。  
  
 *SQL_Server_login_from_certificate*  
 指定映射到证书的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录帐户的名称。  
  
 *SQL_Server_login_from_AsymKey*  
 指定映射到非对称密钥的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录帐户的名称。  
  
 WITH GRANT OPTION  
 指示该主体还可以向其他主体授予所指定的权限。  
  
 AS *SQL_Server_login*  
 指定执行此查询的主体要从哪个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名派生其授予该权限的权限。  
  
## <a name="remarks"></a>注释  
 仅当当前数据库时，可以授予服务器范围的权限**master**。  
  
 有关终结点的信息会显示在[sys.endpoints](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)目录视图。 有关服务器权限的信息会显示在[sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)目录视图，以及有关服务器主体的信息会显示在[sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)目录视图。  
  
 端点为服务器级安全对象。 下表列出了可授予的对端点最为具体的限定权限，以及隐含这些权限的更为通用的权限。  
  
|端点权限|端点权限隐含的权限|服务器权限隐含的权限|  
|-------------------------|------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER ANY ENDPOINT|  
|CONNECT|CONTROL|CONTROL SERVER|  
|CONTROL|CONTROL|CONTROL SERVER|  
|TAKE OWNERSHIP|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 需要对端点的 CONTROL 权限或对服务器的 ALTER ANY ENDPOINT 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-granting-view-definition-permission-on-an-endpoint"></a>A. 授予对端点的 VIEW DEFINITION 权限  
 以下示例将对端点 `VIEW DEFINITION` 的 `Mirror7` 权限授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名 `ZArifin`。  
  
```  
USE master;  
GRANT VIEW DEFINITION ON ENDPOINT::Mirror7 TO ZArifin;  
GO  
```  
  
### <a name="b-granting-take-ownership-permission-with-the-grant-option"></a>B. 使用 GRANT OPTION 授予 TAKE OWNERSHIP 权限  
 以下示例使用 `TAKE OWNERSHIP`，将对端点 `Shipping83` 的 `PKomosinski` 权限授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户 `GRANT OPTION`。  
  
```  
USE master;  
GRANT TAKE OWNERSHIP ON ENDPOINT::Shipping83 TO PKomosinski   
    WITH GRANT OPTION;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [拒绝终结点权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-endpoint-permissions-transact-sql.md)   
 [REVOKE 终结点权限 &#40;Transact SQL &#41;](../../t-sql/statements/revoke-endpoint-permissions-transact-sql.md)   
 [CREATE ENDPOINT (Transact-SQL)](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [终结点目录视图 &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [sys.endpoints &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)   
 [权限（数据库引擎）](../../relational-databases/security/permissions-database-engine.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

