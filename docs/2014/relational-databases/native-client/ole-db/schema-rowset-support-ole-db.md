---
title: 架构行集支持 (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- schema rowsets [OLE DB]
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- SQL Server Native Client OLE DB provider, schema rowsets
- rowsets [OLE DB], schema
ms.assetid: a75b4b69-b095-4690-9b31-a2b32a67489e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 83b6ea8594d22527f2f9b87a77d70671c5724111
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48203457"
---
# <a name="schema-rowset-support-ole-db"></a>架构行集支持 (OLE DB)
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口还支持从链接服务器返回架构信息时处理[!INCLUDE[tsql](../../../includes/tsql-md.md)]分布式查询。  
  
> [!NOTE]  
>  尽管 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支持同义词，但 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 不返回同义词的元数据。  
  
 下面的表列表架构行集和支持的限制列[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序。  
  
|架构行集|限制列|  
|-------------------|-------------------------|  
|DBSCHEMA_CATALOGS|CATALOG_NAME|  
|DBSCHEMA_COLUMN_PRIVILEGES|支持所有限制。<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME GRANTOR GRANTEE|  
|DBSCHEMA_COLUMNS|支持所有限制。<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME<br /><br /> 以下附加列专用于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]：<br /><br /> -COLUMN_LCID，这是排序规则的区域设置 ID。 COLUMN_LCID 是与 Windows LCID 相同的值。<br />-COLUMN_COMPFLAGS 定义对于排序规则支持哪些比较。 数据格式与 DBPROB_FINDCOMPAREOPS 相同。<br />-COLUMN_SORTID，这是[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]排序的排序规则的样式。<br />-COLUMN_TDSCOLLATION，这是[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]列排序规则。<br />-IS_COMPUTED，如果列是计算的列，VARIANT_FALSE 否则为 VARIANT_TRUE。|  
|DBSCHEMA_FOREIGN_KEYS|支持所有限制。<br /><br /> PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME FK_TABLE_CATALOG FK_TABLE_SCHEMA FK_TABLE_NAME|  
|DBSCHEMA_INDEXES|支持限制 1、2、3 和 5。<br /><br /> TABLE_CATALOG TABLE_SCHEMA INDEX_NAME TABLE_NAME|  
|DBSCHEMA_PRIMARY_KEYS|支持所有限制。<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|DBSCHEMA_PROCEDURE_PARAMETERS|支持所有限制。<br /><br /> PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PARAMETER_NAME|  
|DBSCHEMA_PROCEDURES|支持限制 1、2 和 3。<br /><br /> PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME<br /><br /> DBSCHEMA_PROCEDURES 只返回可由当前用户执行的过程，或返回已向当前用户授予 VIEW DEFINITION 权限的过程。|  
|DBSCHEMA_PROVIDER_TYPES|支持所有限制。<br /><br /> DATA_TYPE BEST_MATCH|  
|DBSCHEMA_SCHEMATA|支持所有限制。<br /><br /> CATALOG_NAME SCHEMA_NAME SCHEMA_OWNER|  
|DBSCHEMA_STATISTICS|支持所有限制。<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|DBSCHEMA_TABLE_CONSTRAINTS|支持所有限制。<br /><br /> CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME CONSTRAINT_TYPE|  
|DBSCHEMA_TABLE_PRIVILEGES|支持所有限制。<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME GRANTOR GRANTEE|  
|DBSCHEMA_TABLES|支持所有限制。<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
|DBSCHEMA_TABLES_INFO|支持所有限制。<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
  
## <a name="in-this-section"></a>本节内容  
 [架构行集中的分布式查询支持](schema-rowsets-distributed-query-support.md)  
  
 [LINKEDSERVERS 行集&#40;OLE DB&#41;](schema-rowsets-linkedservers-rowset.md)  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 本机客户端&#40;OLE DB&#41;](sql-server-native-client-ole-db.md)   
 [使用用户定义类型](../features/using-user-defined-types.md)  
  
  
