---
title: OLE DB 表值参数类型支持（属性） | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (properties)
ms.assetid: b9c4e6ed-fe4f-4ef8-9bc8-784d80d44039
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5cdd19895a1cf91e1c5c8608013cb52482f946c5
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2018
ms.locfileid: "51559448"
---
# <a name="ole-db-table-valued-parameter-type-support-properties"></a>OLE DB 表值参数类型支持（属性）
  本主题提供有关与表值参数行集对象相关联的 OLE DB 属性和属性集的信息。  
  
## <a name="properties"></a>属性  
 以下是通过表值参数行集对象上的 irowsetinfo:: Getproperties 方法公开的属性的列表。 请注意，所有表值参数行集属性都是只读的。 因此，尝试设置任何通过 iopenrowset:: Openrowset 或 ITableDefinitionWithConstraints::CreateTableWithConstraints 属性的方法为非默认值将导致错误，并且会创建任何对象。  
  
 在此处未列出在表值参数行集对象中未实现的属性。 有关属性的完整列表，请参阅 Windows 数据访问组件中的 OLE DB 文档。  
  
|属性 ID|ReplTest1|  
|-----------------|-----------|  
|DBPROP_ABORTPRESERVE|VARIANT_TRUE|  
|DBPROP_ACCESSORDER|DBPROPVAL_AO_RANDOM|  
|DBPROP_BLOCKINGSTORAGEOBJECTS|VARIANT_TRUE|  
|DBPROP_BOOKMARKS<br /><br /> DBPROP_LITERALBOOKMARKS|R/W：只读<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：在表值参数行集对象上不允许书签。|  
|DBPROP_BOOKMARKSKIPPED|VARIANT_FALSE|  
|DBPROP_BOOKMARKTYPE|DBPROPVAL_BMK_NUMERIC|  
|DBPROP_CANHOLDROWS|VARIANT_FALSE|  
|DBPROP_CHANGEINSERTEDROWS|VARIANT_TRUE|  
|DBPROP_COLUMNRESTRICT|VARIANT_FALSE|  
|DBPROP_COMMANDTIMEOUT|0|  
|DBPROP_COMMITPRESERVE|VARIANT_TRUE|  
|DBPROP_DEFERRED|VARIANT_FALSE|  
|DBPROP_DELAYSTORAGEOBJECTS|VARIANT_FALSE|  
|DBPROP_IAccessor<br /><br /> DBPROP_IColumnsInfo<br /><br /> DBPROP_IConvertType<br /><br /> DBPROP_IRowset<br /><br /> DBPROP_IRowsetInfo,<br /><br /> DBPROP_IColumnsRowset|VARIANT_TRUE|  
|DBPROP_IConnectionPointContainer<br /><br /> DBPROP_IMultipleResults<br /><br /> DBPROP_IRowsetUpdate<br /><br /> DBPROP_IRowsetIdentity<br /><br /> DBPROP_IRowsetLocate<br /><br /> DBPROP_IRowsetScroll<br /><br /> DBPROP_IRowsetResynch|VARIANT_FALSE|  
|DBPROP_IRowsetChange|VARIANT_TRUE<br /><br /> 注意：表值参数行集对象支持 IRowsetChange 接口。<br /><br /> 通过使用 DBPROP_IRowsetChange 等于 VARIANT_TRUE 而创建的行集将展现立即更新模式行为。<br /><br /> 但是，如果 BLOB 列绑定用作 ISequentialStream 对象，则使用者应在该表值参数行集对象的整个生存期中保留这些列。|  
|DBPROP_ISupportErrorInfo|VARIANT_TRUE|  
|DBPROP_ISequentialStream|VARIANT_TRUE|  
|DBPROP_IMMOBILEROWS|VARIANT_TRUE|  
|DBPROP_LITERALIDENTITY|VARIANT_TRUE|  
|DBPROP_LOCKMODE|DBPROPVAL_LM_NONE|  
|DBPROP_MAXOPENROWS|0|  
|DBPROP_MAXPENDINGROWS|0|  
|DBPROP_MAXROWS|0|  
|DBPROP_NOTIFICATIONPHASES|0|  
|DBPROP_NOTIFYCOLUMNSET DBPROP_NOTIFYROWDELETE DBPROP_NOTIFYROWFIRSTCHANGE DBPROP_NOTIFYROWINSERT DBPROP_NOTIFYROWRESYNCH DBPROP_NOTIFYROWSETRELEASE DBPROP_NOTIFYROWSETFETCH-POSITIONCHANGE DBPROP_NOTIFYROWUNDOCHANGE DBPROP_NOTIFYROWUNDODELETE DBPROP_NOTIFYROWUNDOINSERT DBPROP_NOTIFYROWUPDATE|0|  
|DBPROP_OTHERINSERT DBPROP_OTHERUPDATEDELETE|VARIANT_FALSE|  
|DBPROP_OWNINSERT<br /><br /> DBPROP_OWNUPDATEDELETE|VARIANT_TRUE|  
|DBPROP_QUICKRESTART|VARIANT_TRUE|  
|DBPROP_REENTRANTEVENTS|VARIANT_FALSE|  
|DBPROP_REMOVEDELETED|VARIANT_TRUE|  
|DBPROP_RETURNPENDINGINSERTS|VARIANT_TRUE|  
|DBPROP_ROWRESTRICT|VARIANT_FALSE|  
|DBPROP_ROWTHREADMODEL|DBPROPVAL_RT_FREETHREAD|  
|DBPROP_SERVERCURSOR|VARIANT_FALSE|  
|DBPROP_SERVERDATAONINSERT|VARIANT_FALSE|  
|DBPROP_STRONGIDENTITY|VARIANT_TRUE|  
|DBPROP_TRANSACTEDOBJECT|VARIANT_FALSE|  
|DBPROP_UNIQUEROWS|VARIANT_FALSE|  
|DBPROP_UPDATABILITY|DBPROPVAL_UP_CHANGE &#124; DBPROPVAL_UP_DELETE &#124; DBPROPVAL_UP_INSERT|  
  
