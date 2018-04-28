---
title: 分布式查询支持架构行集在 |Microsoft 文档
description: 分布式查询中架构行集的支持
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_SQLSERVERSESSION property
- schema rowsets [OLE DB]
- distributed queries [SQL Server], OLE DB Driver for SQL Server
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- rowsets [OLE DB], schema
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aa604a66d953a4e25c3df3f20fb32218e179451b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="schema-rowsets---distributed-query-support"></a>架构行集的分布式的查询支持
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  若要支持[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]分布式查询，SQL Server 的 OLE DB 驱动程序**IDBSchemaRowset**接口返回链接服务器上的元数据。  
  
 如果 DBPROPSET_SQLSERVERSESSION 属性 SSPROP_QUOTEDCATALOGNAMES 是 VARIANT_TRUE，则可以为目录名称指定带引号的标识符（例如 "my.catalog"）。 当限制架构行集输出的目录，用于 SQL Server 的 OLE DB 驱动程序识别出两部分名称包含的链接的服务器和目录名称。 下表中的架构行集，指定一个两部分目录名称作为*linked_server***。***目录*将输出限制为的适用目录中的命名的链接服务器。  
  
|架构行集|目录限制|  
|-------------------|-------------------------|  
|DBSCHEMA_CATALOGS|CATALOG_NAME|  
|DBSCHEMA_COLUMNS|TABLE_CATALOG|  
|DBSCHEMA_PRIMARY_KEYS|TABLE_CATALOG|  
|DBSCHEMA_TABLES|TABLE_CATALOG|  
|DBSCHEMA_FOREIGN_KEYS|PK_TABLE_CATALOG FK_TABLE_CATALOG|  
|DBSCHEMA_INDEXES|TABLE_CATALOG|  
|DBSCHEMA_COLUMN_PRIVILEGES|TABLE_CATALOG|  
|DBSCHEMA_TABLE_PRIVILEGES|TABLE_CATALOG|  
  
> [!NOTE]  
>  若要限制对所有目录从链接服务器架构行集，请使用语法*linked_server* （其中的时间段分隔符是指定名称的一部分）。 该语法等同于将目录名称限制指定为 NULL，当链接服务器指示有不支持目录的数据源时也使用此语法。  
  
 SQL Server 的 OLE DB 驱动程序定义的架构行集 LINKEDSERVERS，返回已注册为链接服务器的 OLE DB 数据源的列表。  
  
## <a name="see-also"></a>另请参阅  
 [架构行集支持&#40;OLE DB&#41;](../../oledb/ole-db/schema-rowset-support-ole-db.md)   
 [LINKEDSERVERS 行集&#40;OLE DB&#41;](../../oledb/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
  
