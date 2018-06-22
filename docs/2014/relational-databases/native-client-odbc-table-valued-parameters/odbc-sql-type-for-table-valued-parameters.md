---
title: 表值参数的 ODBC SQL 类型 |Microsoft 文档
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
- SQL_SS_TABLE
ms.assetid: 6725bfb9-5f10-4115-be09-fd9c9f5779ea
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 0b537b4807dc96dcc5f3b30acbd591dc108939f2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014771"
---
# <a name="odbc-sql-type-for-table-valued-parameters"></a>表值参数的 ODBC SQL 类型
  对表值参数的支持是通过新的 ODBC SQL 类型 SQL_SS_TABLE 提供的。  
  
## <a name="remarks"></a>Remarks  
 不能将 SQL_SS_TABLE 转换为任何其他 ODBC 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型。  
  
 如果作为 C 数据类型中使用 SQL_SS_TABLE *ValueType* SQLBindParameter 或尝试参数对其进行设置 SQL_DESC_TYPE SQL_SS_TABLE 到应用程序参数描述符 (APD) 记录中，返回 SQL_ERROR 和诊断记录将生成带有 SQLSTATE = HY003，"应用程序缓冲区类型无效"。  
  
 如果在 IPD 记录中将 SQL_DESC_TYPE 设置为 SQL_SS_TABLE，并且对应的应用程序参数描述符记录不为 SQL_C_DEFAULT，则会返回 SQL_ERROR，并生成带有 SQLSTATE=HY003 的诊断记录“应用程序缓冲区类型无效”。 这可能会出现*ParameterType* SQLSetDescField、 SQLSetDescRec 或 SQLBindParameter。  
  
 如果*TargetType*调用 SQLGetData 时，参数将为 SQL_SS_TABLE，则返回 SQL_ERROR 和诊断记录将生成带有 SQLSTATE = HY003，"应用程序缓冲区类型无效"。  
  
 不能将表值参数列作为 SQL_SS_TABLE 类型绑定。 如果`SQLBindParameter`使用调用*ParameterType*设置为 SQL_SS_TABLE，返回 SQL_ERROR 和诊断记录将生成带有 SQLSTATE = HY004，"无效的 SQL 数据类型"。 这也会发生与 SQLSetDescField 和 SQLSetDescRec。  
  
 表值参数列值与参数和结果列具有相同的数据转换选项。  
  
 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更高版本中只能将表值参数用作输入参数。 如果尝试将 SQL_DESC_PARAMETER_TYPE 设置为通过 SQLBindParameter 或 SQLSetDescField SQL_PARAM_INPUT 以外的值，会返回 SQL_ERROR 并诊断记录添加到与 SQLSTATE 语句 = HY105 和消息"参数无效类型"。  
  
 表值参数列不能使用在 SQL_DEFAULT_PARAM *StrLen_or_IndPtr*，这是因为使用表值参数不支持每个行的默认值。 应用程序可以改为将 SQL_CA_SS_COL_HAS_DEFAULT_VALUE 列属性设置为 1。 这表示该列的所有行均具有默认值。 如果*StrLen_or_IndPtr*设置到 SQL_DEFAULT_PARAM，SQLExecute 或 SQLExecDirect 将返回 SQL_ERROR，并且诊断记录将添加到与 SQLSTATE 语句 = HY090 和消息"字符串或缓冲区长度无效"。  
  
## <a name="see-also"></a>请参阅  
 [表值参数&#40;ODBC&#41;](table-valued-parameters-odbc.md)  
  
  