---
title: "分布式查询支持架构行集在 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_SQLSERVERSESSION property
- schema rowsets [OLE DB]
- distributed queries [SQL Server], SQL Server Native Client OLE DB provider
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- rowsets [OLE DB], schema
ms.assetid: 11354bb6-be42-4d8d-854c-42dd3dc38656
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: da9ecaba4dd896f93d7a8e035dd51ae00c429eb8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="schema-rowsets---distributed-query-support"></a>架构行集的分布式的查询支持
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  若要支持[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]分布式查询， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序**IDBSchemaRowset**接口返回链接服务器上的元数据。  
  
 如果 DBPROPSET_SQLSERVERSESSION 属性 SSPROP_QUOTEDCATALOGNAMES 是 VARIANT_TRUE，则可以为目录名称指定带引号的标识符（例如 "my.catalog"）。 当限制架构行集输出的目录， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序可识别两部分名称包含的链接的服务器和目录名称。 下表中的架构行集，指定一个两部分目录名称作为*linked_server***。***目录*将输出限制为的适用目录中的命名的链接服务器。  
  
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
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序定义的架构行集 LINKEDSERVERS，返回已注册为链接服务器的 OLE DB 数据源的列表。  
  
## <a name="see-also"></a>另请参阅  
 [架构行集支持 &#40; OLE DB &#41;](../../../relational-databases/native-client/ole-db/schema-rowset-support-ole-db.md)   
 [LINKEDSERVERS 行集 &#40; OLE DB &#41;](../../../relational-databases/native-client/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
  
