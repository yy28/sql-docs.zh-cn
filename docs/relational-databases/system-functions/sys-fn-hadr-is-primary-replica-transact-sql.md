---
title: sys. fn_hadr_is_primary_replica （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_hadr_is_primary_replica
- fn_hadr_is_primary_replica_TSQL
- fn_hadr_is_primary_replica
- sys.fn_hadr_is_primary_replica_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_hadr_is_primary_replica
- sys.fn_hadr_is_primary_replica
ms.assetid: c9b1969f-be1d-4dfb-a33d-551f380b9e27
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: befd4ba78a3d147acd8dd2adbd8fcb81500ec4b8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "68811415"
---
# <a name="sysfn_hadr_is_primary_replica-transact-sql"></a>sys.fn_hadr_is_primary_replica (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  用于确定当前副本是否为主副本。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.fn_hadr_is_primary_replica ( 'dbname' )  
```  
  
## <a name="arguments"></a>参数  
 "*dbname*"  
 数据库的名称。 *dbname*的类型为 sysname。  
  
## <a name="returns"></a>返回  
 如果当前实例上的数据库是主副本，则返回 1。 否则，返回 0。  
  
## <a name="remarks"></a>备注  
 使用此函数可以方便地确定本地实例承载是否承载指定可用性数据库的主副本。 示例代码可与以下代码相似。  
  
```  
If sys.fn_hadr_is_primary_replica ( @dbname ) <> 1   
BEGIN  
-- If this is not the primary replica, exit (probably without error).  
END  
-- If this is the primary replica, continue to do the backup.  
  
```  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-sysfn_hadr_is_primary_replica"></a>A. 使用 sys.fn_hadr_is_primary_replica  
 如果本地实例上的指定数据库是主副本，则以下示例返回 1。  
  
```  
SELECT sys.fn_hadr_is_primary_replica ('TestDB');  
GO  
```    
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组函数 &#40;Transact-sql&#41;](../../relational-databases/system-functions/always-on-availability-groups-functions-transact-sql.md)   
 [sys. dm_hadr_database_replica_states &#40;transact-sql&#41;](../..//relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) [AlwaysOn 可用性组 &#40;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md) SQL Server&#41;   
 [&#40;Transact-sql&#41;创建可用性组](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [更改可用性组 &#40;Transact-sql&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [AlwaysOn 可用性组目录视图 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)     
  
  
