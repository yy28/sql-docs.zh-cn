---
title: OLE DB 表值参数类型支持 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (OLE DB)
ms.assetid: 147036a0-260e-4f81-8b3b-89209e023a32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ef0667c28d87deb6c714a91bbe3605792c51c1e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48133147"
---
# <a name="ole-db-table-valued-parameter-type-support"></a>OLE DB 表值参数类型支持
  本主题介绍了表值参数的 OLE DB 类型支持。  
  
## <a name="table-valued-parameter-rowset-object"></a>表值参数行集对象  
 您可以创建表值参数的专用行集对象。 使用 ITableDefinitionWithConstraints::CreateTableWithConstraints 或 iopenrowset:: Openrowset 创建表值参数行集对象。 为此，请将 pTableID 参数的 eKind 成员设置为 DBKIND_GUID_NAME，并提供 CLSID_ROWSET_INMEMORY 作为 guid 成员。 必须在指定服务器类型名称为表值参数*pwszName*的成员*pTableID*使用 iopenrowset:: Openrowset 时。 表值参数行集对象行为与常规 SQL Server Native Client OLE DB Provider 对象类似。  
  
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
  
 DBTYPE_TABLE 具有与 DBTYPE_IUNKNOWN 相同的格式。 它是指向数据缓冲区中某个对象的指针。 为完成绑定中的规范，使用者应填充 DBOBJECT 缓冲区，并将 iid 设置为某个行集对象接口 (IID_IRowset)。 如果绑定中未指定 DBOBJECT，则将假定为 IID_IRowset。  
  
 不支持任何其他类型转换为 DBTYPE_TABLE 或从 DBTYPE_TABLE 转换为任何其他类型。 针对 DBTYPE_TABLE 到 DBTYPE_TABLE 的转换以外的任何请求，IConvertType::CanConvert 将对不支持的转换返回 S_FALSE。 这将假定对 Command 对象进行 DBCONVERTFLAGS_PARAMETER 转换。  
  
## <a name="methods"></a>方法  
 有关支持表值参数的 OLE DB 方法的信息，请参阅[OLE DB Table-Valued 参数类型支持&#40;方法&#41;](ole-db-table-valued-parameter-type-support-methods.md)。  
  
## <a name="properties"></a>属性  
 有关支持表值参数的 OLE DB 属性有关的信息，请参阅[OLE DB Table-Valued 参数类型支持&#40;属性&#41;](ole-db-table-valued-parameter-type-support-properties.md)。  
  
## <a name="see-also"></a>请参阅  
 [表值参数 (OLE DB)](table-valued-parameters-ole-db.md)   
 [使用表值参数 (OLE DB)](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
