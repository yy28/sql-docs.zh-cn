---
title: SQL驱动程序功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDrivers
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDrivers
helpviewer_keywords:
- SQLDrivers function [ODBC]
ms.assetid: 6b5b7514-e9cb-4cfd-8b7a-ab51dfab9efa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2496e7cd5f2abe0831c72484bed374d7aa1513ce
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302758"
---
# <a name="sqldrivers-function"></a>SQLDrivers 函数
**一致性**  
 版本介绍： ODBC 2.0 标准合规性： ODBC  
  
 **摘要**  
 **SQLDriver**列出了驱动程序描述和驱动程序属性关键字。 此函数仅由驱动程序管理器实现。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLDrivers(  
     SQLHENV         EnvironmentHandle,  
     SQLUSMALLINT    Direction,  
     SQLCHAR *       DriverDescription,  
     SQLSMALLINT     BufferLength1,  
     SQLSMALLINT *   DescriptionLengthPtr,  
     SQLCHAR *       DriverAttributes,  
     SQLSMALLINT     BufferLength2,  
     SQLSMALLINT *   AttributesLengthPtr);  
```  
  
## <a name="arguments"></a>参数  
 *环境处理*  
 [输入]环境句柄。  
  
 *方向*  
 [输入]确定驱动程序管理器是获取列表中的下一个驱动程序说明（SQL_FETCH_NEXT），还是搜索从列表开头 （SQL_FETCH_FIRST） 开始。  
  
 *驱动程序描述*  
 [输出]指向要返回驱动程序描述的缓冲区的指针。  
  
 如果*驱动程序描述*为 NULL，*则描述长度Ptr*仍将返回字符总数（不包括字符数据的空终止字符），这些字符可在*驱动程序描述*指向的缓冲区中返回。  
  
 *缓冲区长度1*  
 [输入]**驱动程序描述*缓冲区的长度（以字符表示）。  
  
 *描述 长度*  
 [输出]指向缓冲区的指针，其中返回可在\**Driver 描述*中返回的字符总数（不包括空终止字符）。 如果可返回的字符数大于或等于*BufferLength1，* 则\**驱动程序描述中的驱动程序描述*将截断为*BufferLength1*减去空终止字符的长度。  
  
 *驱动程序属性*  
 [输出]指向要返回驱动程序属性值对列表的缓冲区的指针（请参阅"注释"）。  
  
 如果*驱动程序属性*为 NULL，*属性长度Ptr*仍将返回可用返回*的驱动程序属性*指向 的缓冲区中的字节总数（不包括字符数据的空终止字符）。  
  
 *缓冲区长度2*  
 [输入]\**驱动程序属性*缓冲区的长度（以字符表示）。 如果*\*Driver 描述*值是 Unicode 字符串（在调用**SQLDriverW**时），*缓冲区长度*参数必须是偶数。  
  
 *属性长度Ptr*  
 [输出]指向缓冲区的指针，用于返回可在\**DriverAttributes*中返回的字节总数（不包括空终止字节）。 如果可供返回的字节数大于或等于*BufferLength2，* 则\**DriverAttributes*中的属性值对列表将截断为*BufferLength2*减去空终止字符的长度。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLDrivers**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_ENV*Handle*的*句柄类型*和环境*句柄*句柄。 下表列出了**SQLDRIVERS**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|（DM） 特定于驱动程序管理器的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01004|字符串数据，右截断|（DM） 缓冲区\**驱动程序描述*不够大，无法返回完整的驱动程序说明。 因此，描述被截断。 完整的驱动程序描述的长度在\**描述长度Ptr*中返回。 （函数返回SQL_SUCCESS_WITH_INFO。<br /><br /> （DM） 缓冲区\**驱动程序属性*不够大，无法返回属性值对的完整列表。 因此，列表被截断。 属性值对的未压缩列表的长度在 **属性长度Ptr*中返回。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|（DM） 驱动程序管理器无法分配支持执行或完成函数所需的内存。|  
|HY010|函数序列错误|（DM） **SQLExecute、SQLExecDirect**或**SQLMore 结果**被调用语句*句柄*并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY090|无效的字符串或缓冲区长度|（DM） 为参数*BufferLength1*指定的值小于 0。<br /><br /> （DM） 为参数*BufferLength2*指定的值小于 0 或等于 1。|  
|HY103|无效检索代码|（DM） 为参数*方向*指定的值不等于SQL_FETCH_FIRST或SQL_FETCH_NEXT。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
  
## <a name="comments"></a>注释  
 **SQLDriver**在驱动程序描述缓冲区中\*返回*驱动程序说明*。 它将有关\**DriverAttributes*缓冲区中的驱动程序的其他信息作为关键字-值对的列表。 驱动程序的系统信息中列出的所有关键字都将返回所有驱动程序，但**CreateDSN**除外，它用于提示数据源的创建，因此是可选的。 每个对都用空字节终止，并且整个列表用空字节终止（即，两个空字节标记列表的末尾）。 例如，使用 C 语法的基于文件的驱动程序可能会返回以下属性列表（"\0"表示空字符）：  
  
```  
FileUsage=1\0FileExtns=*.dbf\0\0  
```  
  
 如果\* *DriverAttributes*不够大以容纳整个列表，则列表将被截断 **，SQLDriver**返回 SQLSTATE 01004（数据截断），并且列表的长度（不包括最终的 null 终止字节）在 #*属性LengthPtr*中返回。  
  
 安装驱动程序时，将从系统信息中添加驱动程序属性关键字。 有关详细信息，请参阅安装[ODBC 组件](../../../odbc/reference/install/installing-odbc-components.md)。  
  
 应用程序可以多次调用**SQLDriver**来检索所有驱动程序说明。 驱动程序管理器从系统信息中检索此信息。 当不再有驱动程序描述时 **，SQLDriver**将返回SQL_NO_DATA。 如果在**SQLDriver**返回SQL_NO_DATA后立即调用 SQL_FETCH_NEXT，它将返回第一个驱动程序说明。 有关应用程序如何使用**SQLDriver**返回的信息的信息，请参阅[选择数据源或驱动程序](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 如果SQL_FETCH_NEXT在第一次调用时传递给**SQLDrivers，****则 SQLDrivers**将返回第一个数据源名称。  
  
 由于**SQLDriver**是在驱动程序管理器中实现的，因此无论特定驱动程序的标准符合性如何，它都支持所有驱动程序。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|发现并列出连接到数据源所需的值|[SQLBrowseConnect 函数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|连接到数据源|[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|返回数据源名称|[SQLDataSources 函数](../../../odbc/reference/syntax/sqldatasources-function.md)|  
|使用连接字符串或对话框连接到数据源|[SQLDriverConnect 函数](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
