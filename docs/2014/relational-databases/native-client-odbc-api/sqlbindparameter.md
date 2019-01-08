---
title: SQLBindParameter |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLBindParameter function
ms.assetid: c302c87a-e7f4-4d2b-a0a7-de42210174ac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cba973be9b4dc2ec0da286b2d01b636f0ca4e2b4
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53364689"
---
# <a name="sqlbindparameter"></a>SQLBindParameter
  `SQLBindParameter` 可以消除数据转换时用于提供数据的负担[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序，从而导致应用程序的客户端和服务器组件的显著的性能提升。 其他好处包括在插入或更新近似数字数据类型时减少精度损失。  
  
> [!NOTE]  
>  在将 `char` 和 `wchar` 类型数据插入某一图像列时，将使用要传入的数据的大小，而非转换为二进制格式后的数据大小。  
  
 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序在某一参数数组的单个数组元素上遇到错误，则该驱动程序将继续为其余数组元素执行语句。 如果该应用程序为语句绑定了某一由参数状态元素构成的数组，则可以从该数组确定生成错误的参数行。  
  
 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序，则在绑定输入参数时指定 SQL_PARAM_INPUT。 在绑定用 OUTPUT 关键字定义的存储过程参数时，只指定 SQL_PARAM_OUTPUT 或 SQL_PARAM_INPUT_OUTPUT。  
  
 [SQLRowCount](sqlrowcount.md)不与可靠[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序绑定参数数组的数组元素在语句执行过程中导致错误。 ODBC 语句属性 SQL_ATTR_PARAMS_PROCESSED_PTR 报告在发生错误前已处理的行数。 然后，如有必要，该应用程序将遍历其参数状态数组，以便发现成功执行的语句数目。  
  
## <a name="binding-parameters-for-sql-character-types"></a>SQL 字符类型的绑定参数  
 如果传入的 SQL 数据类型为字符类型， *ColumnSize*是以字符为单位 （而非字节） 的大小。 如果以字节为单位的数据字符串的长度大于 8000， *ColumnSize*应设置为`SQL_SS_LENGTH_UNLIMITED`，，该值指示是否有 SQL 类型的大小没有限制。  
  
 例如，如果 SQL 数据类型为`SQL_WVARCHAR`， *ColumnSize*不应超过 4000。 如果实际数据长度大于 4000，然后*ColumnSize*应设置为`SQL_SS_LENGTH_UNLIMITED`以便`nvarchar(max)`将由驱动程序。  
  
## <a name="sqlbindparameter-and-table-valued-parameters"></a>SQLBindParameter 和表值参数  
 其他参数类型，如表值参数绑定的是 SQLBindParameter。  
  
 在已绑定某一表值参数后，也绑定其列。 若要绑定的列，请调用[SQLSetStmtAttr](sqlsetstmtattr.md)将 SQL_SOPT_SS_PARAM_FOCUS 设置为表值参数的序号。 然后，对于表值参数中每个列调用 SQLBindParameter。 若要返回到顶级参数绑定，请将 SQL_SOPT_SS_PARAM_FOCUS 设置为 0。  
  
 有关将参数映射到表值参数的描述符字段的信息，请参阅[绑定和 Data Transfer of Table-Valued 参数和列值](../native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)。  
  
 有关表值参数的详细信息，请参阅[表值参数&#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlbindparameter-support-for-enhanced-date-and-time-features"></a>SQLBindParameter 对日期和时间增强功能的支持  
 参数值的日期/时间类型转换中所述[从 C 到 SQL 转换](../native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md)。 请注意该类型的参数`time`并`datetimeoffset`必须具有*ValueType*指定为`SQL_C_DEFAULT`或`SQL_C_BINARY`如果其相应结构 (`SQL_SS_TIME2_STRUCT`和`SQL_SS_TIMESTAMPOFFSET_STRUCT`) 使用。  
  
 有关详细信息，请参阅[日期和时间改进&#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlbindparameter-support-for-large-clr-udts"></a>SQLBindParameter 对大型 CLR UDT 的支持  
 `SQLBindParameter` 支持大型 CLR 用户定义类型 (UDT)。 有关详细信息，请参阅[Large CLR User-Defined 类型&#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 实现的详细信息](odbc-api-implementation-details.md)   
 [SQLBindParameter 函数](https://go.microsoft.com/fwlink/?LinkId=59328)  
  
  
