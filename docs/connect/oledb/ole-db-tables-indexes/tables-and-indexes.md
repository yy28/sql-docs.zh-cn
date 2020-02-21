---
title: 表和索引 | Microsoft Docs
description: 使用 OLE DB Driver for SQL Server 创建、更改和删除表和索引
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, indexes
- OLE DB, tables
- ITableDefinition interface
- tables [OLE DB]
- IIndexDefinition interface
- OLE DB Driver for SQL Server, tables
- OLE DB Driver for SQL Server, indexes
- indexes [OLE DB]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 0fc8aeed348f64c17894fa3432a7a81274ffbea4
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "68015237"
---
# <a name="tables-and-indexes"></a>表和索引
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  适用于 SQL Server 的 OLE DB 驱动程序公开 IIndexDefinition 和 ITableDefinition 接口，使使用者能够创建、更改和删除 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 表和索引   。 表和索引定义是否有效取决于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的版本。  
  
 创建或删除表和索引的功能取决于使用者应用程序用户的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 访问权限。 删除表的功能还可以通过是否存在声明性引用完整性约束或其他因素进行进一步限制。  
  
 面向 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的大多数应用程序均使用 SQL-DMO，而不是这些 OLE DB Driver for SQL Server 接口。 SQL-DMO 是支持所有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理功能的 OLE 自动化对象的集合。 面向多个 OLE DB 访问接口的应用程序使用多种 OLE DB 访问接口支持的通用 OLE DB 接口。  
  
 在特定于访问接口的 DBPROPSET_SQLSERVERCOLUMN 属性集中，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 定义了以下属性。  
  
|属性 ID|说明|  
|-----------------|-----------------|  
|SSPROP_COL_COLLATIONNAME|键入：VT_BSTR<br /><br /> R/W：写入<br /><br /> 默认值：Null<br /><br /> 说明:此属性只能在 ITableDefinition 中使用  。 该属性中指定的字符串可在创建 [CREATE TABLE](../../../t-sql/statements/create-table-transact-sql.md)<br /><br /> 语句时使用。|  
  
## <a name="in-this-section"></a>本节内容  
  
-   [创建 SQL Server 表](../../oledb/ole-db-tables-indexes/creating-sql-server-tables.md)  
  
-   [向 SQL Server 表添加列](../../oledb/ole-db-tables-indexes/adding-a-column-to-a-sql-server-table.md)  
  
-   [从 SQL Server 表中删除列](../../oledb/ole-db-tables-indexes/removing-a-column-from-a-sql-server-table.md)  
  
-   [删除 SQL Server 表](../../oledb/ole-db-tables-indexes/dropping-a-sql-server-table.md)  
  
-   [创建 SQL Server 索引](../../oledb/ole-db-tables-indexes/creating-sql-server-indexes.md)  
  
-   [删除 SQL Server 索引](../../oledb/ole-db-tables-indexes/dropping-a-sql-server-index.md)  
  
## <a name="see-also"></a>另请参阅  
 [适用于 SQL Server 的 OLE DB 驱动程序编程](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)   
 [DROP TABLE (Transact-SQL)](../../../t-sql/statements/drop-table-transact-sql.md)   
 [CREATE INDEX (Transact-SQL)](../../../t-sql/statements/create-index-transact-sql.md)   
 [DROP INDEX (Transact-SQL)](../../../t-sql/statements/drop-index-transact-sql.md)  
  
  
