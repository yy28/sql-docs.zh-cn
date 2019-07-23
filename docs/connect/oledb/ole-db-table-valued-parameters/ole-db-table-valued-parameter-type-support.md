---
title: OLE DB 表值参数类型支持 | Microsoft Docs
description: OLE DB 表值参数类型支持
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (OLE DB)
author: pmasl
ms.author: pelopes
ms.openlocfilehash: abff9abb82ad0ff54d9b1126541b98babbd6bd76
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015291"
---
# <a name="ole-db-table-valued-parameter-type-support"></a>OLE DB 表值参数类型支持
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  本文介绍了 OLE DB 表值参数类型支持。  
  
## <a name="table-valued-parameter-rowset-object"></a>表值参数行集对象  
 您可以创建表值参数的专用行集对象。 使用 ITableDefinitionWithConstraints:: CreateTableWithConstraints 或 IOpenRowset:: OpenRowset 创建表值参数行集对象。 为此，请将 pTableID 参数的 eKind 成员设置为 DBKIND_GUID_NAME，并提供 CLSID_ROWSET_INMEMORY 作为 guid 成员    。 使用 IOpenRowset:: OpenRowset 时, 必须在*pTableID*的*pwszName*成员中指定表值参数的服务器类型名称。 表值参数行集对象的行为类似于 SQL Server 对象的常规 OLE DB 驱动程序。  
  
```  
const GUID CLSID_ROWSET_TVP =   
{0xc7ef28d5, 0x7bee, 0x443f, {0x86, 0xda, 0xe3, 0x98, 0x4f, 0xcd, 0x4d, 0xf9}};  
  
CoType RowsetTVP  
{  
[mandatory] interface IAccessor;  
[mandatory] interface IColumnsInfo;  
[mandatory] interface IConvertType;  
[mandatory] interface IRowset;  
[mandatory] interface IRowsetInfo;  
[optional]  interface IColumnsRowset;  
[optional]  interface IRowsetChange;  
[optional]  interface ISupportErrorInfo;  
};  
```  
  
## <a name="dbtypetable"></a>DBTYPE_TABLE  
 新类型 DBTYPE_TABLE 表示表类型。 该类型在需要 DBTYPE 的多个 OLE DB 接口中指定了表值参数。  
  
```  
#define DBTYPE_TABLE (143)  
```  
  
 DBTYPE_TABLE 具有与 DBTYPE_IUNKNOWN 相同的格式。 它是指向数据缓冲区中某个对象的指针。 为完成绑定中的规范，使用者应填充 DBOBJECT 缓冲区，并将 iid 设置为某个行集对象接口 (IID_IRowset)  。 如果绑定中未指定 DBOBJECT，则将假定为 IID_IRowset。  
  
 不支持将任何其他类型转换为 DBTYPE_TABLE，反之亦然。 针对 DBTYPE_TABLE 到 DBTYPE_TABLE 的转换以外的任何请求，IConvertType::CanConvert 将对不支持的转换返回 S_FALSE。 这将假定对 Command 对象进行 DBCONVERTFLAGS_PARAMETER 转换。  
  
## <a name="methods"></a>方法  
 有关支持表值参数的 OLE DB 方法的信息, 请参阅[OLE DB 表值参数类型支持&#40;方法&#41;](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-methods.md)。  
  
## <a name="properties"></a>属性  
 有关支持表值参数的 OLE DB 属性的信息, 请参阅[OLE DB 表值参数类型支持&#40;属性&#41;](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-properties.md)。  
  
## <a name="see-also"></a>另请参阅  
 [表值参数 (OLE DB)](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [使用表值参数 (OLE DB)](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
