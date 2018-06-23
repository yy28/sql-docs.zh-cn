---
title: OLE DB 表值参数类型支持 （方法） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (methods)
ms.assetid: e3c2a450-8fd4-44cb-93d8-affe1b65c68e
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e7a22684fabd74400a280396c696c7936081a8d5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128748"
---
# <a name="ole-db-table-valued-parameter-type-support-methods"></a>OLE DB 表值参数类型支持（方法）
  以下标准 OLE DB 方法支持表值参数：  
  
|方法|表值参数支持|  
|------------|-------------------------------------|  
|ITableDefinitionWithConstraints::CreateTableWithConstraints|在您了解表值参数的类型信息并且希望基于该类型信息实例化表值参数行集对象时使用。<br /><br /> 有关详细信息，请参阅"静态方案"[表值参数行集创建](table-valued-parameter-rowset-creation.md)。|  
|IOpenRowset::OpenRowset|在您不了解表值参数的类型信息并且希望基于从服务器检索的元数据信息实例化表值参数行集对象时使用。<br /><br /> 有关详细信息，请参阅"动态方案"[表值参数行集创建](table-valued-parameter-rowset-creation.md)。|  
|ISSCommandWithParameters::SetParameterInfo|若要指定表值参数的命令参数，使用者指定参数的类型为"table"或"DBTYPE_TABLE"中*pwszName* DBPARAMBINDINFO 结构的成员。 *UlParamSize*设置为 ~ 0。 详细信息，请参阅"表值参数规范"中[Executing Commands Containing Table-Valued 参数](executing-commands-containing-table-valued-parameters.md)。|  
|ISSCommandWithParameters::SetParameterProperties|设置特定于表值参数的属性，如架构名称、类型名称、列顺序和默认列。<br /><br /> 使用者指定中的参数的序号*iOrdinal*的 SSPARAMPROPS 结构。 请求的属性集为 DBPROPSET_SQLSERVERPARAMETER。|  
|ISSCommandWithParameters::GetParameterInfo|获取某一指定命令的所有参数的类型。<br /><br /> 对于表值参数， *wType* DBPARAMINFO 结构中的字段将包含类型 DBTYPE_TABLE。 *UlParamSize*字段将设置为 ~ 0 来指示未知的长度。|  
|ISSCommandWithParameters::GetParameterProperties|获取 DBTYPE_TABLE 类型的参数的附加类型信息。<br /><br /> 使用者指定中的参数的序号*iOrdinal* SSPARAMPROPS 结构中的成员。 使用者可以请求任何下列出 ISSCommandWithParameters::SetParameterProperties DBPROPSET_SQLSERVERPARAMETER 设置的属性中的属性。<br /><br /> 由于使用者不清楚表值参数类型，访问接口必须将 SSPROP_PARAM_TYPE_TYPENAME、SSPROP_PARAM_TYPE_SCHEMANAME 和 SSPROP_PARAM_TYPE_CATALOGNAME 设置为各自的正确值。 其余属性（SSPROP_PARAM_TABLE_DEFAULT_COLUMNS 和 SSPROP_PARAM_TABLE_COLUMN_SORT_ORDER）将具有各自的默认值。 使用者已发现的表值参数类型名称后，它使用 IOpenRowset::OpenRowset 来创建此表值参数，指定表值参数类型的名称的实例。 有关详细信息，请参阅[表值参数类型发现](../../database-engine/dev-guide/table-valued-parameter-type-discovery.md)。|  
|IRowsetInfo::GetProperties|获取表值参数行集属性。 使用者可以使用这些属性对绑定进行最佳设置。|  
|IColumnsRowset::GetColumnsRowset|检索有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表的元数据信息。 对于表值参数，同一接口提供有关各列的详细元数据信息，如下所示：<br /><br /> -DBCOLUMN_FLAGS 指示通过 DBCOLUMNFLAGS_ISNULLABLE 位的可为 null。<br />-DBCOLUMN_ISUNIQUE 指示列是否为标识列。<br />-DBCOLUMN_COMPUTEMODE 指示是否计算列。|  
|IAccessor::CreateAccessor|若要将表值参数行集对象绑定到命令参数，请创建访问器中的使用其*wType*成员设置为 DBTYPE_TABLE。 DBOBJECT 结构将包含 IID_IRowset 或在任何其他有效的行集对象接口*iid*成员。 其余字段的处理方式类似于 DBTYPE_IUNKNOWN。|  
  
## <a name="see-also"></a>请参阅  
 [OLE DB 表值参数类型支持](ole-db-table-valued-parameter-type-support.md)   
 [表值参数行集创建](table-valued-parameter-rowset-creation.md)   
 [使用表值参数&#40;OLE DB&#41;](table-valued-parameters-ole-db.md)  
  
  