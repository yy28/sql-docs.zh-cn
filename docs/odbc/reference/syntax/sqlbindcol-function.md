---
title: SQLBindCol 功能 |微软文档
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
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBindCol
helpviewer_keywords:
- SQLBindCol function [ODBC]
ms.assetid: 41a37655-84cd-423f-9daa-e0b47b88dc54
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 90bb1c1aa4dbfa2614f689faa47eb0c41a6cecd6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298737"
---
# <a name="sqlbindcol-function"></a>SQLBindCol 函数
**一致性**  
 推出版本： ODBC 1.0 标准合规性： ISO 92  
  
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
 *语句句柄*  
 [输入]语句句柄。  
  
 ColumnNumber   
 [输入]要绑定的结果集列的编号。 列按增加列顺序编号，从 0 开始，其中列 0 是书签列。 如果未使用书签（即SQL_ATTR_USE_BOOKMARKS语句属性设置为SQL_UB_OFF，则列编号从 1 开始。  
  
 *目标类型*  
 [输入]\**目标ValuePtr*缓冲区的 C 数据类型的标识符。 当它使用**SQLFetch、SQLFetchScroll、SQLBulk****操作**或**SQLSetPos**从数据源检索数据时，驱动程序会将数据转换为此类型; **SQLFetch**当它使用**SQLBulk 操作**或**SQLSetPos**将数据发送到数据源时，驱动程序将转换此类型的数据。 有关有效的 C 数据类型和类型标识符的列表，请参阅附录 D：数据类型中的[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)部分。  
  
 如果*TargetType*参数是间隔数据类型，则分别用于数据中的 SQL_DESC_DATETIME_INTERVAL_PRECISION 和 SQL_DESC_PRECISION 字段中设置的默认间隔前导精度 （2） 和默认间隔秒精度 （6）。 如果*TargetType*参数SQL_C_NUMERIC，则数据将使用在 ARD 的SQL_DESC_PRECISION和SQL_DESC_SCALE字段中设置的默认精度（驱动程序定义）和默认比例 （0）。 如果任何默认精度或比例不合适，应用程序应通过调用**SQLSetDescField**或**SQLSetDescRec**显式设置相应的描述符字段。  
  
 您还可以指定扩展的 C 数据类型。 有关详细信息，请参阅[ODBC 中的 C 数据类型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
 *目标价值Ptr*  
 [延迟输入/输出]指向要绑定到列的数据缓冲区。 **SQLFetch**和**SQLFetchScroll**返回此缓冲区中的数据。 当*操作*SQL_FETCH_BY_BOOKMARK时 **，SQLBulk 操作**返回此缓冲区中的数据;当*操作*SQL_ADD或SQL_UPDATE_BY_BOOKMARK时，它会从该缓冲区检索数据。 当*操作*SQL_REFRESH时 **，SQLSetPos**返回此缓冲区中的数据;当*操作*SQL_UPDATE时，它将从该缓冲区检索数据。  
  
 如果*TargetValuePtr*是空指针，则驱动程序将取消绑定列的数据缓冲区。 应用程序可以通过使用SQL_UNBIND选项调用**SQLFreeStmt**取消绑定所有列。 如果调用**SQLBindCol**中的*TargetValuePtr*参数是空指针，但*StrLen_or_IndPtr*参数是有效的值，则应用程序可以取消绑定列的数据缓冲区，但仍为列绑定长度/指示器缓冲区。  
  
 *缓冲区长度*  
 [输入]以字节为单位\**的目标价值Ptr*缓冲区的长度。  
  
 当驱动程序返回可变长度数据（如字符或二进制数据）时，驱动程序使用*BufferLength*来避免写入\**TargetValuePtr*缓冲区的末尾。 请注意，当驱动程序将字符数据\*返回到*TargetValuePtr*时，驱动程序会计算 null 终止字符。 \*因此 *，TargetValuePtr*必须包含 null 终止字符的空间，否则驱动程序将截截数据。  
  
 当驱动程序返回固定长度数据（如整数或日期结构）时，驱动程序将忽略*BufferLength*并假定缓冲区足够大以容纳数据。 因此，应用程序为固定长度数据分配足够大的缓冲区非常重要，否则驱动程序将写入缓冲区的末尾。  
  
 当*缓冲区长度*小于 0，但当缓冲区长度为 0 时 **，SQLBindCol**返回 SQLSTATE HY090（无效字符串或缓冲区长度），但当*缓冲区长度*为 0 时，则返回 SQLSTATE HY090（无效字符串或缓冲区长度）。 但是，如果*TargetType*指定字符类型，则应用程序不应将*BufferLength*设置为 0，因为符合 ISO CLI 的驱动程序在这种情况下返回 SQLSTATE HY090（无效字符串或缓冲区长度）。  
  
 *StrLen_or_IndPtr*  
 [延迟输入/输出]指向长度/指示器缓冲区以绑定到列。 **SQLFetch**和**SQLFetchScroll**返回此缓冲区中的值。 当操作SQL_ADD、SQL_UPDATE_BY_BOOKMARK或SQL_DELETE_BY_BOOKMARK*操作*时 **，SQLBulk操作**从该缓冲区检索值。 **sqlBulk 操作**在操作*SQL_FETCH_BY_BOOKMARK时返回*此缓冲区中的值。 当*操作*SQL_REFRESH时 **，SQLSetPos**将返回此缓冲区中的值;当*操作*SQL_UPDATE时，它将从该缓冲区检索值。  
  
 **SQLFetch、SQLFetchScroll、SQLBulk****操作**和**SQLSetPos**可以在长度/指示器缓冲区中返回以下值： **SQLFetch**  
  
-   可供返回的数据的长度  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 应用程序可以将以下值放在长度/指示器缓冲区中，以便与**SQLBulk 操作**或**SQLSetPos**一起使用 ：  
  
-   发送的数据的长度  
  
-   SQL_NTS  
  
-   SQL_NULL_DATA  
  
-   SQL_DATA_AT_EXEC  
  
-   SQL_LEN_DATA_AT_EXEC宏的结果  
  
-   SQL_COLUMN_IGNORE  
  
 如果指标缓冲区和长度缓冲区是单独的缓冲区，则指示器缓冲区只能返回SQL_NULL_DATA，而长度缓冲区可以返回所有其他值。  
  
 有关详细信息，请参阅[SQLBulk 操作函数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)[、SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)函数[、SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)函数[和使用长度/指标值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)。  
  
 如果*StrLen_or_IndPtr*为空指针，则不使用长度或指标值。 这是提取数据时的错误，并且数据为 NULL。  
  
 如果应用程序将在 64 位操作系统上运行，请参阅[ODBC 64 位信息](../../../odbc/reference/odbc-64-bit-information.md)。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLBindCol**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_STMT的*句柄类型*和*语句句柄*的*句柄*。 下表列出了**SQLBindCol**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|07006|受限数据类型属性冲突|（DM）*列编号*参数为 0，*并且 TargetType*参数不SQL_C_BOOKMARK或SQL_C_VARBOOKMARK。|  
|07009|无效描述符索引|为参数*ColumnNumber*指定的值超过了结果集中的最大列数。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY003|无效的应用程序缓冲区类型|参数*TargetType*既不是有效的数据类型，也不是SQL_C_DEFAULT。|  
|HY010|函数序列错误|（DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用**SQLBindCol**时，此异步函数仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore 结果**被调用语句*句柄*并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。<br /><br /> （DM） 为*语句句柄*调用了异步执行函数，并且在调用此函数时仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于**SQLExecute***语句句柄*并返回SQL_NEED_DATA。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY090|无效的字符串或缓冲区长度|（DM） 为参数*BufferLength*指定的值小于 0。<br /><br /> （DM） 驱动程序是 ODBC 2。*x*驱动程序 *，ColumnNumber*参数设置为 0，并为参数*BufferLength*指定的值不等于 4。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现可选功能|驱动程序或数据源不支持*由 TargetType*参数和相应列的特定于驱动程序的 SQL 数据类型的组合指定的转换。<br /><br /> 参数*列编号*为 0，驱动程序不支持书签。<br /><br /> 驱动程序仅支持 ODBC 2。*x*和参数*TargetType*是以下原因之一：<br /><br /> SQL_C_NUMERICSQL_C_SBIGINTSQL_C_UBIGINT<br /><br /> 和附录 D 中的[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)中列出的任何间隔 C 数据类型：数据类型。<br /><br /> 驱动程序仅支持 3.50 之前的 ODBC 版本，并且参数*TargetType* SQL_C_GUID。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*关联的驱动程序不支持该函数。|  
  
## <a name="comments"></a>注释  
 **SQLBindCol**用于将结果集中的列关联或*绑定*到应用程序中的数据缓冲区和长度/指示器缓冲区。 当应用程序调用**SQLFetch、SQLFetchScroll**或**SQLSetPos**来获取数据时，驱动程序将返回指定缓冲区中绑定列的数据;否则，驱动程序将返回指定缓冲区中绑定列的数据。 **SQLFetchScroll**有关详细信息，请参阅[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)。 当应用程序调用**SQLBulk操作**以更新或插入行或**SQLSetPos**以更新行时，驱动程序将从指定的缓冲区检索绑定列的数据;否则，驱动程序将检索绑定列的数据。有关详细信息，请参阅[SQLBulk 操作函数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)或[SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md)。 有关绑定的详细信息，请参阅[检索结果（基本）](../../../odbc/reference/develop-app/retrieving-results-basic.md)。  
  
 请注意，列不必绑定来从它们检索数据。 应用程序还可以调用**SQLGetData**从列检索数据。 尽管可以绑定行中的某些列并为其他列调用**SQLGetData，** 但受一些限制。 有关详细信息，请参阅[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)。  
  
## <a name="binding-unbinding-and-rebinding-columns"></a>绑定、取消绑定和重新绑定列  
 即使从结果集中获取数据，也可以在任何时候绑定、取消绑定或反弹。 下次调用使用绑定的函数时，新绑定将生效。 例如，假设应用程序将列绑定到结果集中并调用**SQLFetch**。 驱动程序返回绑定缓冲区中的数据。 现在假设应用程序将列绑定到一组不同的缓冲区。 驱动程序不会在新绑定的缓冲区中放置刚提取的行的数据。 相反，它会等待，直到再次调用**SQLFetch，** 然后将下一行的数据放在新绑定的缓冲区中。  
  
> [!NOTE]  
>  语句属性SQL_ATTR_USE_BOOKMARKS应始终在将列绑定到列 0 之前进行设置。 这不是必需的，但强烈建议这样做。  
  
## <a name="binding-columns"></a>绑定列  
 要绑定列，应用程序调用**SQLBindCol**并传递数据缓冲区的列号、类型、地址和长度以及长度/指示器缓冲区的地址。 有关如何使用这些地址的信息，请参阅本节后面的"缓冲区地址"。 有关绑定列的详细信息，请参阅使用[SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)。  
  
 推迟使用这些缓冲区;也就是说，应用程序在**SQLBindCol**中绑定它们，但驱动程序从其他函数（即**SQLBulk 操作****、SQLFetch、SQLFetchScroll**或**SQLSetPos）** 访问它们。 **SQLFetchScroll** 应用程序有责任确保**SQLBindCol**中指定的指针保持有效，只要绑定仍然有效。 如果应用程序允许这些指针无效（例如，它释放缓冲区），然后调用期望它们有效的函数，则后果未定义。 有关详细信息，请参阅[延迟缓冲区](../../../odbc/reference/develop-app/deferred-buffers.md)。  
  
 绑定仍然有效，直到它被新的绑定替换，列未绑定，或释放语句。  
  
## <a name="unbinding-columns"></a>取消绑定列  
 要取消绑定单个列，应用程序调用**SQLBindCol，***其中列号*设置为该列的编号，而*TargetValuePtr*设置为空指针。 如果*列编号*引用未绑定列 **，SQLBindCol**仍返回SQL_SUCCESS。  
  
 要取消绑定所有列，应用程序将**SQLFreeStmt**调用 *，fOption*设置为SQL_UNBIND。 这也可以通过将 ARD 的SQL_DESC_COUNT字段设置为零来实现。  
  
## <a name="rebinding-columns"></a>重新绑定列  
 应用程序可以执行两个操作中的任何一个来更改绑定：  
  
-   调用**SQLBindCol**为已绑定的列指定新绑定。 驱动程序用新绑定覆盖旧绑定。  
  
-   指定要添加到由绑定调用**SQLBindCol**指定的缓冲区地址的偏移量。 有关详细信息，请参阅下一节"绑定偏移量"。  
  
## <a name="binding-offsets"></a>绑定偏移  
 绑定偏移量是在取消引用之前添加到数据和长度/指标缓冲区的地址（如*TargetValuePtr*和*StrLen_or_IndPtr*参数中指定的值。 使用偏移时，绑定是应用程序缓冲区布局方式的"模板"，应用程序可以通过更改偏移量将此"模板"移动到不同的内存区域。 由于相同的偏移量添加到每个绑定中的每个地址，因此不同列的缓冲区之间的相对偏移量必须与每组缓冲区中的相对偏移量相同。 使用按行绑定时，始终如此;应用程序必须仔细布局其缓冲区，这样在使用按列绑定时为 true。  
  
 使用绑定偏移量与通过调用**SQLBindCol**重新绑定列的效果基本相同。 区别在于，对**SQLBindCol**的新调用指定数据缓冲区和长度/指示器缓冲区的新地址，而使用绑定偏移量不会更改地址，而只会向地址添加偏移量。 应用程序可以随时指定新的偏移量，并且此偏移量始终添加到最初绑定的地址。 特别是，如果偏移量设置为 0，或者如果语句属性设置为空指针，则驱动程序将使用最初绑定的地址。  
  
 要指定绑定偏移量，应用程序将SQL_ATTR_ROW_BIND_OFFSET_PTR语句属性设置到 SQLINTEGER 缓冲区的地址。 在应用程序调用使用绑定的函数之前，它会在此缓冲区中放置一个偏移量。 要确定要使用的缓冲区的地址，驱动程序将偏移量添加到绑定中的地址。 地址和偏移量的总和必须是有效地址，但向其添加偏移量的地址不必有效。 有关如何使用绑定偏移量的详细信息，请参阅本节后面的"缓冲区地址"。  
  
## <a name="binding-arrays"></a>绑定数组  
 如果行集大小（SQL_ATTR_ROW_ARRAY_SIZE语句属性的值）大于 1，则应用程序将绑定缓冲区的数组而不是单个缓冲区。 有关详细信息，请参阅[块游标](../../../odbc/reference/develop-app/block-cursors.md)。  
  
 应用程序可以通过两种方式绑定数组：  
  
-   将数组绑定到每列。 这称为*按列绑定*，因为每个数据结构（数组）包含单个列的数据。  
  
-   定义一个结构来保存整个行的数据并绑定这些结构的数组。 这称为*行绑定*，因为每个数据结构都包含单个行的数据。  
  
 每个缓冲区数组必须具有至少与行集大小相同的元素数。  
  
> [!NOTE]  
>  应用程序必须验证对齐是否有效。 有关对齐注意事项的详细信息，请参阅[对齐](../../../odbc/reference/develop-app/alignment.md)。  
  
## <a name="column-wise-binding"></a>按列绑定  
 在按列绑定中，应用程序将单独的数据和长度/指示器数组绑定到每列。  
  
 要使用按列绑定，应用程序首先将SQL_ATTR_ROW_BIND_TYPE语句属性设置为SQL_BIND_BY_COLUMN。 （这是默认值。对于要绑定的每个列，应用程序执行以下步骤：  
  
1.  分配数据缓冲区数组。  
  
2.  分配长度/指示器缓冲区的数组。  
  
    > [!NOTE]  
    >  如果使用按列绑定时应用程序直接写入描述符，则可以将单独的数组用于长度和指标数据。  
  
3.  使用以下参数调用**SQLBindCol：**  
  
    -   *TargetType*是数据缓冲区数组中单个元素的类型。  
  
    -   *目标价值Ptr*是数据缓冲区数组的地址。  
  
    -   *缓冲区长度*是数据缓冲区数组中单个元素的大小。 当数据为固定长度数据时，将忽略*BufferLength*参数。  
  
    -   *StrLen_or_IndPtr*长度/指示器数组的地址。  
  
 有关如何使用此信息的详细信息，请参阅本节后面的"缓冲区地址"。 有关按列绑定的详细信息，请参阅[列-Wise 绑定](../../../odbc/reference/develop-app/column-wise-binding.md)。  
  
## <a name="row-wise-binding"></a>按行绑定  
 在按行绑定中，应用程序定义一个结构，其中包含要绑定的每个列的数据和长度/指示器缓冲区。  
  
 要使用行绑定，应用程序将执行以下步骤：  
  
1.  定义一个结构来保存一行数据（包括数据和长度/指标缓冲区），并分配这些结构的数组。  
  
    > [!NOTE]  
    >  如果使用按行绑定时应用程序直接写入描述符，则可以将单独的字段用于长度和指标数据。  
  
2.  将SQL_ATTR_ROW_BIND_TYPE语句属性设置为包含单个数据行的结构大小，或将结果列绑定到的缓冲区实例的大小。 长度必须包含所有绑定列的空间以及结构或缓冲区的任何填充，以确保当绑定列的地址以指定长度递增时，结果将指向下一行中同一列的开头。 在 ANSI C 中使用*大小*运算符时，此行为得到保证。  
  
3.  调用**SQLBindCol，** 对要绑定的每个列具有以下参数：  
  
    -   *TargetType*是要绑定到列的数据缓冲区成员的类型。  
  
    -   *TargetValuePtr*是第一个数组元素中数据缓冲区成员的地址。  
  
    -   *缓冲区长度*是数据缓冲区成员的大小。  
  
    -   *StrLen_or_IndPtr*是要绑定的长度/指示器成员的地址。  
  
 有关如何使用此信息的详细信息，请参阅本节后面的"缓冲区地址"。 有关按列绑定的详细信息，请参阅[行-Wise 绑定](../../../odbc/reference/develop-app/row-wise-binding.md)。  
  
## <a name="buffer-addresses"></a>缓冲区地址  
 *缓冲区地址*是数据或长度/指示器缓冲区的实际地址。 驱动程序在缓冲区写入缓冲区之前（如在提取时间）之前计算缓冲区地址。 它根据以下公式计算，该公式使用*TargetValuePtr*中指定的地址 *，StrLen_or_IndPtr*参数、绑定偏移量和行号：  
  
 *绑定地址* + *绑定偏移*量 = （（*行号*- 1） x*元素大小*）  
  
 其中公式的变量定义如下表所述。  
  
|变量|描述|  
|--------------|-----------------|  
|*绑定地址*|对于数据缓冲区，在**SQLBindCol**中使用*TargetValuePtr*参数指定的地址。<br /><br /> 对于长度/指示器缓冲区，使用**SQLBindCol**中*StrLen_or_IndPtr*参数指定的地址。 有关详细信息，请参阅"描述符和 SQLBindCol"部分中的"附加注释"。<br /><br /> 如果绑定地址为 0，则不返回任何数据值，即使前一个公式计算的地址为非零。|  
|*绑定偏移*|如果使用按行绑定，则存储在使用SQL_ATTR_ROW_BIND_OFFSET_PTR语句属性指定的地址的值。<br /><br /> 如果使用按列绑定，或者SQL_ATTR_ROW_BIND_OFFSET_PTR语句属性的值为空指针，*则绑定偏移*量为 0。|  
|*Row Number*|行集中的行的 1 个基于的编号。 对于默认的单行提取，这是 1。|  
|*元素大小*|绑定数组中元素的大小。<br /><br /> 如果使用按列绑定，则长度/指示器缓冲区的大小**为（SQLINTEGER）。** 对于数据缓冲区，如果数据类型为可变长度，则为**SQLBindCol**中的*BufferLength*参数的值;如果数据类型为固定长度，则为数据类型的大小。<br /><br /> 如果使用按行绑定，则这是数据和长度/指示器缓冲区SQL_ATTR_ROW_BIND_TYPE语句属性的值。|  
  
## <a name="descriptors-and-sqlbindcol"></a>描述符和 SQLBindCol  
 以下各节介绍**SQLBindCol**如何与描述符进行交互。  
  
> [!CAUTION]  
>  为一个语句调用**SQLBindCol**可能会影响其他语句。 当显式分配与语句关联的 ARD 并且也与其他语句关联时，将发生这种情况。 由于**SQLBindCol**修改了描述符，因此修改将应用于与此描述符关联的所有语句。 如果这不是必需的行为，则应用程序在调用**SQLBindCol**之前应将其描述符与其他语句分离。  
  
## <a name="argument-mappings"></a>参数映射  
 从概念上讲 **，SQLBindCol**按顺序执行以下步骤：  
  
1.  调用**SQLGetStmtAttr**以获取 ARD 句柄。  
  
2.  调用**SQLGetDescField**获取此描述符的SQL_DESC_COUNT字段，如果*列数*参数中的值超过SQL_DESC_COUNT的值，则调用**SQLSetDescField**以将SQL_DESC_COUNT的值增加到*列号*。  
  
3.  多次调用**SQLSetDescField**将值分配给 ARD 的以下字段：  
  
    -   将SQL_DESC_TYPE和SQL_DESC_CONCISE_TYPE设置为*TargetType*的值，但如果*TargetType*是日期时间或间隔子类型的简洁标识符之一，则分别将SQL_DESC_TYPE设置为SQL_DATETIME或SQL_INTERVAL;将SQL_DESC_CONCISE_TYPE设置到简洁标识符;并将SQL_DESC_DATETIME_INTERVAL_CODE设置为相应的日期时间或间隔子代码。  
  
    -   设置一个或多个适用于*TargetType*的SQL_DESC_LENGTH、SQL_DESC_PRECISION、SQL_DESC_SCALE和SQL_DESC_DATETIME_INTERVAL_PRECISION。  
  
    -   将SQL_DESC_OCTET_LENGTH字段设置为*缓冲区长度*的值。  
  
    -   将SQL_DESC_DATA_PTR字段设置为*目标值*的值。  
  
    -   将SQL_DESC_INDICATOR_PTR字段设置为*StrLen_or_Ind*的值。 （请参阅以下段落。  
  
    -   将SQL_DESC_OCTET_LENGTH_PTR字段设置为*StrLen_or_Ind*的值。 （请参阅以下段落。  
  
 *StrLen_or_Ind*参数引用的变量用于指标和长度信息。 如果提取遇到列的空值，它将存储SQL_NULL_DATA此变量中;如果提取遇到列的 null 值，则它将存储SQL_NULL_DATA。否则，它将数据长度存储在此变量中。 将空指针传递为*StrLen_or_Ind*防止提取操作返回数据长度，但如果遇到空值且无法返回SQL_NULL_DATA，则使提取失败。  
  
 如果对**SQLBindCol**的调用失败，它将在 ARD 中设置的描述符字段的内容未定义，并且 ARD SQL_DESC_COUNT字段的值保持不变。  
  
## <a name="implicit-resetting-of-count-field"></a>COUNT 字段的隐式重置  
 **SQLBindCol**仅当增加SQL_DESC_COUNT值时，才会将SQL_DESC_COUNT*列编号*参数的值设置。 如果*TargetValuePtr*参数中的值为空指针，而*ColumnNumber*参数中的值等于SQL_DESC_COUNT（即，取消绑定最高绑定列时），则SQL_DESC_COUNT设置为最高剩余绑定列的数量。  
  
## <a name="cautions-regarding-sql_default"></a>关于SQL_DEFAULT注意事项  
 要成功检索列数据，应用程序必须正确确定应用程序缓冲区中数据的长度和起始点。 当应用程序指定显式*TargetType*时，很容易检测到应用程序误解。 但是，当应用程序指定*SQL_DEFAULT 的 TargetType*时 **，SQLBindCol**可以应用于与应用程序预期数据类型不同的数据类型的列，从更改元数据或将代码应用于其他列。 在这种情况下，应用程序可能并不总是确定提取的列数据的开始或长度。 这可能导致未报告的数据错误或内存冲突。  
  
## <a name="code-example"></a>代码示例  
 在下面的示例中，应用程序在客户表上执行**SELECT**语句，以返回按名称排序的客户帐号、名称和电话号码的结果集。 然后，它调用**SQLBindCol**将数据列绑定到本地缓冲区。 最后，应用程序使用**SQLFetch**提取每行数据，并打印每个客户的姓名、ID 和电话号码。  
  
 有关更多代码示例，请参阅[SQLBulk 操作函数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)[、SQLColumns 函数](../../../odbc/reference/syntax/sqlcolumns-function.md)[、SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)和[SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
```cpp  
// SQLBindCol_ref.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <stdio.h>  
  
#define UNICODE  
#include <sqlext.h>  
  
#define NAME_LEN 50  
#define PHONE_LEN 60
  
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
                  retcode = SQLBindCol(hstmt, 1, SQL_C_WCHAR, &sCustID, 100, &cbCustID);  
                  retcode = SQLBindCol(hstmt, 2, SQL_C_WCHAR, szName, NAME_LEN, &cbName);  
                  retcode = SQLBindCol(hstmt, 3, SQL_C_WCHAR, szPhone, PHONE_LEN, &cbPhone);   
  
                  // Fetch and print each row of data. On an error, display a message and exit.  
                  for (int i=0 ; ; i++) {  
                     retcode = SQLFetch(hstmt);  
                     if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO)  
                        show_error();  
                     if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
                     {
                        //replace wprintf with printf
                        //%S with %ls
                        //warning C4477: 'wprintf' : format string '%S' requires an argument of type 'char *'
                        //but variadic argument 2 has type 'SQLWCHAR *'
                        //wprintf(L"%d: %S %S %S\n", i + 1, sCustID, szName, szPhone);  
                        printf("%d: %ls %ls %ls\n", i + 1, sCustID, szName, szPhone);  
                    }    
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
  
 另请参阅[示例 ODBC 计划](../../../odbc/reference/sample-odbc-program.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|返回有关结果集中列的信息|[SQLDescribeCol 函数](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|获取数据块或滚动浏览结果集|[SQLFetchScroll Function（SQLFetchScroll 函数）](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|获取多行数据|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|在语句上释放列缓冲区|[SQLFreeStmt 函数](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|获取数据列的一部分或全部|[SQLGetData 函数](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|返回结果集列数|[SQLNumResultCols 函数](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
