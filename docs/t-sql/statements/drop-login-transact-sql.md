---
title: "DROP LOGIN (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP LOGIN
- DROP_LOGIN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting login accounts
- logins [SQL Server], removing
- DROP LOGIN statement
- removing login accounts
- dropping login accounts
ms.assetid: acb5c3dc-7aa2-49f6-9330-573227ba9b1a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e43f37e0aa24cf6ab1ac7b01b378e461e5dea706
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="drop-login-transact-sql"></a>DROP LOGIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  删除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录帐户。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
DROP LOGIN login_name  
```  
  
## <a name="arguments"></a>参数  
 *login_name*  
 指定要删除的登录名。  
  
## <a name="remarks"></a>注释  
 不能删除正在登录的登录名。 也不能删除拥有任何安全对象、服务器级对象或 SQL Server 代理作业的登录名。  
  
 可以删除数据库用户映射到的登录名，但是这会创建孤立用户。 有关详细信息，请参阅 [孤立用户故障排除 (SQL Server)](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)。  
  
 在[!INCLUDE[ssSDS](../../includes/sssds-md.md)]、 登录数据需要进行身份验证连接和服务器级防火墙规则暂时缓存在每个数据库。 定期刷新此缓存。 若要强制执行身份验证缓存的刷新，并确保数据库具有登录名表的最新版本，执行[DBCC FLUSHAUTHCACHE &#40;Transact SQL &#41;](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 要求对服务器拥有 ALTER ANY LOGIN 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-dropping-a-login"></a>A. 删除登录名  
 下列示例将删除登录名 `WilliJo`。  
  
```  
DROP LOGIN WilliJo;  
GO 
```  
 
  
## <a name="see-also"></a>另请参阅  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)  

