---
title: SQLBindParameter |Microsoft 文档
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-api
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLBindParameter function
ms.assetid: c302c87a-e7f4-4d2b-a0a7-de42210174ac
caps.latest.revision: 46
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3c078adc30fee659d87e58a1ea6ac44e25e68236
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32946892"
---
# <a name="sqlbindparameter"></a>SQLBindParameter
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLBindParameter**可以消除数据转换时用于提供数据的负担[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序，从而导致的应用程序的客户端和服务器组件的显著的性能提升。 其他好处包括在插入或更新近似数字数据类型时减少精度损失。  
  
> [!NOTE]  
>  插入时**char**和**wchar**使用类型为 image 列，正在传递的数据的大小的数据，而不是转换为二进制格式后的数据的大小。  
  
 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序在某一参数数组的单个数组元素上遇到错误，则该驱动程序将继续为其余数组元素执行语句。 如果该应用程序为语句绑定了某一由参数状态元素构成的数组，则可以从该数组确定生成错误的参数行。  
  
 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序，则在绑定输入参数时指定 SQL_PARAM_INPUT。 在绑定用 OUTPUT 关键字定义的存储过程参数时，只指定 SQL_PARAM_OUTPUT 或 SQL_PARAM_INPUT_OUTPUT。  
  
 [SQLRowCount](../../relational-databases/native-client-odbc-api/sqlrowcount.md)不与可靠[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序，如果数组元素的绑定参数数组在语句执行过程中会导致错误。 ODBC 语句属性 SQL_ATTR_PARAMS_PROCESSED_PTR 报告在发生错误前已处理的行数。 然后，如有必要，该应用程序将遍历其参数状态数组，以便发现成功执行的语句数目。  
  
## <a name="binding-parameters-for-sql-character-types"></a>SQL 字符类型的绑定参数  
 如果传入的 SQL 数据类型是字符类型， *columnsize 类型*是以字符为单位 （而不是字节） 的大小。 如果以字节为单位的数据字符串的长度大于 8000， *columnsize 类型*应设置为**SQL_SS_LENGTH_UNLIMITED**，，该值指示是否有 SQL 类型的大小没有限制。  
  
 例如，如果 SQL 数据类型是**SQL_WVARCHAR**， *columnsize 类型*不应为大于 4000。 如果实际数据长度大于 4000、 然后*columnsize 类型*应设置为**SQL_SS_LENGTH_UNLIMITED**以便**nvarchar (max)** 将由驱动程序。  
  
## <a name="sqlbindparameter-and-table-valued-parameters"></a>SQLBindParameter 和表值参数  
 其他参数类型，如表值参数由 SQLBindParameter 绑定。  
  
 在已绑定某一表值参数后，也绑定其列。 若要将列绑定，请调用[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)将： SQL_SOPT_SS_PARAM_FOCUS 设置为表值参数的序号。 然后，对于表值参数中的每个列调用 SQLBindParameter。 若要返回到顶级参数绑定，请将 SQL_SOPT_SS_PARAM_FOCUS 设置为 0。  
  
 有关参数映射到表值参数的描述符字段的信息，请参阅[绑定和 Data Transfer of Table-Valued 参数和列的值](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)。  
  
 有关表值参数的详细信息，请参阅[表值参数 & #40; ODBC & #41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlbindparameter-support-for-enhanced-date-and-time-features"></a>SQLBindParameter 对日期和时间增强功能的支持  
 日期/时间类型的参数值将转换中所述[从 C 到 SQL 转换](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md)。 请注意该类型参数的**时间**和**datetimeoffset**必须具有*ValueType*指定为**SQL_C_DEFAULT**或**SQL_C_BINARY**如果及其相应的结构 (**SQL_SS_TIME2_STRUCT**和**SQL_SS_TIMESTAMPOFFSET_STRUCT**) 使用。  
  
 有关详细信息，请参阅[日期和时间改进 & #40; ODBC & #41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlbindparameter-support-for-large-clr-udts"></a>SQLBindParameter 对大型 CLR UDT 的支持  
 **SQLBindParameter**支持大型 CLR 用户定义类型 (Udt)。 有关详细信息，请参阅[Large CLR User-Defined 类型 & #40; ODBC & #41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 实现详细信息](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SQLBindParameter 函数](http://go.microsoft.com/fwlink/?LinkId=59328)  
  
  
