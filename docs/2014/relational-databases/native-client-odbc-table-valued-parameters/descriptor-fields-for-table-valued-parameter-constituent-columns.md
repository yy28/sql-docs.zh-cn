---
title: 表值参数构成列的描述符字段 |Microsoft 文档
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
- table-valued parameters (ODBC), descriptor fields for constituent columns
ms.assetid: 944b3968-fd47-4847-98d6-b87e8ef2acdc
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6888494d35b16987cf5d3b3e8a55a44784d2ca11
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026113"
---
# <a name="descriptor-fields-for-table-valued-parameter-constituent-columns"></a>表值参数构成列的描述符字段
  在本部分中所述的表值参数描述符字段操作使用[SQLSetDescField](../native-client-odbc-api/sqlsetdescfield.md)和[SQLSetDescField](../native-client-odbc-api/sqlsetdescfield.md)与实现参数描述符 （的句柄IPD)。  
  
## <a name="remarks"></a>Remarks  
 SQL_DESC_AUTO_UNIQUE_VALUE 用于表值参数以及其他功能。  
  
|属性名称|类型|Description|  
|--------------------|----------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|SQL_TRUE 指示该列是标识列。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以使用此信息来优化性能，但应用程序不需要将其设置为标识列。|  
  
 以下属性将添加到应用程序参数描述符 (APD) 和实现参数描述符 (IPD) 中的所有参数类型：  
  
|属性名称|类型|Description|  
|--------------------|----------|-----------------|  
|SQL_CA_SS_COLUMN_COMPUTED|SQLSMALLINT|SQL_TRUE 指示该列是计算列。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以使用此信息来优化性能，但应用程序不需要将其设置为计算列。<br /><br /> 对于非表值参数列的绑定，将忽略此属性。|  
|SQL_CA_SS_COLUMN_IN_UNIQUE_KEY|SQLSMALLINT|SQL_TRUE 指示表值参数列参与唯一键。 这可能导致查询性能提高。 对于非表值参数列的绑定，将忽略此属性。|  
|SQL_CA_SS_COLUMN_SORT_ORDER|SQLSMALLINT|指示表值参数列的排序顺序。 这可能导致查询性能提高。 对于非表值参数列的绑定，将忽略此属性。 下面列出了可能的值：<br /><br /> -SQL_SS_ASCENDING_ORDER<br />-SQL_SS_DESCENDING_ORDER<br />-SQL_SS_ORDER_UNSPECIFIED<br /><br /> SQL_SS_ASCENDING_ORDER 和 SQL_SS_DESCENDING_ORDER 以外的值将产生 SQLSTATE 为 HY024 的错误和“属性值无效”消息，并且将被视为此属性的默认值 SQL_SS_ORDER_UNSPECIFIED。|  
|SQL_CA_SS_COLUMN_SORT_ORDINAL|SQLSMALLINT|指示表值参数列在列集中的序号，它定义表值参数的整体排序顺序。 这可能导致查询性能提高。 对于非表值参数列的绑定，将忽略此属性。 排序序号从 1 开始。 默认值 0 指示表值参数列未进行列排序。|  
|SQL_CA_SS_COLUMN_HAS_DEFAULT_VALUE|SQLSMALLINT|指示表值参数中的所有行是否都将具有此列的默认值。 对于表值参数，无法逐行选择默认值。 值 SQL_FALSE 指示行将具有非默认值。 这是默认设置。 值 SQL_TRUE 指示此列的所有行都将具有默认值。<br /><br /> 如果设置为 SQL_TRUE，则不会将任何数据发送到服务器。<br /><br /> 如果服务器处理不需要相应列值，则此字段还可以用于标识列或计算列。|  
  
 这些属性仅对表值参数列有效。 对于其他参数，将忽略它们。  
  
 如果为表值参数列设置了 SQL_CA_SS_COL_HAS_DEFAULT_VALUE，则该列的 SQL_DESC_DATA_PTR 必须为 Null 指针。 否则，SQLExecute 或 SQLExecDirect 将返回 SQL_ERROR。 将使用 SQLSTATE 生成诊断记录 = 07S01 和消息"参数不允许使用默认参数\<p >，列\<c >"，其中\<p > 是的参数序号和\<c > 是列序号。  
  
## <a name="see-also"></a>请参阅  
 [表值参数&#40;ODBC&#41;](table-valued-parameters-odbc.md)  
  
  