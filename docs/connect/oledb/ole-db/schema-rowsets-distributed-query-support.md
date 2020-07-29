---
title: 架构行集中的分布式查询支持 | Microsoft Docs
description: 架构行集中的分布式查询支持
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_SQLSERVERSESSION property
- schema rowsets [OLE DB]
- distributed queries [SQL Server], OLE DB Driver for SQL Server
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- rowsets [OLE DB], schema
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 9c1207278d194df83a69109b14768eb3b99a719e
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86012790"
---
# <a name="schema-rowsets---distributed-query-support"></a>架构行集 - 分布式查询支持
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  为了支持 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分布式查询，适用于 SQL Server 的 OLE DB 驱动程序 IDBSchemaRowset 接口返回链接服务器上的元数据  。  
  
 如果 DBPROPSET_SQLSERVERSESSION 属性 SSPROP_QUOTEDCATALOGNAMES 是 VARIANT_TRUE，则可以为目录名称指定带引号的标识符（例如 "my.catalog"）。 如果按目录限制架构行集输出，则适用于 SQL Server 的 OLE DB 驱动程序识别包含链接服务器和目录名称的由两个部分组成的名称。 对于下表中的架构行集，将一个由两部分组成的目录名称指定为 _linked\_server_ **.** _catalog_ 可将输出限制为命名链接服务器的适用目录。  
  
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
>  若要将架构行集限制为来自链接服务器的所有目录，请使用语法 linked_server  （其中，下划线分隔符是名称规范的一部分）。 该语法等同于将目录名称限制指定为 NULL，当链接服务器指示有不支持目录的数据源时也使用此语法。  
 
 适用于 SQL Server 的 OLE DB 驱动程序定义架构行集 LINKEDSERVERS，返回注册为链接服务器的 OLE DB 数据源列表。  
  
## <a name="see-also"></a>另请参阅  
 [架构行集支持 (OLE DB)](../../oledb/ole-db/schema-rowset-support-ole-db.md)   
 [LINKEDSERVERS 行集 &#40;OLE DB&#41;](../../oledb/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
  
