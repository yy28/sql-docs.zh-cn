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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63067813"
---
# <a name="sqlbindparameter"></a>SQLBindParameter
  `SQLBindParameter`当用于为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE client ODBC 驱动程序提供数据时，可以消除数据转换的负担，从而提高应用程序的客户端和服务器组件的性能。 其他好处包括在插入或更新近似数字数据类型时减少精度损失。  
  
> [!NOTE]  
>  在将 `char` 和 `wchar` 类型数据插入某一图像列时，将使用要传入的数据的大小，而非转换为二进制格式后的数据大小。  
  
 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序在某一参数数组的单个数组元素上遇到错误，则该驱动程序将继续为其余数组元素执行语句。 如果该应用程序为语句绑定了某一由参数状态元素构成的数组，则可以从该数组确定生成错误的参数行。  
  
 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序，则在绑定输入参数时指定 SQL_PARAM_INPUT。 在绑定用 OUTPUT 关键字定义的存储过程参数时，只指定 SQL_PARAM_OUTPUT 或 SQL_PARAM_INPUT_OUTPUT。  
  
 [](sqlrowcount.md)如果绑定参数数组的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数组元素导致语句执行出错，则 Native Client ODBC 驱动程序的 SQLRowCount 不可靠。 ODBC 语句属性 SQL_ATTR_PARAMS_PROCESSED_PTR 报告在发生错误前已处理的行数。 然后，如有必要，该应用程序将遍历其参数状态数组，以便发现成功执行的语句数目。  
  
## <a name="binding-parameters-for-sql-character-types"></a>SQL 字符类型的绑定参数  
 如果传入的 SQL 数据类型为字符类型，则*ColumnSize*的大小以字符（而非字节）为单位。 如果数据字符串的长度大于8000，则应将*ColumnSize*设置为`SQL_SS_LENGTH_UNLIMITED`，以指示对 SQL 类型的大小没有限制。  
  
 例如，如果 SQL 数据类型为`SQL_WVARCHAR`，则*ColumnSize*不应大于4000。 如果实际数据长度大于4000，则应将*ColumnSize*设置为`SQL_SS_LENGTH_UNLIMITED` ，以便`nvarchar(max)`驱动程序使用。  
  
## <a name="sqlbindparameter-and-table-valued-parameters"></a>SQLBindParameter 和表值参数  
 与其他参数类型一样，表值参数由 SQLBindParameter 绑定。  
  
 在已绑定某一表值参数后，也绑定其列。 若要绑定列，请调用[SQLSetStmtAttr](sqlsetstmtattr.md) ，将 SQL_SOPT_SS_PARAM_FOCUS 设置为表值参数的序号。 然后，为表值参数中的每一列调用 SQLBindParameter。 若要返回到顶级参数绑定，请将 SQL_SOPT_SS_PARAM_FOCUS 设置为 0。  
  
 有关将参数映射到表值参数的描述符字段的信息，请参阅[表值参数和列值的绑定和数据传输](../native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)。  
  
 有关表值参数的详细信息，请参阅[ODBC&#41;&#40;表值参数](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlbindparameter-support-for-enhanced-date-and-time-features"></a>SQLBindParameter 对日期和时间增强功能的支持  
 日期/时间类型的参数值按[从 C 转换到 SQL](../native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md)中所述的方式进行转换。 请注意， `time`类型为的`datetimeoffset`参数必须将*ValueType*指定`SQL_C_DEFAULT`为`SQL_C_BINARY` ，如果使用其对应`SQL_SS_TIME2_STRUCT`的`SQL_SS_TIMESTAMPOFFSET_STRUCT`结构（和），则为。  
  
 有关详细信息，请参阅[ODBC&#41;&#40;日期和时间改进](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlbindparameter-support-for-large-clr-udts"></a>SQLBindParameter 对大型 CLR UDT 的支持  
 
  `SQLBindParameter` 支持大型 CLR 用户定义类型 (UDT)。 有关详细信息，请参阅[&#40;ODBC&#41;的大型 CLR 用户定义类型](../native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 实现细节](odbc-api-implementation-details.md)   
 [SQLBindParameter 函数](https://go.microsoft.com/fwlink/?LinkId=59328)  
  
  
