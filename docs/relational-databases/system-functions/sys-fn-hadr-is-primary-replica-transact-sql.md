---
title: sys.fn_hadr_is_primary_replica (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ebfd66acdc93f1a5148981e06f8adf1c507e1705
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33240507"
---
# <a name="sysfnhadrisprimaryreplica-transact-sql"></a>sys.fn_hadr_is_primary_replica (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  用于确定当前副本是否为主副本。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.fn_hadr_is_primary_replica ( 'dbname' )  
```  
  
## <a name="arguments"></a>参数  
 *dbname*  
 数据库的名称。 *dbname*是 sysname 类型。  
  
## <a name="returns"></a>返回  
 如果当前实例上的数据库是主副本，则返回 1。 否则，返回 0。  
  
## <a name="remarks"></a>注释  
 使用此函数可以方便地确定本地实例承载是否承载指定可用性数据库的主副本。 示例代码可与以下代码相似。  
  
```  
If sys.fn_hadr_is_primary_replica ( @dbname ) <> 1   
BEGIN  
-- If this is not the primary replica, exit (probably without error).  
END  
-- If this is the primary replica, continue to do the backup.  
  
```  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-sysfnhadrisprimaryreplica"></a>A. 使用 sys.fn_hadr_is_primary_replica  
 如果本地实例上的指定数据库是主副本，则以下示例返回 1。  
  
```  
SELECT sys.fn_hadr_is_primary_replica ('TestDB');  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组函数&#40;Transact SQL&#41;](../../relational-databases/system-functions/always-on-availability-groups-functions-transact-sql.md)   
 [AlwaysOn 可用性组 & #40;SQL server& #41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [创建可用性组 & #40;Transact SQL & #41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP (Transact-SQL)](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [AlwaysOn 可用性组目录视图&#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)  
  
  
