---
title: 用于表值参数的 ODBC SQL 类型 |微软文档
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6aae522544f4d9532dbc2d71db1b3d55ebee3da5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297837"
---
# <a name="odbc-sql-type-for-table-valued-parameters"></a>表值参数的 ODBC SQL 类型
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  对表值参数的支持是通过新的 ODBC SQL 类型 SQL_SS_TABLE 提供的。  
  
## <a name="remarks"></a>备注  
 不能将 SQL_SS_TABLE 转换为任何其他 ODBC 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型。  
  
 SQL_SS_TABLE 如果在 SQLBind 参数*的 ValueType*参数中用作 C 数据类型，或者尝试将应用程序参数描述符 （APD） 记录中的SQL_DESC_TYPE设置为SQL_SS_TABLE，则返回SQL_ERROR，并生成使用 SQLSTATE_HY003"无效应用程序缓冲区类型"的诊断记录。  
  
 如果在 IPD 记录中将 SQL_DESC_TYPE 设置为 SQL_SS_TABLE，并且对应的应用程序参数描述符记录不为 SQL_C_DEFAULT，则会返回 SQL_ERROR，并生成带有 SQLSTATE=HY003 的诊断记录“应用程序缓冲区类型无效”。 这可以通过 SQLSetDescField、SQLSetDescRec 或 SQLBind 参数的*参数类型*发生。  
  
 如果在调用 SQLGetData 时SQL_SS_TABLE *TargetType*参数，则返回SQL_ERROR，并生成使用 SQLSTATE_HY003"无效应用程序缓冲区类型"的诊断记录。  
  
 不能将表值参数列作为 SQL_SS_TABLE 类型绑定。 如果**SQLBind 参数**调用*参数设置为*SQL_SS_TABLE，则返回SQL_ERROR，并生成使用 SQLSTATE_HY004"无效 SQL 数据类型"的诊断记录。 SQLSetDescField 和 SQLSetDescRec 也可能发生这种情况。  
  
 表值参数列值与参数和结果列具有相同的数据转换选项。  
  
 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更高版本中只能将表值参数用作输入参数。 如果尝试通过 SQLBind参数或 SQLSetDescField 将SQL_DESC_PARAMETER_TYPE设置为SQL_PARAM_INPUT以外的值，则会返回SQL_ERROR并将诊断记录添加到具有 SQLSTATE_HY105 和消息"无效参数类型"的语句中。  
  
 表值参数列不能在*StrLen_or_IndPtr*中使用SQL_DEFAULT_PARAM，因为表值参数不支持每行默认值。 应用程序可以改为将 SQL_CA_SS_COL_HAS_DEFAULT_VALUE 列属性设置为 1。 这表示该列的所有行均具有默认值。 如果*StrLen_or_IndPtr*设置为SQL_DEFAULT_PARAM，SQLExecute 或 SQLExecDirect 将返回SQL_ERROR，并且诊断记录将添加到具有 SQLSTATE_HY090 和消息"无效字符串或缓冲区长度"的消息的语句中。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;ODBC&#41;的表值参数](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
