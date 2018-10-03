---
title: ad hoc distributed queries 服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- OPENROWSET function, ad hoc distributed queries option
- Ad Hoc Distributed Queries option
- ad hoc distributed queries
- 7415 (Database Engine Error)
- OPENDATASOURCE function, ad hoc distributed queries option
- ad hoc access
ms.assetid: 5b982015-e196-44c3-83b8-275fb9d769b2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ddef6de92c0bb5329e84011f9996368ef6b452dc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47690137"
---
# <a name="ad-hoc-distributed-queries-server-configuration-option"></a>即席分布式查询服务器配置选项
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允许使用 OPENROWSET 和 OPENDATASOURCE 进行即席分布式查询。 此选项设置为 1 时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允许进行即席访问。 如果此选项未设置或设置为 0，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允许进行即席访问。  
  
 即席分布式查询使用 OPENROWSET 和 OPENDATASOURCE 函数连接到使用 OLE DB 的远程数据源。 OPENROWSET 和 OPENDATASOURCE 只应在引用不常访问的 OLE DB 数据源时使用。 对于将要经常访问的数据源，应定义链接服务器。  
  
> [!IMPORTANT]  
>  允许使用临时名称意味着到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的任何经过身份验证的登录名均可访问该访问接口。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理员应对任何本地登录名都能安全访问的访问接口启用此功能。  
  
## <a name="remarks"></a>Remarks  
 尝试进行即席连接但未启用“ 即席分布式查询 ”  会导致错误：消息 7415，级别 16，状态 1，行 1  
  
 已拒绝对 OLE DB 访问接口“Microsoft.ACE.OLEDB.12.0”的即席访问。 必须通过链接服务器来访问此访问接口。  
  
## <a name="examples"></a>示例  
 下面的示例启用即席分布式查询，然后使用 `Seattle1` 函数查询名为 `OPENROWSET` 的服务器。  
  
```  
sp_configure 'show advanced options', 1;  
RECONFIGURE;
GO 
sp_configure 'Ad Hoc Distributed Queries', 1;  
RECONFIGURE;  
GO  
  
SELECT a.*  
FROM OPENROWSET('SQLNCLI', 'Server=Seattle1;Trusted_Connection=yes;',  
     'SELECT GroupName, Name, DepartmentID  
      FROM AdventureWorks2012.HumanResources.Department  
      ORDER BY GroupName, Name') AS a;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [链接服务器（数据库引擎）](../../relational-databases/linked-servers/linked-servers-database-engine.md)   
 [OPENROWSET (Transact-SQL)](../../t-sql/functions/openrowset-transact-sql.md)   
 [OPENDATASOURCE (Transact-SQL)](../../t-sql/functions/opendatasource-transact-sql.md)   
 [sp_addlinkedserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)  
  
  
