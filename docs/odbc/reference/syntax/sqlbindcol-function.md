---
title: SQLBindCol 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3860243580981d995e6581d883e12afe3f033d3b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036217"
---
# <a name="sqlbindcol-function"></a>SQLBindCol 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：ISO 92  
  
 **摘要**  
 **SQLBindCol**将应用程序数据缓冲区绑定到结果集中的列。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
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
 [输入]要绑定的列集的结果数。 列中从 0 开始，其中第 0 列书签列的列顺序递增编号。 如果不使用书签-也就是说，SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_OFF-然后列号从 1 开始。  
  
 *TargetType*  
 [输入]C 数据类型的标识符\* *TargetValuePtr*缓冲区。 当它从数据源检索数据**SQLFetch**， **SQLFetchScroll**， **SQLBulkOperations**，或者**SQLSetPos**、驱动程序将数据转换为此类型;当其将数据发送到数据源**SQLBulkOperations**或**SQLSetPos**，驱动程序将数据从这种类型转换。 有关有效的 C 数据类型和类型标识符的列表，请参阅[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)附录 d： 中的部分数据类型。  
  
 如果*TargetType*参数中的 SQL_DESC_DATETIME_INTERVAL_PRECISION 和 SQL_DESC_PRECISION 字段设置为间隔数据类型，默认时间间隔的前导精度 (2) 和默认时间间隔的秒精度 (6)，ARD，分别用于数据。 如果*TargetType*参数是 SQL_C_NUMERIC，默认的精度 （驱动程序定义） 和 ARD 的 SQL_DESC_PRECISION 和 SQL_DESC_SCALE 字段中设置默认小数位数 (0)，用于数据。 如果任何默认精度或小数位数不适当，应用程序显式应通过调用设置适当的描述符字段**SQLSetDescField**或**SQLSetDescRec**。  
  
 此外可以指定扩展的 C 数据类型。 有关详细信息，请参阅[ODBC 中的 C 数据类型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
 *TargetValuePtr*  
 延迟的输入/输出指向要绑定到的列的数据缓冲区的指针。 **SQLFetch**并**SQLFetchScroll**在此缓冲区中返回数据。 **SQLBulkOperations**在此返回数据缓冲区时*操作*是 SQL_FETCH_BY_BOOKMARK; 它检索的数据从该缓冲区时*操作*SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK。 **SQLSetPos**在此返回数据缓冲区时*操作*是 SQL_REFRESH; 它检索的数据从该缓冲区时*操作*是 SQL_UPDATE。  
  
 如果*TargetValuePtr*是 null 指针，该驱动程序取消绑定列的数据缓冲区。 应用程序可以通过调用取消绑定所有列**SQLFreeStmt**使用 SQL_UNBIND 选项。 应用程序可以取消绑定列的数据缓冲区，但如果仍有长度/指示器缓冲区列中，发往*TargetValuePtr*调用中的参数**SQLBindCol**是 null 指针，但*StrLen_or_IndPtr*参数是有效的值。  
  
 *BufferLength*  
 [输入]长度 **TargetValuePtr*以字节为单位的缓冲区。  
  
 驱动程序使用*BufferLength*以免超出末尾的编写\* *TargetValuePtr*缓冲时它将返回长度可变的数据，如字符或二进制数据。 请注意，该驱动程序，它返回字符数据时都计的 null 终止字符\* *TargetValuePtr*。 **TargetValuePtr*因此必须包含空间的 null 终止字符或驱动程序将截断数据。  
  
 当驱动程序返回固定长度的数据，如整数或日期结构时，驱动程序会忽略*BufferLength*并假定缓冲区足够大以保存数据。 因此，务必要为固定长度的数据分配缓冲区足够大的应用程序或驱动程序将写入缓冲区的结束。  
  
 **SQLBindCol**返回 SQLSTATE HY090 （字符串或缓冲区长度无效） 时*BufferLength*是小于 0，但不是在时*BufferLength*为 0。 但是，如果*TargetType*指定字符的类型，不应设置应用程序*BufferLength*为 0，因为符合 ISO CLI 的驱动程序返回 SQLSTATE HY090 （字符串或缓冲区长度无效），用例。  
  
 *StrLen_or_IndPtr*  
 延迟的输入/输出要绑定到的列的长度/指示器缓冲区的指针。 **SQLFetch**并**SQLFetchScroll**此缓冲区中返回值。 **SQLBulkOperations**检索一个值，从该缓冲区何时*操作*是 SQL_ADD、 SQL_UPDATE_BY_BOOKMARK，还是 SQL_DELETE_BY_BOOKMARK。 **SQLBulkOperations**返回一个值，在此缓冲区何时*操作*是 SQL_FETCH_BY_BOOKMARK。 **SQLSetPos**返回一个值，在此缓冲区何时*操作*是 SQL_REFRESH; 它检索一个值，从该缓冲区时*操作*是 SQL_UPDATE。  
  
 **SQLFetch**， **SQLFetchScroll**， **SQLBulkOperations**，并且**SQLSetPos**可以返回的长度/指示器缓冲区中的以下值：  
  
-   可用于返回的数据的长度  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 应用程序可以将以下值放在与一起使用的长度/指示器缓冲区**SQLBulkOperations**或**SQLSetPos**:  
  
-   正在发送的数据的长度  
  
-   SQL_NTS  
  
-   SQL_NULL_DATA  
  
-   SQL_DATA_AT_EXEC  
  
-   SQL_LEN_DATA_AT_EXEC 宏的结果  
  
-   SQL_COLUMN_IGNORE  
  
 如果指示器缓冲区和长度的缓冲区是单独的缓冲区，指示器缓冲区可返回仅 SQL_NULL_DATA，而长度缓冲区可以返回所有其他值。  
  
 有关详细信息，请参阅[SQLBulkOperations 函数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)， [SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)， [SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md)，和[使用长度/指示器值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md).  
  
 如果*StrLen_or_IndPtr*是使用空指针、 没有长度或指示器值。 当提取数据和数据为 NULL 时，这是一个错误。  
  
 请参阅[ODBC 64-Bit 信息](../../../odbc/reference/odbc-64-bit-information.md)，如果你的应用程序将在 64 位操作系统上运行。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLBindCol**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用来获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和一个*处理*的*StatementHandle*。 下表列出了通常由返回的 SQLSTATE 值**SQLBindCol** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|Error|描述|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07006|受限制的数据类型属性冲突|（数据挖掘） *ColumnNumber*参数为 0，并且*TargetType* SQL_C_BOOKMARK 或 SQL_C_VARBOOKMARK 参数不是。|  
|07009|描述符索引无效|为参数指定的值*ColumnNumber*超出最大结果集中的列数。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY003|无效的应用程序缓冲区类型|自变量*TargetType*是有效的数据类型既不 SQL_C_DEFAULT。|  
|HY010|函数序列错误|(DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLBindCol**调用。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*和返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 的调用以异步方式执行的函数*StatementHandle*和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**曾为*StatementHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 的参数指定的值*BufferLength*小于 0。<br /><br /> (DM) 驱动程序是 ODBC 2。*x*驱动程序， *ColumnNumber*参数设置为 0，并为该参数指定的值*BufferLength*不是等于 4。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|驱动程序或数据源不支持指定的组合来转换*TargetType*参数和特定于驱动程序的 SQL 数据类型的相应列。<br /><br /> 自变量*ColumnNumber*为 0 时，该驱动程序不支持书签。<br /><br /> 该驱动程序支持仅 ODBC 2。*x*和参数*TargetType*是以下之一：<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> 和中列出的 C 间隔数据类型的任何[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)中附录 d:数据类型。<br /><br /> 该驱动程序仅支持之前需 3.50 和参数的 ODBC 版本*TargetType*已 SQL_C_GUID。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*StatementHandle*不支持该函数。|  
  
## <a name="comments"></a>注释  
 **SQLBindCol**用于将相关联，或*绑定，* 结果中的列设置为数据缓冲区和应用程序中的长度/指示器缓冲区。 当应用程序调用**SQLFetch**， **SQLFetchScroll**，或**SQLSetPos**来提取数据，该驱动程序返回的数据绑定的列指定缓冲区中; 对于详细信息，请参阅[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)。 当应用程序调用**SQLBulkOperations**若要更新或插入行或**SQLSetPos**更新的行，该驱动程序中检索数据对于绑定列指定的缓冲区中; 有关详细信息请参阅[SQLBulkOperations 函数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)或[SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md)。 有关绑定的详细信息，请参阅[检索结果 （基本）](../../../odbc/reference/develop-app/retrieving-results-basic.md)。  
  
 请注意，列不需要将绑定到从其检索数据。 应用程序还可以调用**SQLGetData**来从列中检索数据。 尽管可以将绑定中的行和调用的某些列，但**SQLGetData**对于其他操作系统，这会受到某些限制。 有关详细信息，请参阅[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)。  
  
## <a name="binding-unbinding-and-rebinding-columns"></a>绑定、 取消绑定操作，和重新绑定列  
 列可以绑定、 未绑定，或在任何时候，从结果集中提取数据，即使重新绑定。 新绑定使用的绑定的函数调用的下一步时间生效。 例如，假设应用程序绑定中的列的结果集和调用**SQLFetch**。 该驱动程序绑定的缓冲区中返回的数据。 现在假设应用程序绑定到一组不同的缓冲区的列。 该驱动程序不会在新绑定的缓冲区中将只是提取行的数据。 相反，它将等待，直至**SQLFetch**再次调用，然后在新绑定的缓冲区的下一步的行的数据。  
  
> [!NOTE]  
>  语句属性 SQL_ATTR_USE_BOOKMARKS 应始终设置绑定到列 0 之前。 这不是必需的但强烈建议。  
  
## <a name="binding-columns"></a>绑定列  
 若要将列绑定，应用程序调用**SQLBindCol** ，并将传递列号、 类型、 地址和长度的数据缓冲区和长度/指示器缓冲区的地址。 有关如何使用这些地址的信息，请参阅"缓冲区的地址，"更高版本在本部分中。 有关绑定列的详细信息，请参阅[使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)。  
  
 使用这些缓冲区被延迟;也就是说，应用程序将绑定中对其**SQLBindCol**但该驱动程序访问它们中的其他函数-即**SQLBulkOperations**， **SQLFetch**， **SQLFetchScroll**，或**SQLSetPos**。 它是应用程序的责任，以确保在指定指针**SQLBindCol**保持有效，前提是该绑定将保持有效。 如果该应用程序允许这些指针变为无效-例如，它将释放缓冲区-，然后调用预计这些无效的函数，结果不确定。 有关详细信息，请参阅[延迟的缓冲区](../../../odbc/reference/develop-app/deferred-buffers.md)。  
  
 绑定保持有效，直到它替换为新的绑定，该列为未绑定，或释放该语句。  
  
## <a name="unbinding-columns"></a>正在取消绑定列  
 若要取消绑定的单个列，应用程序调用**SQLBindCol**与*ColumnNumber*设置为的列数和*TargetValuePtr*设置为 null 指针。 如果*ColumnNumber*未绑定的列，是指**SQLBindCol**仍将返回 SQL_SUCCESS。  
  
 若要取消绑定所有列，应用程序调用**SQLFreeStmt**与*fOption*设置为 SQL_UNBIND。 这还会通过设置为零 ARD SQL_DESC_COUNT 字段来完成。  
  
## <a name="rebinding-columns"></a>重新绑定列  
 应用程序可以执行两项操作才能更改绑定之一：  
  
-   调用**SQLBindCol**以指定新的绑定已绑定的列。 该驱动程序将使用新覆盖旧的绑定。  
  
-   指定要添加到绑定调用中所指定的缓冲区地址的偏移量**SQLBindCol**。 有关详细信息，请参阅下一部分中，"绑定偏移量。"  
  
## <a name="binding-offsets"></a>绑定的偏移量  
 绑定偏移量是一个值，添加到的数据和长度/指示器缓冲区的地址 (中指定的那样*TargetValuePtr*并*StrLen_or_IndPtr*参数) 它们取消引用之前。 当使用偏移量时，绑定是一个"模板"的应用程序的缓冲区的布局方式，并在应用程序可以移动此"模板"到不同区域的内存更改偏移量。 由于相同的偏移量添加到每个绑定中的每个地址，为不同的列在缓冲区之间的相对偏移量必须是相同的缓冲区每组中。 在使用按行绑定; 时，这是始终，则返回 true应用程序必须仔细设置此属性为 true 时使用按列绑定其缓冲区布局。  
  
 使用绑定的偏移量基本上具有相同的效果重新绑定列，通过调用**SQLBindCol**。 不同之处在于新调用**SQLBindCol**指定的数据缓冲区和长度/指示器缓冲区的新地址，而使用绑定偏移量不会更改地址，但只需向其添加偏移量。 只要想，并且此偏移量始终添加到最初绑定地址，该应用程序可以指定新的偏移量。 具体而言，如果偏移量设置为 0 或语句属性设置为 null 指针，该驱动程序将使用最初绑定的地址。  
  
 若要指定绑定偏移量，该应用程序设置为 SQLINTEGER 缓冲区的地址的 SQL_ATTR_ROW_BIND_OFFSET_PTR 语句属性。 应用程序调用一个函数，使用绑定之前，它会在此缓冲区中的字节将偏移量。 若要确定要使用的缓冲区的地址，驱动程序会添加到绑定中的地址偏移量。 地址和偏移量的总和必须为有效的地址，但不是需要是有效的偏移量添加到的地址。 有关如何使用绑定的偏移量的详细信息，请参阅"缓冲区的地址，"更高版本在本部分中。  
  
## <a name="binding-arrays"></a>绑定数组  
 如果大于 1 的行集大小 （SQL_ATTR_ROW_ARRAY_SIZE 语句属性的值），该应用程序将绑定的而不是单个缓冲区的缓冲区的数组。 有关详细信息，请参阅[块状游标](../../../odbc/reference/develop-app/block-cursors.md)。  
  
 应用程序可以将数组绑定通过两种方式：  
  
-   将数组绑定到每个列。 这被称为*按列绑定*因为每个数据结构 （数组） 包含对单个列的数据。  
  
-   定义一种结构来保存整个行的数据，并将绑定这些结构的数组。 这被称为*按行绑定*因为每个数据结构包含单个行的数据。  
  
 每个缓冲区数组作为行集的大小必须至少多少元素。  
  
> [!NOTE]  
>  应用程序必须验证对齐方式有效。 有关对齐方式的详细信息，请参阅[对齐](../../../odbc/reference/develop-app/alignment.md)。  
  
## <a name="column-wise-binding"></a>按列绑定  
 在按列绑定中，应用程序将单独的数据和长度/指示器数组绑定到每个列。  
  
 若要使用按列绑定，应用程序首先将 SQL_ATTR_ROW_BIND_TYPE 语句属性设置为 SQL_BIND_BY_COLUMN。 （这是默认值）。对于要绑定每个列，该应用程序执行以下步骤：  
  
1.  分配数据缓冲区数组。  
  
2.  分配长度/指示器缓冲区的数组。  
  
    > [!NOTE]  
    >  如果在使用按列绑定时，应用程序将直接写入描述符，独立的数组可以用于长度和指示器数据。  
  
3.  调用**SQLBindCol**使用以下参数：  
  
    -   *TargetType*是数据缓冲区数组中的单个元素的类型。  
  
    -   *TargetValuePtr*是数据缓冲区数组的地址。  
  
    -   *BufferLength*是数据缓冲区数组中的单个元素的大小。 *BufferLength*固定长度的数据的数据时，将忽略参数。  
  
    -   *StrLen_or_IndPtr*是长度/指示器数组的地址。  
  
 有关如何使用此信息的详细信息，请参阅"缓冲区的地址，"更高版本在本部分中。 按列绑定的详细信息，请参阅[按列绑定](../../../odbc/reference/develop-app/column-wise-binding.md)。  
  
## <a name="row-wise-binding"></a>按行绑定  
 在按行绑定中，应用程序定义的结构，包含要绑定每个列的数据和长度/指示器缓冲区。  
  
 若要使用按行绑定，应用程序，请执行以下步骤：  
  
1.  定义一个结构以容纳单个行的数据 （包括数据和长度/指示器缓冲区），并分配这些结构的数组。  
  
    > [!NOTE]  
    >  如果在使用按行绑定时，应用程序将直接写入描述符，单独的字段可用于长度和指示器数据。  
  
2.  包含单个数据行的结构的大小或实例的结果列将绑定到其中的缓冲区大小设置 SQL_ATTR_ROW_BIND_TYPE 语句属性。 长度必须包括所有绑定的列，以及结构或缓冲区，以确保当绑定列的地址与指定的长度递增时，结果将点到下一行中的同一列开头的任何填充大小的空间。 使用时*sizeof* ANSI C 中的运算符，将保证该行为。  
  
3.  调用**SQLBindCol**与要绑定每个列的以下参数：  
  
    -   *TargetType*是要绑定到列的数据缓冲区成员的类型。  
  
    -   *TargetValuePtr*是第一个数组元素中的数据缓冲区成员的地址。  
  
    -   *BufferLength*是数据缓冲区成员的大小。  
  
    -   *StrLen_or_IndPtr*是要绑定的长度/指示器成员的地址。  
  
 有关如何使用此信息的详细信息，请参阅"缓冲区的地址，"更高版本在本部分中。 按列绑定的详细信息，请参阅[按行绑定](../../../odbc/reference/develop-app/row-wise-binding.md)。  
  
## <a name="buffer-addresses"></a>缓冲区地址  
 *缓冲区地址*是数据或长度/指示器缓冲区的实际地址。 它将写入到缓冲区 （如期间提取时间） 之前，驱动程序计算的缓冲区地址。 从下面的公式，使用中指定的地址计算*TargetValuePtr*并*StrLen_or_IndPtr*自变量、 绑定偏移量和行号：  
  
 *绑定地址* + *绑定偏移量*+ ((*行号*-1) x*元素大小*)  
  
 其中公式的变量定义如下表中所述。  
  
|变量|描述|  
|--------------|-----------------|  
|*绑定地址*|数据缓冲区，使用指定的地址*TargetValuePtr*中的参数**SQLBindCol**。<br /><br /> 长度/指示器缓冲区，使用指定的地址*StrLen_or_IndPtr*中的参数**SQLBindCol**。 有关详细信息，请参阅"描述符和 SQLBindCol"部分中的"附加注释"。<br /><br /> 如果绑定的地址为 0，不返回任何数据值，即使上面的公式计算得出的地址为非零值。|  
|*绑定偏移量*|如果使用按行绑定，则使用 SQL_ATTR_ROW_BIND_OFFSET_PTR 语句属性将指定的地址上存储的值。<br /><br /> 如果使用按列绑定或 SQL_ATTR_ROW_BIND_OFFSET_PTR 语句属性的值为 null 指针，*绑定的偏移量*为 0。|  
|*行号*|从 1 开始的行集中的行数。 对于单行提取操作，这是默认值，这是 1。|  
|*元素大小*|绑定的数组中的元素的大小。<br /><br /> 如果使用按列绑定，则这是**sizeof(SQLINTEGER)** 的长度/指示器缓冲区。 它是值的数据缓冲区*BufferLength*中的参数**SQLBindCol**如果数据类型是可变长度和数据类型的大小的数据类型固定长度。<br /><br /> 如果使用按行绑定，则这是数据和长度/指示器缓冲区将 SQL_ATTR_ROW_BIND_TYPE 语句属性的值。|  
  
## <a name="descriptors-and-sqlbindcol"></a>描述符和 SQLBindCol  
 以下各节介绍如何**SQLBindCol**与描述符进行交互。  
  
> [!CAUTION]  
>  调用**SQLBindCol**为一条语句可能会影响其他语句。 当与语句相关联 ARD 显式分配，并且仍与其他语句相关联时，将发生这种情况。 因为**SQLBindCol**修改描述符，所做的修改将应用于此说明符与之关联的所有语句。 如果这不是所需的行为，应用程序应取消关联此描述符的其他语句之前它将调用**SQLBindCol**。  
  
## <a name="argument-mappings"></a>参数映射  
 从概念上讲， **SQLBindCol**序列中执行以下步骤：  
  
1.  调用**SQLGetStmtAttr**以获得 ARD 句柄。  
  
2.  调用**SQLGetDescField**若要获取此描述符 SQL_DESC_COUNT 字段中，并且如果中的值*ColumnNumber*自变量超出 SQL_DESC_COUNT，调用的值**SQLSetDescField** SQL_DESC_COUNT 到值增加*ColumnNumber*。  
  
3.  调用**SQLSetDescField**多次将值分配到 ARD 的以下字段：  
  
    -   设置的值的 SQL_DESC_TYPE 和 SQL_DESC_CONCISE_TYPE *TargetType*，只不过如果*TargetType*是一个 datetime 或间隔子类型的简洁标识符，它将 SQL_DESC_TYPE 设置为 SQL_日期时间或 SQL_INTERVAL，分别;设置 SQL_DESC_CONCISE_TYPE 为简明的标识符;和集 SQL_DESC_DATETIME_INTERVAL_CODE 到相应的日期时间或间隔子代码。  
  
    -   将一个或多个 SQL_DESC_LENGTH、 SQL_DESC_PRECISION、 SQL_DESC_SCALE 和 SQL_DESC_DATETIME_INTERVAL_PRECISION，设置为适合*TargetType*。  
  
    -   设置的值的 SQL_DESC_OCTET_LENGTH 字段*BufferLength*。  
  
    -   设置 SQL_DESC_DATA_PTR 字段的值*TargetValue*。  
  
    -   SQL_DESC_INDICATOR_PTR 字段设置为值*StrLen_or_Ind*。 （请参阅下面的段落中。）  
  
    -   SQL_DESC_OCTET_LENGTH_PTR 字段设置为值*StrLen_or_Ind*。 （请参阅下面的段落中。）  
  
 该变量的*StrLen_or_Ind*参数是指用于指示符和长度的信息。 如果提取遇到 null 值的列，它将 SQL_NULL_DATA 存储在此变量，例如：否则，它将在此变量中存储的数据长度。 传递 null 指针视为*StrLen_or_Ind*保持从返回的数据长度的提取操作但会提取失败，如果它遇到 null 值而无法返回 SQL_NULL_DATA。  
  
 如果在调用**SQLBindCol**失败，该值将设置在 ARD 的描述符字段的内容是不确定和 ARD SQL_DESC_COUNT 字段的值保持不变。  
  
## <a name="implicit-resetting-of-count-field"></a>隐式重置计数字段  
 **SQLBindCol**设置的值 SQL_DESC_COUNT *ColumnNumber*参数仅当这会增加 SQL_DESC_COUNT 的值。 如果中的值*TargetValuePtr*参数是空指针，并且中的值*ColumnNumber*参数等于 SQL_DESC_COUNT （即，当取消绑定的最高绑定列），然后 SQL_DESC_计数设置为最高的其余绑定列数。  
  
## <a name="cautions-regarding-sqldefault"></a>有关 SQL_DEFAULT 的注意事项  
 若要成功检索列数据，应用程序必须确定正确的长度和应用程序缓冲区中的数据的起始点。 当应用程序指定了显式*TargetType*，轻松地检测到应用程序误解。 但是，当应用程序指定了*TargetType* SQL_DEFAULT 的**SQLBindCol**可应用于不同的数据类型的列从一个目标应用程序，从对更改元数据或通过将代码应用于不同的列。 在这种情况下，应用程序可能不总是确定的开始或提取的列数据的长度。 这可能会导致数据未报告的错误或内存冲突。  
  
## <a name="code-example"></a>代码示例  
 在以下示例中，应用程序执行**选择**来返回结果集的客户 Id、 名称和电话号码的 Customers 表的语句按名称排序。 然后，它调用**SQLBindCol**要绑定到的本地缓冲区的数据的列。 最后，应用程序读取的数据与每一行**SQLFetch**并输出每个客户的名称、 ID 和电话号码。  
  
 有关更多的代码示例，请参阅[SQLBulkOperations 函数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)， [SQLColumns 函数](../../../odbc/reference/syntax/sqlcolumns-function.md)， [SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)，和[SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```cpp  
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
|在结果集中返回列的相关信息|[SQLDescribeCol 函数](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|提取的数据块或滚动浏览结果集|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|正在提取多行数据|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|释放语句列缓冲区|[SQLFreeStmt 函数](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|正在提取部分或全部的数据列|[SQLGetData 函数](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|返回数的结果集列|[SQLNumResultCols 函数](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
