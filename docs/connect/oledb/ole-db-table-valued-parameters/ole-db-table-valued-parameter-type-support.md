---
title: OLE DB 表值参数类型支持 |Microsoft 文档
description: OLE DB Table-Valued 参数类型支持
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (OLE DB)
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fab229c7f3f078b980ae758371ab126782bd63fd
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2018
---
# <a name="ole-db-table-valued-parameter-type-support"></a>OLE DB 表值参数类型支持
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本指南介绍了 OLE DB 类型支持表值参数。  
  
## <a name="table-valued-parameter-rowset-object"></a>表值参数行集对象  
 您可以创建表值参数的专用行集对象。 通过使用 ITableDefinitionWithConstraints::CreateTableWithConstraints 或 IOpenRowset::OpenRowset 创建表值参数行集对象。 若要执行此操作，将设置*eKind*的成员*pTableID*参数 DBKIND_GUID_NAME，并提供为 CLSID_ROWSET_INMEMORY *guid*成员。 必须在指定服务器类型名称为表值参数*pwszName*的成员*pTableID*使用 IOpenRowset::OpenRowset 时。 表值参数行集对象的行为类似正则 OLE DB 驱动程序的 SQL Server 对象。  
  
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
  
 DBTYPE_TABLE 具有与 DBTYPE_IUNKNOWN 相同的格式。 它是指向数据缓冲区中的对象的指针。 有关在绑定中的完整说明，请使用者填满 DBOBJECT 缓冲区中，与*iid*设置为行集对象接口 (IID_IRowset) 之一。 如果在绑定中不指定任何 DBOBJECT，则将假定为 IID_IRowset。  
  
 与其他 DBTYPE_TABLE 任何其他类型的转换不受支持。 IConvertType::CanConvert 将 DBTYPE_TABLE 以外的任何请求 DBTYPE_TABLE 转换到的不支持转换为返回 S_FALSE。 这假定 DBCONVERTFLAGS_PARAMETER 命令对象上。  
  
## <a name="methods"></a>方法  
 有关 OLE DB 支持表值参数的方法的信息，请参阅[OLE DB Table-Valued 参数类型支持&#40;方法&#41;](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-methods.md)。  
  
## <a name="properties"></a>属性  
 有关 OLE DB 支持表值参数的属性的信息，请参阅[OLE DB Table-Valued 参数类型支持&#40;属性&#41;](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-properties.md)。  
  
## <a name="see-also"></a>另请参阅  
 [表值参数&#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [使用表值参数 &#40; OLE DB &#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
