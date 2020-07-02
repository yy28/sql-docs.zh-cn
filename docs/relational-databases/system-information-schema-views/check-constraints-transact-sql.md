---
title: CHECK_CONSTRAINTS （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- CHECK_CONSTRAINTS
- CHECK_CONSTRAINTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CHECK_CONSTRAINTS view
- INFORMATION_SCHEMA.CHECK_CONSTRAINTS view
ms.assetid: e9577fd2-c349-4dff-874c-9e57d2e5a3ec
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8e11221d32ff632d339330f2a97f78bc6615965f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85752836"
---
# <a name="check_constraints-transact-sql"></a>CHECK_CONSTRAINTS (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asdw-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  针对当前数据库的每个 CHECK 约束返回一行。 该信息架构视图返回当前用户对其拥有权限的对象的相关信息。  
  
 若要从这些视图中检索信息，请指定 INFORMATION_SCHEMA 的完全限定名称 **。**_view_name_。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**CONSTRAINT_CATALOG**|**nvarchar （** 128 **）**|约束限定符。|  
|**CONSTRAINT_SCHEMA**|**nvarchar （** 128 **）**|约束所属架构的名称。<br /><br /> &#42;&#42; 重要 &#42;&#42; 不要使用 INFORMATION_SCHEMA 视图来确定对象的架构。 INFORMATION_SCHEMA 视图仅表示对象的元数据的子集。 查找对象架构的唯一可靠方法是查询 sys.databases 目录视图。|  
|**CONSTRAINT_NAME**|**sysname**|约束名称。|  
|**CHECK_CLAUSE**|**nvarchar （** 4000 **）**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 定义语句的实际文本。|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;的系统视图 &#40;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [&#40;Transact-sql&#41;的信息架构视图](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys. check_constraints &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)   
 [sys.objects (Transact-SQL)](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  
