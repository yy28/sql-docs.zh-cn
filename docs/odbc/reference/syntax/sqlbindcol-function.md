---
title: SQLBindCol 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLBindCol
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLBindCol
helpviewer_keywords:
- SQLBindCol function [ODBC]
ms.assetid: 41a37655-84cd-423f-9daa-e0b47b88dc54
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 27b78b2b74e4990ce22d47fd433ae7147fc3d536
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sqlbindcol-function"></a>SQLBindCol 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLBindCol**将应用程序数据缓冲区绑定到结果集中的列。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLBindCol(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   ColumnNumber,  
      SQLSMALLINT    TargetType,  
      SQLPOINTER     TargetValuePtr,  
      SQLLEN         BufferLength,  
      SQLLEN *       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *ColumnNumber*  
 [输入]要绑定的列集的结果数。 按从 0 开始，其中第 0 列书签列的递增列顺序对列进行编号。 如果未使用书签 — 即 SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_OFF-然后列编号从 1 开始。  
  
 *TargetType*  
 [输入]C 数据类型的标识符\* *TargetValuePtr*缓冲区。 当它从数据源检索数据**SQLFetch**， **SQLFetchScroll**， **SQLBulkOperations**，或**SQLSetPos**，驱动程序将数据转换为此类型;当其将数据发送到数据源**SQLBulkOperations**或**SQLSetPos**，驱动程序将数据转换从该类型。 有关有效的 C 数据类型和类型标识符的列表，请参阅[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)附录 d： 数据类型中的部分。  
  
 如果*TargetType*自变量不是间隔数据类型，默认时间间隔前导精度 (2) 和默认间隔秒精度 (6) 中的 SQL_DESC_DATETIME_INTERVAL_PRECISION 和 SQL_DESC_PRECISION 字段设置ARD，分别用于数据。 如果*TargetType*自变量是 SQL_C_NUMERIC，（驱动程序定义） 的默认精度和 ARD SQL_DESC_PRECISION 和 SQL_DESC_SCALE 字段中设置默认小数位数 (0)，用于的数据。 如果任何默认精度或小数位数不合适，应用程序显式应通过调用设置适当的描述符字段**SQLSetDescField**或**SQLSetDescRec**。  
  
 你还可以指定扩展的 C 数据类型。 有关详细信息，请参阅[ODBC 中的 C 数据类型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
 *TargetValuePtr*  
 [延迟的输入/输出]指向要将绑定到列的数据缓冲区的指针。 **SQLFetch**和**SQLFetchScroll**在此缓冲区中返回数据。 **SQLBulkOperations**返回数据，在此缓冲区时*操作*是 SQL_FETCH_BY_BOOKMARK; 它从此检索数据的缓冲区时*操作*SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK。 **SQLSetPos**返回数据，在此缓冲区时*操作*是 SQL_REFRESH; 它从此检索数据的缓冲区时*操作*是 SQL_UPDATE。  
  
 如果*TargetValuePtr*是 null 指针，该驱动程序解除绑定列的数据缓冲区。 应用程序可以通过调用取消绑定所有列**SQLFreeStmt** SQL_UNBIND 选项。 应用程序可以取消绑定列的数据缓冲区，但如果仍有长度/指示器缓冲区列中，绑定*TargetValuePtr*对的调用中的自变量**SQLBindCol**是 null 指针，但*StrLen_or_IndPtr*参数是一个有效的值。  
  
 *BufferLength*  
 [输入]长度 **TargetValuePtr*以字节为单位的缓冲区。  
  
 驱动程序使用*BufferLength*为了避免超出末尾的\* *TargetValuePtr*缓冲当它返回可变长度数据，如字符或二进制数据。 请注意该驱动程序，它返回到的字符数据时都计的 null 终止字符\* *TargetValuePtr*。 **TargetValuePtr*因此必须包含空间的 null 终止字符或驱动程序将截断数据。  
  
 在驱动程序返回固定长度的数据，如整数或日期结构，该驱动程序会忽略*BufferLength*并假定缓冲区为大到足以保留数据。 因此，务必要为固定长度的数据分配足够大的缓冲区的应用程序或驱动程序将写入缓冲区的末尾。  
  
 **SQLBindCol**返回 SQLSTATE HY090 （无效字符串或缓冲区长度） 时*BufferLength*是小于 0，但不是在*BufferLength*为 0。 但是，如果*TargetType*指定字符的类型，应用程序不应设置*BufferLength*为 0，因为符合 ISO CLI – 驱动程序返回 SQLSTATE HY090 （无效字符串或缓冲区长度），用例。  
  
 *StrLen_or_IndPtr*  
 [延迟的输入/输出]指向要将绑定到列的长度/指示器缓冲区的指针。 **SQLFetch**和**SQLFetchScroll**此缓冲区中返回值。 **SQLBulkOperations**检索一个值，从该缓冲区时*操作*是 SQL_ADD、 SQL_UPDATE_BY_BOOKMARK，还是 SQL_DELETE_BY_BOOKMARK。 **SQLBulkOperations**返回一个值在此缓冲区时*操作*是 SQL_FETCH_BY_BOOKMARK。 **SQLSetPos**返回一个值在此缓冲区时*操作*是 SQL_REFRESH; 它从这检索某个值的缓冲区时*操作*是 SQL_UPDATE。  
  
 **SQLFetch**， **SQLFetchScroll**， **SQLBulkOperations**，和**SQLSetPos**可以返回长度/指示器缓冲区中的以下值：  
  
-   可用于返回数据的长度  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 应用程序可以将以下值放在与一起使用的长度/指示器缓冲区**SQLBulkOperations**或**SQLSetPos**:  
  
-   所发送的数据的长度  
  
-   SQL_NTS 以  
  
-   SQL_NULL_DATA  
  
-   SQL_DATA_AT_EXEC  
  
-   SQL_LEN_DATA_AT_EXEC 宏的结果  
  
-   SQL_COLUMN_IGNORE  
  
 如果指示器缓冲区和长度缓冲区都是单独的缓冲区，指示器缓冲区可以返回仅 SQL_NULL_DATA，而长度缓冲区可以返回所有其他值。  
  
 有关详细信息，请参阅[SQLBulkOperations 函数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)， [SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)， [SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md)，和[使用长度/指示器值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md).  
  
 如果*StrLen_or_IndPtr*是使用 null 指针，没有长度或指示器值。 提取数据和数据为 NULL 时，这是一个错误。  
  
 请参阅[ODBC 64 位信息](../../../odbc/reference/odbc-64-bit-information.md)，如果你的应用程序将在 64 位操作系统上运行。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLBindCol**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLBindCol**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07006|受限制的数据类型属性冲突|(DM) *ColumnNumber*自变量为 0，和*TargetType*参数不为 SQL_C_BOOKMARK 或 SQL_C_VARBOOKMARK。|  
|07009|无效的描述符索引|为参数指定的值*ColumnNumber*超出最大结果集中的列数。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY003|应用程序缓冲区类型无效|自变量*TargetType*已既不有效的数据类型，也不 SQL_C_DEFAULT。|  
|HY010|函数序列错误|(DM) 为与关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLBindCol**调用。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*并返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 以异步方式执行的函数曾为*StatementHandle*和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 值的参数的指定*BufferLength*小于 0。<br /><br /> (DM) 驱动程序是 ODBC 2。*x*驱动程序， *ColumnNumber*参数已设置为 0，并为参数指定的值*BufferLength*未等于 4。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|驱动程序或数据源不支持指定的组合来转换*TargetType*自变量和相应的列的特定于驱动程序的 SQL 数据类型。<br /><br /> 自变量*ColumnNumber*是 0 和驱动程序不支持书签。<br /><br /> 驱动程序还支持仅 ODBC 2。*x*和自变量*TargetType*是以下之一：<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> 和中的任何间隔 C 数据类型列出[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)附录 d： 数据类型中。<br /><br /> 该驱动程序仅支持之前售价 3.50 和的自变量的 ODBC 版本*TargetType*已 SQL_C_GUID。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*StatementHandle*不支持该函数。|  
  
## <a name="comments"></a>注释  
 **SQLBindCol**用于将相关联，或*绑定，*结果中的列设置为数据缓冲区和应用程序中的长度/指示器缓冲区。 在应用程序调用**SQLFetch**， **SQLFetchScroll**，或**SQLSetPos**以提取数据，该驱动程序返回的数据绑定的列指定的缓冲区中; 对于详细信息，请参阅[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)。 在应用程序调用**SQLBulkOperations**若要更新或插入行或**SQLSetPos**若要更新的行，该驱动程序将检索的数据绑定中的列的指定缓冲区; 有关详细信息请参阅[SQLBulkOperations 函数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)或[SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md)。 有关绑定的详细信息，请参阅[检索结果 (Basic)](../../../odbc/reference/develop-app/retrieving-results-basic.md)。  
  
 请注意列不需要将绑定到从中检索数据。 应用程序还可以调用**SQLGetData**从列检索数据。 但也可以将绑定中的行和调用的某些列**SQLGetData**对于其他操作系统，这会受到某些限制。 有关详细信息，请参阅[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)。  
  
## <a name="binding-unbinding-and-rebinding-columns"></a>绑定、 正在取消绑定，和重新绑定列  
 可以绑定、 未绑定，或在任何时候，从结果集中提取数据的情况下，即使重新绑定列。 新绑定调用的函数，使用绑定的下一步时间生效。 例如，假设应用程序绑定中的列的结果集和调用**SQLFetch**。 在绑定的缓冲区，该驱动程序返回的数据。 现在，假设应用程序绑定到一组不同的缓冲区的列。 驱动程序不会将新绑定的缓冲区中的数据只提取行。 相反，它将等待，直至**SQLFetch**会再次调用，然后在新绑定的缓冲区的下一步的行的数据。  
  
> [!NOTE]  
>  语句属性 SQL_ATTR_USE_BOOKMARKS 应始终设置绑定列到列 0 之前。 这不是必需的但强烈建议。  
  
## <a name="binding-columns"></a>绑定列  
 若要绑定的列，应用程序调用**SQLBindCol**并将传递列号、 类型、 地址和长度的数据缓冲区和长度/指示器缓冲区的地址。 有关如何使用这些地址的信息，请参阅"缓冲区的地址，"本部分中更高版本。 有关绑定列的详细信息，请参阅[使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)。  
  
 将推迟，这些缓冲区的使用;即，应用程序将在绑定**SQLBindCol**但从其他函数的驱动程序访问它们-即**SQLBulkOperations**， **SQLFetch**， **SQLFetchScroll**，或**SQLSetPos**。 若要确保指针中指定的应用程序的负责**SQLBindCol**保持有效，只要绑定保持有效。 如果应用程序允许这些指针变为无效-例如，它会释放缓冲区，然后需要它们才能有效的函数的调用，将出现哪些后果是不确定。 有关详细信息，请参阅[延迟缓冲区](../../../odbc/reference/develop-app/deferred-buffers.md)。  
  
 绑定保持有效，直到它替换为新的绑定，该列为未绑定，或释放该语句。  
  
## <a name="unbinding-columns"></a>正在取消绑定列  
 要解除绑定的单个列，应用程序调用**SQLBindCol**与*ColumnNumber*设为该列数和*TargetValuePtr*设置为 null 指针。 如果*ColumnNumber*的未绑定列，是指**SQLBindCol**仍会返回 SQL_SUCCESS。  
  
 若要取消绑定所有列，应用程序调用**SQLFreeStmt**与*fOption*设置为 SQL_UNBIND。 这还可以通过将 ARD 为零的 SQL_DESC_COUNT 字段设置实现。  
  
## <a name="rebinding-columns"></a>重新绑定列  
 应用程序可以执行更改绑定的两个操作之一：  
  
-   调用**SQLBindCol**可指定已绑定的列的新绑定。 该驱动程序替换为新将覆盖旧的绑定。  
  
-   指定要添加到指定的绑定调用的缓冲区地址的偏移量**SQLBindCol**。 有关详细信息，请参阅下一部分中，"绑定偏移量。"  
  
## <a name="binding-offsets"></a>绑定偏移量  
 绑定偏移量是添加到的数据和长度/指示器缓冲区的地址值 (根据中的指定*TargetValuePtr*和*StrLen_or_IndPtr*自变量) 取消引用它们之前。 当使用偏移量时，绑定"模板"的应用程序的缓冲区布局方式，以及应用程序可以通过将移动此"模板"到不同区域的内存更改偏移量。 因为相同的偏移量添加到每个绑定中的每个地址，为不同的列在缓冲区之间的相对偏移量必须在每个集的缓冲区内相同。 在使用按行绑定; 时，这是始终 true应用程序必须仔细布局此项为 true，在使用专用于列的绑定时及其缓冲区。  
  
 使用绑定的偏移量基本上具有相同的效果重新列绑定通过调用**SQLBindCol**。 区别是，对的新调用**SQLBindCol**指定的数据缓冲区和长度/指示器缓冲区的新地址，而使用的绑定偏移量不会更改地址，但只需将偏移量添加到它们。 每当想，并且此偏移量始终添加到最初绑定地址，则应用程序可以指定新的偏移量。 具体而言，如果偏移量设置为 0 或语句特性设置为 null 指针，该驱动程序将使用最初绑定的地址。  
  
 若要指定绑定偏移量，应用程序 SQL_ATTR_ROW_BIND_OFFSET_PTR 语句将该属性设置 SQLINTEGER 缓冲区的地址。 应用程序调用一个函数，使用绑定之前，它会偏移量将以字节为单位，在此缓冲区中。 若要确定要使用的缓冲区的地址，该驱动程序将偏移量添加到绑定中的地址。 地址和偏移量之和必须是有效的地址，但不是需要是有效的偏移量添加到的地址。 有关如何使用绑定偏移量的详细信息，请参阅"缓冲区的地址，"本部分中更高版本。  
  
## <a name="binding-arrays"></a>绑定数组  
 如果大于 1 的行集大小 （SQL_ATTR_ROW_ARRAY_SIZE 语句属性的值），应用程序将绑定而不是单个缓冲区的缓冲区的数组。 有关详细信息，请参阅[块状游标](../../../odbc/reference/develop-app/block-cursors.md)。  
  
 应用程序可以将数组绑定两种方式：  
  
-   将数组绑定到每个列。 这称为*列绑定*因为每个数据结构 （数组） 包含单个列的数据。  
  
-   定义一个结构，用于保存数据时的整个行，并将绑定的这些结构数组。 这称为*按行绑定*因为每个数据结构包含单个行的数据。  
  
 每个缓冲区数组必须具有至少尽可能多的元素的行集的大小。  
  
> [!NOTE]  
>  应用程序必须验证对齐方式有效。 有关对齐注意事项的详细信息，请参阅[对齐](../../../odbc/reference/develop-app/alignment.md)。  
  
## <a name="column-wise-binding"></a>按列绑定  
 在列绑定中，应用程序将不同的数据和长度/指示器数组绑定到每个列。  
  
 若要使用专用于列的绑定，该应用程序首先 SQL_ATTR_ROW_BIND_TYPE 语句将该属性设置 SQL_BIND_BY_COLUMN。 （这是默认值）。对于每个绑定的列，应用程序执行以下步骤：  
  
1.  分配数据缓冲区数组。  
  
2.  分配一个数组的长度/指示器缓冲区。  
  
    > [!NOTE]  
    >  如果在使用专用于列的绑定时，应用程序将直接写入描述符，单独的数组可以用于长度和指标数据。  
  
3.  调用**SQLBindCol**使用以下参数：  
  
    -   *TargetType*是中的数据缓冲区数组的单个元素的类型。  
  
    -   *TargetValuePtr*是数据缓冲区数组的地址。  
  
    -   *BufferLength*是中的数据缓冲区数组的单个元素的大小。 *BufferLength*固定长度的数据的数据时，将忽略自变量。  
  
    -   *StrLen_or_IndPtr*是长度/指示器数组的地址。  
  
 有关如何使用此信息的详细信息，请参阅"缓冲区的地址，"本部分中更高版本。 有关列的绑定的详细信息，请参阅[按列绑定](../../../odbc/reference/develop-app/column-wise-binding.md)。  
  
## <a name="row-wise-binding"></a>按行绑定  
 在按行绑定中，应用程序定义包含的每一列绑定的数据和长度/指示器缓冲区的结构。  
  
 若要使用按行绑定，该应用程序，请执行以下步骤：  
  
1.  定义一个结构，用于保存数据 （包括数据和长度/指示器缓冲区） 的单个行，并分配这些结构的数组。  
  
    > [!NOTE]  
    >  如果在使用按行绑定时，应用程序将直接写入描述符，不同的字段，可以用于长度和指标数据。  
  
2.  到包含数据的单个行的结构的大小或实例的结果列将绑定到其中的缓冲区的大小，请设置 SQL_ATTR_ROW_BIND_TYPE 语句属性。 长度必须包括所有绑定的列和结构或缓冲区，以确保当绑定列的地址将递增，具有指定长度，结果将点到下一行中的同一列的开头的任何填充空间。 使用时*sizeof* ANSI C 中的运算符，此行为保证。  
  
3.  调用**SQLBindCol**与每个列绑定的以下参数：  
  
    -   *TargetType*是要绑定到列的数据缓冲区成员的类型。  
  
    -   *TargetValuePtr*是第一个数组元素中的数据缓冲区成员的地址。  
  
    -   *BufferLength*是数据缓冲区成员的大小。  
  
    -   *StrLen_or_IndPtr*是要绑定的长度/指示器成员的地址。  
  
 有关如何使用此信息的详细信息，请参阅"缓冲区的地址，"本部分中更高版本。 有关列的绑定的详细信息，请参阅[按行绑定](../../../odbc/reference/develop-app/row-wise-binding.md)。  
  
## <a name="buffer-addresses"></a>缓冲区地址  
 *缓冲地址*是数据或长度/指示器缓冲区的实际地址。 写入的缓冲区 （如期间提取时间） 之前，该驱动程序将计算的缓冲区地址。 从使用中指定的地址以下公式计算*TargetValuePtr*和*StrLen_or_IndPtr*自变量、 绑定偏移量和行号：  
  
 *绑定地址* + *绑定偏移量*+ ((*行号*– 1) x*元素大小*)  
  
 其中的公式变量定义下表中所述。  
  
|变量|Description|  
|--------------|-----------------|  
|*绑定地址*|数据缓冲区，使用指定的地址*TargetValuePtr*中的参数**SQLBindCol**。<br /><br /> 为长度/指示器缓冲区，使用指定的地址*StrLen_or_IndPtr*中的参数**SQLBindCol**。 有关详细信息，请参阅"描述符和 SQLBindCol"部分中的"附加注释"。<br /><br /> 如果绑定的地址为 0，不返回任何数据值，即使前面的公式来计算出的地址为非零值。|  
|*绑定偏移量*|如果使用按行绑定，则存储在地址的值指定具有 SQL_ATTR_ROW_BIND_OFFSET_PTR 语句属性。<br /><br /> 如果使用列绑定或 SQL_ATTR_ROW_BIND_OFFSET_PTR 语句属性的值是 null 指针，*绑定偏移量*为 0。|  
|*行号*|基于 1 的行集中的行数。 对于单行更行提取，这是默认安全设置，这是 1。|  
|*元素大小*|绑定的数组中元素的大小。<br /><br /> 如果使用列的绑定，这是**sizeof(SQLINTEGER)**长度/指示器缓冲区。 对于数据缓冲区，它是值*BufferLength*中的参数**SQLBindCol**如果数据类型是长度可变，并且数据类型的大小，如果数据类型为固定长度。<br /><br /> 如果使用按行绑定，这是数据和长度/指示器缓冲区 SQL_ATTR_ROW_BIND_TYPE 语句属性的值。|  
  
## <a name="descriptors-and-sqlbindcol"></a>说明符和 SQLBindCol  
 以下各节描述了如何**SQLBindCol**与描述符交互。  
  
> [!CAUTION]  
>  调用**SQLBindCol**为一条语句可能会影响其他语句。 当与语句关联 ARD 显式分配且又与其他语句相关联，将发生这种情况。 因为**SQLBindCol**修改描述符，修改将应用于此说明符与之关联的所有语句。 如果这不是所需的行为，应用程序应取消关联此描述符从其他语句之前它将调用**SQLBindCol**。  
  
## <a name="argument-mappings"></a>自变量映射  
 从概念上讲， **SQLBindCol**序列中执行以下步骤：  
  
1.  调用**SQLGetStmtAttr**以获得 ARD 句柄。  
  
2.  调用**SQLGetDescField**若要获取此描述符 SQL_DESC_COUNT 字段，并且如果中的值*ColumnNumber*参数超过 SQL_DESC_COUNT，调用的值**SQLSetDescField**增加到 SQL_DESC_COUNT 值*ColumnNumber*。  
  
3.  调用**SQLSetDescField**多次将值分配到 ARD 以下字段：  
  
    -   SQL_DESC_TYPE 和 SQL_DESC_CONCISE_TYPE 设置的值为*TargetType*，只不过如果*TargetType*是日期时间或间隔的子类型的简洁标识符，它将 SQL_DESC_TYPE 设置为 SQL_DATETIME 或 SQL_INTERVAL，分别;为简洁的标识符; 设置 SQL_DESC_CONCISE_TYPE并将设置 SQL_DESC_DATETIME_INTERVAL_CODE 到相应的日期时间或间隔子代码。  
  
    -   将一个或多个 SQL_DESC_LENGTH、 SQL_DESC_PRECISION、 SQL_DESC_SCALE 和 SQL_DESC_DATETIME_INTERVAL_PRECISION，设置为适合*TargetType*。  
  
    -   将 SQL_DESC_OCTET_LENGTH 字段设置为的值*BufferLength*。  
  
    -   将 SQL_DESC_DATA_PTR 字段设置为的值*TargetValue*。  
  
    -   将 SQL_DESC_INDICATOR_PTR 字段设置为的值*StrLen_or_Ind*。 （请参阅以下段落。）  
  
    -   将 SQL_DESC_OCTET_LENGTH_PTR 字段设置为的值*StrLen_or_Ind*。 （请参阅以下段落。）  
  
 变量的*StrLen_or_Ind*自变量是指用于指示器和长度的信息。 如果提取遇到 null 值的列，它将 SQL_NULL_DATA 存储在此变量，例如：否则，它将此变量中存储的数据长度。 将 null 作为指针传递*StrLen_or_Ind*会保持提取操作返回的数据长度，但使失败如果它遇到 null 值，并且无法返回 SQL_NULL_DATA 提取。  
  
 如果调用**SQLBindCol**失败，它将设置在 ARD 描述符字段的内容是不确定和 ARD SQL_DESC_COUNT 字段的值保持不变。  
  
## <a name="implicit-resetting-of-count-field"></a>隐式重置计数字段  
 **SQLBindCol**设置的值的 SQL_DESC_COUNT *ColumnNumber*参数仅当这会增加 SQL_DESC_COUNT 的值。 如果中的值*TargetValuePtr*参数是空指针，并且中的值*ColumnNumber*参数是否等于 SQL_DESC_COUNT （即，当取消绑定最高绑定列），然后 SQL_DESC_计数设置为最大剩余绑定的列数。  
  
## <a name="cautions-regarding-sqldefault"></a>有关 SQL_DEFAULT 的注意事项  
 若要成功检索列数据，应用程序必须确定正确的长度和应用程序缓冲区中的数据的起始点。 当应用程序将指定的显式*TargetType*，应用程序错误理解容易被检测出。 但是，当应用程序指定*TargetType*的 SQL_DEFAULT， **SQLBindCol**可以应用于不同的数据类型的列从一个预期应用程序，从更改元数据或通过将代码应用于不同的列。 在这种情况下，应用程序可能不总是可以确定的开始或读取的列数据的长度。 这可能导致数据未报告的错误或内存冲突。  
  
## <a name="code-example"></a>代码示例  
 在以下示例中，应用程序执行**选择**语句 Customers 表以返回结果集的客户 Id、 名称和电话号码，按名称排序。 然后，它调用**SQLBindCol**要绑定到的本地缓冲区的数据的列。 最后，应用程序，则提取的数据与每个行**SQLFetch** ，并输出每个客户的名称、 ID 和电话号码。  
  
 有关更多的代码示例，请参阅[SQLBulkOperations 函数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)， [SQLColumns 函数](../../../odbc/reference/syntax/sqlcolumns-function.md)， [SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)，和[SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```  
// SQLBindCol_ref.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <stdio.h>  
  
#define UNICODE  
#include <sqlext.h>  
  
#define NAME_LEN 50  
#define PHONE_LEN 20  
  
void show_error() {  
   printf("error\n");  
}  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt = 0;  
   SQLRETURN retcode;  
   SQLWCHAR szName[NAME_LEN], szPhone[PHONE_LEN], sCustID[NAME_LEN];  
   SQLLEN cbName = 0, cbCustID = 0, cbPhone = 0;  
  
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            // Connect to data source  
            retcode = SQLConnect(hdbc, (SQLWCHAR*) L"NorthWind", SQL_NTS, (SQLWCHAR*) NULL, 0, NULL, 0);  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {   
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               retcode = SQLExecDirect(hstmt, (SQLWCHAR *) L"SELECT CustomerID, ContactName, Phone FROM CUSTOMERS ORDER BY 2, 1, 3", SQL_NTS);  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
                  // Bind columns 1, 2, and 3  
                  retcode = SQLBindCol(hstmt, 1, SQL_C_CHAR, &sCustID, 100, &cbCustID);  
                  retcode = SQLBindCol(hstmt, 2, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
                  retcode = SQLBindCol(hstmt, 3, SQL_C_CHAR, szPhone, PHONE_LEN, &cbPhone);   
  
                  // Fetch and print each row of data. On an error, display a message and exit.  
                  for (i ; ; i++) {  
                     retcode = SQLFetch(hstmt);  
                     if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO)  
                        show_error();  
                     if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
                        wprintf(L"%d: %S %S %S\n", i + 1, sCustID, szName, szPhone);  
                     else  
                        break;  
                  }  
               }  
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLCancel(hstmt);  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}  
```  
  
 另请参阅[示例 ODBC 程序](../../../odbc/reference/sample-odbc-program.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|在结果集中返回的列的相关信息|[SQLDescribeCol 函数](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|提取的数据块，或通过结果滚动设置|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|提取数据的多个的行|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|释放的语句上的列缓冲区|[SQLFreeStmt 函数](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|提取部分或全部数据列|[SQLGetData 函数](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|返回的结果数设置列|[SQLNumResultCols 函数](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
