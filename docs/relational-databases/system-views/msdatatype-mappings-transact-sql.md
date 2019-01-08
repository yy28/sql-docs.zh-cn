---
title: MSdatatype_mappings (Transact SQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 5af1233e81c996e98287a637e01ad1d249671303
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52785089"
---
# <a name="msdatatypemappings-transact-sql"></a>MSdatatype_mappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdatatype_mappings**视图将 SQL Server 数据类型映射到非 SQL Server 数据库管理系统 (DBMS) 使用的数据类型。 此表存储中**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**dbms_name**|**nvarchar(128)**|是 DBMS 的名称。 以下是可能的值及其说明。<br /><br /> **MSSQLSERVER**:目标为 SQL Server 数据库。<br />**ORACLE**:目标为 Oracle 数据库。<br />**DB2**:目标为 IBM DB2 数据库。<br />**SYBASE**:目标为 Sybase 数据库。|  
|**sql_type**|**nvarchar(128)**|是 SQL Server 数据类型。|  
|**dest_type**|**nvarchar(128)**|为非 SQL Server 数据类型的名称。|  
|**dest_prec**|**bigint**|为非 SQL Server 数据类型的精度。|  
|**dest_create_params**|**int**|仅限内部使用。|  
|**dest_nullable**|**bit**|为非 SQL Server 数据类型是否支持 NULL 值。|  
  
## <a name="see-also"></a>请参阅  
 [异类数据库复制](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [指定 Oracle 发布服务器的数据类型映射](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
