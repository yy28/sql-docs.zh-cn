---
title: "表值参数构成列的描述符字段 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-table-valued-parameters
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: table-valued parameters (ODBC), descriptor fields for constituent columns
ms.assetid: 944b3968-fd47-4847-98d6-b87e8ef2acdc
caps.latest.revision: "24"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e0001cdd0d2295196aa565876f8a380142ad2552
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="descriptor-fields-for-table-valued-parameter-constituent-columns"></a>表值参数构成列的描述符字段
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  在本部分中所述的表值参数描述符字段操作使用[SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md)和[SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md)与实现参数描述符 （的句柄IPD)。  
  
## <a name="remarks"></a>注释  
 SQL_DESC_AUTO_UNIQUE_VALUE 用于表值参数以及其他功能。  
  
|属性名称|类型|Description|  
|--------------------|----------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|SQL_TRUE 指示该列是标识列。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以使用此信息来优化性能，但应用程序不需要将其设置为标识列。|  
  
 以下属性将添加到应用程序参数描述符 (APD) 和实现参数描述符 (IPD) 中的所有参数类型：  
  
|属性名称|类型|Description|  
|--------------------|----------|-----------------|  
|SQL_CA_SS_COLUMN_COMPUTED|SQLSMALLINT|SQL_TRUE 指示该列是计算列。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以使用此信息来优化性能，但应用程序不需要将其设置为计算列。<br /><br /> 对于非表值参数列的绑定，将忽略此属性。|  
|SQL_CA_SS_COLUMN_IN_UNIQUE_KEY|SQLSMALLINT|SQL_TRUE 指示表值参数列参与唯一键。 这可能导致查询性能提高。 对于非表值参数列的绑定，将忽略此属性。|  
|SQL_CA_SS_COLUMN_SORT_ORDER|SQLSMALLINT|指示表值参数列的排序顺序。 这可能导致查询性能提高。 对于非表值参数列的绑定，将忽略此属性。 下面列出了可能的值： <br />**SQL_SS_ASCENDING_ORDER**<br />**SQL_SS_DESCENDING_ORDER**<br />**SQL_SS_ORDER_UNSPECIFIED**<br /><br /> 之外的其他值**SQL_SS_ASCENDING_ORDER**和**SQL_SS_DESCENDING_ORDER**生成与错误**SQLSTATE HY024**消息无效的属性值，并都是视为**SQL_SS_ORDER_UNSPECIFIED**，这是此属性的默认值。|  
|SQL_CA_SS_COLUMN_SORT_ORDINAL|SQLSMALLINT|指示表值参数列在列集中的序号，它定义表值参数的整体排序顺序。 这可能导致查询性能提高。 对于非表值参数列的绑定，将忽略此属性。 排序序号从 1 开始。 默认值 0 指示表值参数列未进行列排序。|  
|SQL_CA_SS_COLUMN_HAS_DEFAULT_VALUE|SQLSMALLINT|指示表值参数中的所有行是否都将具有此列的默认值。 对于表值参数，无法逐行选择默认值。 值 SQL_FALSE 指示行将具有非默认值。 这是默认设置。 值 SQL_TRUE 指示此列的所有行都将具有默认值。<br /><br /> 如果设置为 SQL_TRUE，则不会将任何数据发送到服务器。<br /><br /> 如果服务器处理不需要相应列值，则此字段还可以用于标识列或计算列。|  
  
 这些属性仅对表值参数列有效。 对于其他参数，将忽略它们。  
  
 如果为表值参数列设置了 SQL_CA_SS_COL_HAS_DEFAULT_VALUE，则该列的 SQL_DESC_DATA_PTR 必须为 Null 指针。 否则，SQLExecute 或 SQLExecDirect 将返回 SQL_ERROR。 将使用 SQLSTATE 生成诊断记录 = 07S01 和消息"参数不允许使用默认参数\<p >，列\<c >"，其中\<p > 是的参数序号和\<c > 是列序号。  
  
## <a name="see-also"></a>另请参阅  
 [表值参数 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
