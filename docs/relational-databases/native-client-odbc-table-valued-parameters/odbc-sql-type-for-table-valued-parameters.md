---
title: 表值参数的 ODBC SQL 类型 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL_SS_TABLE
ms.assetid: 6725bfb9-5f10-4115-be09-fd9c9f5779ea
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 8353afa21266fdcb0e9a04e03cedee7113d634c2
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39542067"
---
# <a name="odbc-sql-type-for-table-valued-parameters"></a>表值参数的 ODBC SQL 类型
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  对表值参数的支持是通过新的 ODBC SQL 类型 SQL_SS_TABLE 提供的。  
  
## <a name="remarks"></a>Remarks  
 不能将 SQL_SS_TABLE 转换为任何其他 ODBC 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型。  
  
 如果 SQL_SS_TABLE 用作中的 C 数据类型*ValueType* SQLBindParameter 或尝试的参数进行为 SQL_SS_TABLE 应用程序参数描述符 (APD) 记录中的 SQL_DESC_TYPE 设置，则返回 SQL_ERROR 并诊断记录生成具有 SQLSTATE = HY003，"应用程序缓冲区类型无效"。  
  
 如果在 IPD 记录中将 SQL_DESC_TYPE 设置为 SQL_SS_TABLE，并且对应的应用程序参数描述符记录不为 SQL_C_DEFAULT，则会返回 SQL_ERROR，并生成带有 SQLSTATE=HY003 的诊断记录“应用程序缓冲区类型无效”。 这可能会出现*ParameterType* SQLSetDescField、 SQLSetDescRec 或 SQLBindParameter。  
  
 如果*TargetType*时调用 SQLGetData，参数为 SQL_SS_TABLE，则返回 SQL_ERROR 并诊断记录生成带有 SQLSTATE = HY003，"应用程序缓冲区类型无效"。  
  
 不能将表值参数列作为 SQL_SS_TABLE 类型绑定。 如果**SQLBindParameter**使用调用*ParameterType*设置为 SQL_SS_TABLE，则返回 SQL_ERROR 并的诊断记录生成带有 SQLSTATE = HY004，"SQL 数据类型无效"。 SQLSetDescField 和 SQLSetDescRec，这也会发生。  
  
 表值参数列值与参数和结果列具有相同的数据转换选项。  
  
 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更高版本中只能将表值参数用作输入参数。 如果尝试将 SQL_DESC_PARAMETER_TYPE 设置为通过 SQLBindParameter 或 SQLSetDescField SQL_PARAM_INPUT 以外的值，则返回 SQL_ERROR，并的诊断记录添加到语句具有 SQLSTATE = HY105 和消息"参数无效类型"。  
  
 表值参数列不能使用在 SQL_DEFAULT_PARAM *StrLen_or_IndPtr*，因为与表值参数不支持按行默认值。 应用程序可以改为将 SQL_CA_SS_COL_HAS_DEFAULT_VALUE 列属性设置为 1。 这表示该列的所有行均具有默认值。 如果*StrLen_or_IndPtr*设置为 SQL_DEFAULT_PARAM，SQLExecute 或 SQLExecDirect 将返回 SQL_ERROR，且的诊断记录将添加到语句具有 SQLSTATE = HY090 和消息"字符串或缓冲区长度无效"。  
  
## <a name="see-also"></a>请参阅  
 [表值参数&#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
