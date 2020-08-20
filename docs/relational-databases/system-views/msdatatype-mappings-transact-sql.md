---
description: MSdatatype_mappings (Transact-SQL)
title: MSdatatype_mappings (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdatatype_mappings
- MSdatatype_mappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdatatype_mappings view
ms.assetid: 13cdabb3-6e07-4e8d-ae80-4235022ccc7f
author: stevestein
ms.author: sstein
ms.openlocfilehash: f67f313d177b5ef22e6cb97b9ab25d5281c860e2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463822"
---
# <a name="msdatatype_mappings-transact-sql"></a>MSdatatype_mappings (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSdatatype_mappings**视图将 SQL Server 数据类型映射到非 SQL Server 数据库管理系统 (DBMS) 使用的数据类型。 该表存储在 **msdb** 数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**dbms_name**|**nvarchar(128)**|是 DBMS 的名称。 下面是可能的值及其说明。<br /><br /> **MSSQLSERVER**：目标是 SQL Server 数据库。<br />**Oracle**：目标是 ORACLE 数据库。<br />**DB2**：目标为 IBM DB2 数据库。<br />**Sybase**：目标为 SYBASE 数据库。|  
|**sql_type**|**nvarchar(128)**|是 SQL Server 数据类型。|  
|**dest_type**|**nvarchar(128)**|非 SQL Server 数据类型的名称。|  
|**dest_prec**|**bigint**|非 SQL Server 数据类型的精度。|  
|**dest_create_params**|**int**|仅限内部使用。|  
|**dest_nullable**|**bit**|指示非 SQL Server 数据类型是否支持 NULL 值。|  
  
## <a name="see-also"></a>另请参阅  
 [异类数据库复制](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [指定 Oracle 发布服务器的数据类型映射](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [Transact-sql&#41;&#40;复制表 ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
