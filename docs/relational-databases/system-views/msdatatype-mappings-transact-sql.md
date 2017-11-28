---
title: "MSdatatype_mappings (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSdatatype_mappings
- MSdatatype_mappings_TSQL
dev_langs: TSQL
helpviewer_keywords: MSdatatype_mappings view
ms.assetid: 13cdabb3-6e07-4e8d-ae80-4235022ccc7f
caps.latest.revision: "12"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7ad922397a8c2ed6e0b4faf0f92b84ee8d3408af
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="msdatatypemappings-transact-sql"></a>MSdatatype_mappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdatatype_mappings**视图将 SQL Server 数据类型映射到使用的非 SQL Server 数据库管理系统 (DBMS) 数据类型。 此表存储在**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**dbms_name**|**nvarchar （128)**|是 DBMS 的名称。 以下是可能的值以及及其说明。<br /><br /> **MSSQLSERVER**： 目标是 SQL Server 数据库。<br />**ORACLE**： 目标是 Oracle 数据库。<br />**DB2**： 目标是 IBM DB2 数据库。<br />**SYBASE**： 目标是一个 Sybase 数据库。|  
|**sql_type**|**nvarchar （128)**|为 SQL Server 数据类型。|  
|**dest_type**|**nvarchar （128)**|为非 SQL Server 数据类型的名称。|  
|**dest_prec**|**bigint**|是的非 SQL Server 数据类型的精度。|  
|**dest_create_params**|**int**|仅限内部使用。|  
|**dest_nullable**|**bit**|是如果非 SQL Server 数据类型支持 NULL 值。|  
  
## <a name="see-also"></a>另请参阅  
 [异类数据库复制](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [指定 Oracle 发布服务器的数据类型映射](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [复制表 &#40;Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
