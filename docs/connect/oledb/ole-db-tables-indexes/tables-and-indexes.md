---
title: 表和索引 |Microsoft 文档
description: 创建、 更改和摔表和索引使用的 SQL Server OLE DB 驱动程序
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-tables-indexes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: da3a4a66f2fef351a46965cf4cca1d0335538cee
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="tables-and-indexes"></a>表和索引
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL Server 的 OLE DB 驱动程序公开**IIndexDefinition**和**ITableDefinition**接口，允许使用者能够创建、 更改和删除[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]表和索引。 表和索引定义是否有效取决于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的版本。  
  
 创建或删除表和索引的功能取决于使用者应用程序用户的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 访问权限。 删除表的功能还可以通过是否存在声明性引用完整性约束或其他因素进行进一步限制。  
  
 大多数应用程序面向[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]而不是这些 OLE DB 驱动程序使用 SQL-DMO，为 SQL Server 接口。 SQL-DMO 是支持所有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理功能的 OLE 自动化对象的集合。 面向多个 OLE DB 访问接口的应用程序使用多种 OLE DB 访问接口支持的通用 OLE DB 接口。  
  
 在特定于访问接口的 DBPROPSET_SQLSERVERCOLUMN 属性集中，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 定义了以下属性。  
  
|属性 ID|Description|  
|-----------------|-----------------|  
|SSPROP_COL_COLLATIONNAME|类型：VT_BSTR<br /><br /> R/W：写<br /><br /> 默认值：Null<br /><br /> 说明： 使用此属性仅在**ITableDefinition**。 在创建时使用此属性中指定的字符串[CREATE TABLE](../../../t-sql/statements/create-table-transact-sql.md)<br /><br /> 语句时使用。|  
  
## <a name="in-this-section"></a>本節內容  
  
-   [创建 SQL Server 表](../../oledb/ole-db-tables-indexes/creating-sql-server-tables.md)  
  
-   [向 SQL Server 表添加列](../../oledb/ole-db-tables-indexes/adding-a-column-to-a-sql-server-table.md)  
  
-   [从 SQL Server 表中删除列](../../oledb/ole-db-tables-indexes/removing-a-column-from-a-sql-server-table.md)  
  
-   [删除 SQL Server 表](../../oledb/ole-db-tables-indexes/dropping-a-sql-server-table.md)  
  
-   [创建 SQL Server 索引](../../oledb/ole-db-tables-indexes/creating-sql-server-indexes.md)  
  
-   [删除 SQL Server 索引](../../oledb/ole-db-tables-indexes/dropping-a-sql-server-index.md)  
  
## <a name="see-also"></a>另请参阅  
 [用于 SQL Server 编程的 OLE DB 驱动程序](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)   
 [DROP TABLE & #40;Transact SQL & #41;](../../../t-sql/statements/drop-table-transact-sql.md)   
 [CREATE INDEX (Transact-SQL)](../../../t-sql/statements/create-index-transact-sql.md)   
 [DROP INDEX (Transact-SQL)](../../../t-sql/statements/drop-index-transact-sql.md)  
  
  
