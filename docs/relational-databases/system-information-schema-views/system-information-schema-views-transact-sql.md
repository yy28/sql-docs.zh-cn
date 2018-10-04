---
title: 系统信息架构视图 (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- information schema views
- schemas [SQL Server], information schema views
- metadata [SQL Server], views
- views [SQL Server], information schema
- system views [SQL Server], information schema
ms.assetid: 7e9f1dfe-27e9-40e7-8fc7-bfc5cae6be10
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 9e158719bde4c5259af66a2a768259ca5eb49951
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47727925"
---
# <a name="system-information-schema-views-transact-sql"></a>系统信息架构视图 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  信息架构视图是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供的几种获取元数据的方法之一。 信息架构视图提供独立于系统表的内部 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元数据视图。 尽管已经对基础系统表进行了重要的修改，信息架构视图仍然可使应用程序正常工作。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中包含的信息架构视图符合 ISO 标准中的信息架构定义。  
  
> [!IMPORTANT]  
>  已对信息架构视图进行了一些更改，这可能会中断向后兼容性。 特定视图的主题中介绍了这些更改。  
  
 在引用当前服务器时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持三部分命名约定。 ISO 标准也支持三部分命名约定。 但是，两种命名约定中使用的名称并不相同。 信息架构视图是在名为 INFORMATION_SCHEMA 的特殊架构中定义的。 此架构包含在每个数据库中。 每个信息架构视图包含特定数据库中存储的所有数据对象的元数据。 下表显示了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 名称和 SQL 标准名称之间的关系。  
  
|SQL Server 名称|对应的 SQL 标准等价名称|  
|---------------------|-----------------------------------------------|  
|“数据库”|目录|  
|架构|架构|  
|Object|Object|  
|用户定义数据类型|域|  
  
 上述名称映射约定适用于以下与 ISO 兼容的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 视图。  
  
|||  
|-|-|  
|[CHECK_CONSTRAINTS](../../relational-databases/system-information-schema-views/check-constraints-transact-sql.md)|[REFERENTIAL_CONSTRAINTS](../../relational-databases/system-information-schema-views/referential-constraints-transact-sql.md)|  
|[COLUMN_DOMAIN_USAGE](../../relational-databases/system-information-schema-views/column-domain-usage-transact-sql.md)|[ROUTINES](../../relational-databases/system-information-schema-views/routines-transact-sql.md)|  
|[COLUMN_PRIVILEGES](../../relational-databases/system-information-schema-views/column-privileges-transact-sql.md)|[ROUTINE_COLUMNS](../../relational-databases/system-information-schema-views/routine-columns-transact-sql.md)|  
|[COLUMNS](../../relational-databases/system-information-schema-views/columns-transact-sql.md)|[SCHEMATA](../../relational-databases/system-information-schema-views/schemata-transact-sql.md)|  
|[CONSTRAINT_COLUMN_USAGE](../../relational-databases/system-information-schema-views/constraint-column-usage-transact-sql.md)|[TABLE_CONSTRAINTS](../../relational-databases/system-information-schema-views/table-constraints-transact-sql.md)|  
|[CONSTRAINT_TABLE_USAGE](../../relational-databases/system-information-schema-views/constraint-table-usage-transact-sql.md)|[TABLE_PRIVILEGES](../../relational-databases/system-information-schema-views/table-privileges-transact-sql.md)|  
|[DOMAIN_CONSTRAINTS](../../relational-databases/system-information-schema-views/domain-constraints-transact-sql.md)|[TABLES](../../relational-databases/system-information-schema-views/tables-transact-sql.md)|  
|[DOMAINS](../../relational-databases/system-information-schema-views/domains-transact-sql.md)|[VIEW_COLUMN_USAGE](../../relational-databases/system-information-schema-views/view-column-usage-transact-sql.md)|  
|[KEY_COLUMN_USAGE](../../relational-databases/system-information-schema-views/key-column-usage-transact-sql.md)|[VIEW_TABLE_USAGE](../../relational-databases/system-information-schema-views/view-table-usage-transact-sql.md)|  
|[PARAMETERS](../../relational-databases/system-information-schema-views/parameters-transact-sql.md)|[VIEWS](../../relational-databases/system-information-schema-views/views-transact-sql.md)|  
  
 此外，某些视图还包含对其他类的数据（如字符数据或二进制数据）的引用。  
  
 引用信息架构视图时，必须使用包含 `INFORMATION_SCHEMA` 架构名称的限定名。 例如：  
  
```  
SELECT TABLE_CATALOG, TABLE_SCHEMA, TABLE_NAME, COLUMN_NAME, COLUMN_DEFAULT  
FROM AdventureWorks2012.INFORMATION_SCHEMA.COLUMNS  
WHERE TABLE_NAME = N'Product';  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [系统视图&#40;Transact SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
