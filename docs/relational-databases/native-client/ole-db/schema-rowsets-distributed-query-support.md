---
title: 架构行集中的分布式查询支持 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_SQLSERVERSESSION property
- schema rowsets [OLE DB]
- distributed queries [SQL Server], SQL Server Native Client OLE DB provider
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- rowsets [OLE DB], schema
ms.assetid: 11354bb6-be42-4d8d-854c-42dd3dc38656
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: daf4f4c0c7c6c1d53c2ab899dd150756399d53a3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296949"
---
# <a name="schema-rowsets---distributed-query-support"></a>架构行集 - 分布式查询支持
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  为了支持[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]分布式查询，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序**IDBSchemaRowset**接口返回链接服务器上的元数据。  
  
 如果 DBPROPSET_SQLSERVERSESSION 属性 SSPROP_QUOTEDCATALOGNAMES 是 VARIANT_TRUE，则可以为目录名称指定带引号的标识符（例如 "my.catalog"）。 按目录限制架构行集输出时，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序会识别包含链接服务器和目录名称的两部分名称。 对于下表中的架构行集，将两部分目录名称指定为_linked_server_**。**_目录_将输出限制为命名链接服务器的适用目录。  
  
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
>  若要将架构行集限制为来自链接服务器的所有目录，请使用语法 linked_server（其中，句点分隔符是名称规范的一部分）**。 该语法等同于将目录名称限制指定为 NULL，当链接服务器指示有不支持目录的数据源时也使用此语法。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序定义架构行集链接服务器，返回注册为链接服务器的 OLE DB 数据源的列表。  
  
## <a name="see-also"></a>另请参阅  
 [架构排集支持&#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowset-support-ole-db.md)   
 [LINKEDSERVERS 行集 &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
  
