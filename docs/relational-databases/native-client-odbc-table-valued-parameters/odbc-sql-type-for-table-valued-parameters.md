---
title: 用于表值参数的 ODBC SQL 类型 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL_SS_TABLE
ms.assetid: 6725bfb9-5f10-4115-be09-fd9c9f5779ea
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: beafe79839842f530d4864339da53a7781123447
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "73776409"
---
# <a name="odbc-sql-type-for-table-valued-parameters"></a>表值参数的 ODBC SQL 类型
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  对表值参数的支持是通过新的 ODBC SQL 类型 SQL_SS_TABLE 提供的。  
  
## <a name="remarks"></a>备注  
 不能将 SQL_SS_TABLE 转换为任何其他 ODBC 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型。  
  
 如果 SQL_SS_TABLE 在 SQLBindParameter 的*ValueType*参数中用作 C 数据类型，或者尝试将应用程序参数描述符（APD）记录中的 SQL_DESC_TYPE 设置为 SQL_SS_TABLE，则返回 SQL_ERROR 并使用 SQLSTATE = HY003、"应用程序缓冲区类型无效" 生成诊断记录。  
  
 如果在 IPD 记录中将 SQL_DESC_TYPE 设置为 SQL_SS_TABLE，并且对应的应用程序参数描述符记录不为 SQL_C_DEFAULT，则会返回 SQL_ERROR，并生成带有 SQLSTATE=HY003 的诊断记录“应用程序缓冲区类型无效”。 SQLSetDescField、SQLSetDescRec 或 SQLBindParameter 的*ParameterType*可能会发生这种情况。  
  
 如果在调用 SQLGetData 时 SQL_SS_TABLE 了*TargetType*参数，则返回 SQL_ERROR，并生成包含 SQLSTATE = HY003，"应用程序缓冲区类型无效" 的诊断记录。  
  
 不能将表值参数列作为 SQL_SS_TABLE 类型绑定。 如果在将*ParameterType*设置为 SQL_SS_TABLE 的情况下调用**SQLBindParameter** ，则返回 SQL_ERROR，并生成包含 SQLSTATE = HY004 "SQL 数据类型无效" 的诊断记录。 SQLSetDescField 和 SQLSetDescRec 也会出现这种情况。  
  
 表值参数列值与参数和结果列具有相同的数据转换选项。  
  
 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更高版本中只能将表值参数用作输入参数。 如果尝试通过 SQLBindParameter 或 SQLSetDescField 将 SQL_DESC_PARAMETER_TYPE 设置为 SQL_PARAM_INPUT 以外的值，则返回 SQL_ERROR，并将诊断记录添加到 SQLSTATE = HY105 和消息 "参数无效键入 "。  
  
 表值参数列无法在*StrLen_or_IndPtr*中使用 SQL_DEFAULT_PARAM，因为表值参数不支持每行的默认值。 应用程序可以改为将 SQL_CA_SS_COL_HAS_DEFAULT_VALUE 列属性设置为 1。 这表示该列的所有行均具有默认值。 如果*StrLen_or_IndPtr*设置为 SQL_DEFAULT_PARAM，则 SQLExecute 或 SQLExecDirect 将返回 SQL_ERROR，并且将使用 SQLSTATE = HY090 和消息 "字符串或缓冲区长度无效" 将诊断记录添加到语句中。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC&#41;&#40;表值参数](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