## <a name="property-sets"></a>属性集  
 以下属性集支持表值参数。  
  
### <a name="dbpropsetsqlservercolumn"></a>DBPROPSET_SQLSERVERCOLUMN  
 如果需要通过 ITableDefinitionWithConstraints::CreateTableWithConstraints 用于通过 DBCOLUMNDESC 结构的每个列创建表值参数行集对象的过程中使用者使用此属性。  
  
|属性 ID|属性值|  
|-----------------|--------------------|  
|SSPROP_COL_COMPUTED|R/W：读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 类型：VT_BOOL<br /><br /> 说明：在设置为 VARIANT_TRUE 时，指示该列是计算列。 VARIANT_FALSE 指示它不是计算列。|  
  
### <a name="dbpropsetsqlserverparameter"></a>DBPROPSET_SQLSERVERPARAMETER  
 这些属性是由使用者读取发现对 isscommandwithparameters:: Getparameterproperties 的调用中的表值参数类型信息时，由使用者设置有关表值参数的特定属性时设置通过 isscommandwithparameters:: Setparameterproperties。  
  
 下表详细说明了这些属性。  
  
|属性 ID|属性值|  
|-----------------|--------------------|  
|SSPROP_PARAM_TYPE_TYPENAME|R/W：读/写<br /><br /> 默认值：VT_EMPTY<br /><br /> 类型：VT_BSTR<br /><br /> 说明：使用者使用此属性获取或设置表值参数类型的名称。<br /><br /> 此属性还可以用于 CLR 用户定义类型。<br /><br /> 可以选择指定此属性，以便为表值参数提供表类型名称（在 ODBC 调用语法命令的情况下）。 此属性是即席参数化 SQL 查询所必需的。|  
|SSPROP_PARAM_TYPE_SCHEMANAME|R/W：读/写<br /><br /> 默认值：VT_EMPTY<br /><br /> 类型：VT_BSTR<br /><br /> 说明：使用者使用此属性获取或设置表值参数类型的架构名称。<br /><br /> 此属性还可以用于 CLR 用户定义类型。|  
|SSPROP_PARAM_TYPE_CATALOGNAME|R/W：只读<br /><br /> 默认值：VT_EMPTY<br /><br /> 类型：VT_BSTR<br /><br /> 说明：使用者使用此属性获取表值参数类型的目录名称。<br /><br /> 此属性还可以用于 CLR 用户定义类型。 设置此属性是错误的；用户定义表类型必须与使用它们的表值参数处于同一数据库中。|  
|SSPROP_PARAM_TABLE_DEFAULT_COLUMNS|R/W：读/写<br /><br /> 默认值：VT_EMPTY<br /><br /> 类型： VT_UI2 &#124; VT_ARRAY<br /><br /> 说明：使用者使用此属性指定行集中哪些列集要视作默认值。 将不为这些列发送值。 在从使用者行集对象提取数据时，提供程序不要求对此类列的绑定。<br /><br /> 数组中的每个元素都应是行集对象中某一列的序号。 无效的序号将导致在执行命令时发生错误。|  
|SSPROP_PARAM_TABLE_COLUMN_ORDER|R/W：读/写<br /><br /> 默认值：VT_EMPTY<br /><br /> 类型： VT_UI2 &#124; VT_ARRAY<br /><br /> 说明：使用者使用此属性向服务器提供提示，以便指出列数据的排序顺序。 提供程序不执行任何验证，并且假定使用者符合已提供的规范。 服务器使用此属性执行优化。<br /><br /> 每一列的列顺序信息均由数组中的一对元素表示。 该元素对中的第一个元素是列的编号。 该元素对中的第二个元素将是 1 或 2，分别表示升序或降序。|  
  
## <a name="see-also"></a>请参阅  
 [OLE DB 表值参数类型支持](ole-db-table-valued-parameter-type-support.md)   
 [使用表值参数 (OLE DB)](table-valued-parameters-ole-db.md)  
  
  
