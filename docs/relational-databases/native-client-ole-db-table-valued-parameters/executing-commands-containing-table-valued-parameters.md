---
title: 执行包含表值参数的命令 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-ole-db-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, executing commands containing
ms.assetid: 7ecba6f6-fe7a-462a-9aa3-d5115b6d4529
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 14b5e3e205abaccb2a77ea0278e9e4bcc087608b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="executing-commands-containing-table-valued-parameters"></a>执行包含表值参数的命令
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  执行包含表值参数的命令需要两个阶段：  
  
1.  指定的参数类型。  
  
2.  绑定参数数据。  
  
## <a name="table-valued-parameter-specification"></a>指定表值参数  
 使用者可以指定表值参数的类型。 此信息包括表值参数的类型名称。 如果连接的当前默认架构中不存在该表值参数的用户定义表类型，则它还包括架构名称。 根据服务器的支持情况，使用者还可以指定可选的元数据信息（如列的排序），以及指定特定列的所有行都具有默认值。  
  
 若要指定表值参数，使用者调用 ISSCommandWithParamter::SetParameterInfo，并根据需要调用 ISSCommandWithParameters::SetParameterProperties。 表值参数， *pwszDataSourceType* DBPARAMBINDINFO 结构中的字段具有 DBTYPE_TABLE 的值。 *UlParamSize*字段设置为 ~ 0 来指示该长度是未知。 可以通过 ISSCommandWithParameters::SetParameterProperties 设置表值参数，如架构名称、 类型名称、 列顺序和默认列的特定属性。  
  
## <a name="table-valued-parameter-binding"></a>绑定表值参数  
 表值参数可以是任意行集对象。 访问接口在执行期间从该对象中读取数据并将表值参数发送到服务器。  
  
 若要绑定的表值参数，使用者调用 IAccessor::CreateAccessor。 *WType*的表值参数的 DBBINDING 结构的字段设置为 DBTYPE_TABLE。 *PObject* DBBINDING 结构中的成员为非 NULL，与*pObject*的*iid*成员设置为 IID_IRowset 或任何其他表值参数行集对象接口。 DBBINDING 结构中其余字段的设置方式应与流式 BLOB 的对应字段的设置方式相同。  
  
 对于表值参数以及与表值参数关联的行集对象的绑定，存在如下限制：  
  
-   对于表值参数行集列数据，允许使用的状态值只有 DBSTATUS_S_ISNULL 和 DBSTATUS_S_OK。 DBSTATUS_S_DEFAULT 将导致失败，并且绑定的状态值将设置为 DBSTATUS_E_BADSTATUS。  
  
-   可以使用状态 DBSTATUS_S_DEFAULT 标记表值参数。 有效值只有 DBSTATUS_S_DEFAULT 和 DBSTATUS_S_OK。 当状态设置为 DBSTATUS_S_DEFAULT 时，表值参数的值将对应一个空表。  
  
-   必须使用 SSPROP_PARAM_TABLE_DEFAULT_COLUMNS 属性将表值参数中的只读列（标识列或计算列）标记为采用默认值。 此外，还必须通过 SSPROP_PARAM_TABLE_DEFAULT_COLUMNS 属性将具有默认值的列标记为采用默认值，以允许针对特定表值参数为相应列的数据值使用默认值。 访问接口将忽略为标记为采用默认值的列绑定的数据值。  
  
-   对于具有 DBPROP_COL_AUTOINCREMENT 或 SSPROP_COL_COMPUTED 的列，数据将发送到服务器，除非还设置了 SSPROP_PARAM_TABLE_DEFAULT。  
  
## <a name="see-also"></a>另请参阅  
 [表值参数&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [使用表值参数 & #40; OLE DB & #41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
