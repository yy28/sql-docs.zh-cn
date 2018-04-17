---
title: dbo.server_quotas （Azure SQL 数据库） |Microsoft 文档
ms.custom: ''
ms.date: 08/02/2016
ms.prod: ''
ms.reviewer: ''
ms.suite: sql
ms.prod_service: sql-database
ms.service: sql-database
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dbo.server_quotas
- dbo.server_quotas_TSQL
- server_quotas
- server_quotas_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- server_quotas
ms.assetid: 34423903-1aaa-4a55-88a6-8228315d84e7
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 66f6e2c1cae1b8743314a8a9ff844040e1f91f35
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="dboserverquotas-azure-sql-database"></a>dbo.server_quotas (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> **重要说明!!** 这适用于 **[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11 仅 ！**  
>   
>  此功能处于预览状态。 请不要依赖于此功能的特定实现，因为此功能在将来的版本中可能更改或删除。  
  
 返回服务器上可用的数据库配额类型。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|quota_name|**nvarchar**|服务器的配额类型。 类型**Premium_database**相当于数据库与资源预留。|  
|quota_value|**int**|服务器中允许的配额类型数。|  
  
## <a name="permissions"></a>权限  
 此视图可供所有用户角色有权连接到虚拟**master**数据库。  
  
## <a name="see-also"></a>另请参阅  
 [管理高级数据库](http://go.microsoft.com/fwlink/?LinkID=311927)  
  
  
