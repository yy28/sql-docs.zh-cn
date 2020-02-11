---
title: SQLDrivers 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f54be3d11f4870533513f464c1afdae13e04f367
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68104666"
---
# <a name="sqldrivers-function"></a>SQLDrivers 函数
**度**  
 引入的版本： ODBC 2.0 标准符合性： ODBC  
  
 **总结**  
 **SQLDrivers**列出驱动程序说明和驱动程序属性关键字。 此函数仅由驱动程序管理器实现。  
  
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
 *EnvironmentHandle*  
 送环境句柄。  
  
 *方向键*  
 送确定驱动程序管理器是获取列表中的下一个驱动程序说明（SQL_FETCH_NEXT），还是从列表的开头开始搜索（SQL_FETCH_FIRST）。  
  
 *DriverDescription*  
 输出指向要返回驱动程序说明的缓冲区的指针。  
  
 如果*DriverDescription*为 NULL，则*DescriptionLengthPtr*仍将返回可用于在*DriverDescription*所指向的缓冲区中返回的字符总数（字符数据的 NULL 终止字符除外）。  
  
 *BufferLength1*  
 送**DriverDescription*缓冲区的长度（以字符为限）。  
  
 *DescriptionLengthPtr*  
 输出指向缓冲区的指针，将在此缓冲区中返回可在\* *DriverDescription*中返回的字符总数（不包括 null 终止字符）。 如果可返回的字符数大于或等于*BufferLength1*，则\* *DriverDescription*中的驱动程序说明将截断为*BufferLength1*减去 null 终止字符的长度。  
  
 *DriverAttributes*  
 输出指向缓冲区的指针，将在此缓冲区中返回驱动程序属性值对的列表（请参阅 "注释"）。  
  
 如果*DriverAttributes*为 NULL，则*AttributesLengthPtr*将仍返回在*DriverAttributes*指向的缓冲区中可返回的总字节数（不包括字符数据的 NULL 终止字符）。  
  
 *BufferLength2*  
 送\* *DriverAttributes*缓冲区的长度（以字符为限）。 如果* \*DriverDescription*值是 Unicode 字符串（在调用**SQLDriversW**时），则*BufferLength*参数必须是偶数。  
  
 *AttributesLengthPtr*  
 输出指向缓冲区的指针，该缓冲区用于返回可在\* *DriverAttributes*中返回的总字节数（不包括 null 终止字节）。 如果可返回的字节数大于或等于*BufferLength2*，则\* *DriverAttributes*中的属性值对列表将被截断为*BufferLength2*减去 null 终止字符的长度。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLDrivers**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 时，可以通过使用*HandleType*的 SQL_HANDLE_ENV 和*EnvironmentHandle*的*句柄*调用**SQLGetDiagRec**来获取关联的 SQLSTATE 值。 下表列出了通常由**SQLDrivers**返回的 SQLSTATE 值，并对该函数的上下文中的每个值进行了说明："（DM）" 表示法位于驱动程序管理器返回的 SQLSTATEs 的说明之前。 除非另有说明，否则与每个 SQLSTATE 值相关联的返回代码将 SQL_ERROR。  
  
|SQLSTATE|错误|说明|  
|--------------|-----------|-----------------|  
|01000|一般警告|（DM）驱动程序管理器特定的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|（DM）缓冲区\* *DriverDescription*不够大，无法返回完整的驱动程序描述。 因此，说明已被截断。 完整驱动程序描述的长度将在\* *DescriptionLengthPtr*中返回。 （函数返回 SQL_SUCCESS_WITH_INFO。）<br /><br /> （DM）缓冲区\* *DriverAttributes*不够大，无法返回属性值对的完整列表。 因此，列表已被截断。 在 **AttributesLengthPtr*中返回属性值对的未截断列表的长度。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|HY000|常规错误|发生了一个错误，该错误没有特定的 SQLSTATE，没有为其定义实现特定的 SQLSTATE。 MessageText 缓冲区中的**SQLGetDiagRec**返回的错误消息描述了错误及其原因。 * \**|  
|HY001|内存分配错误|（DM）驱动程序管理器无法分配支持执行或完成该函数所需的内存。|  
|HY010|函数序列错误|为*StatementHandle*调用了**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** ，并返回 SQL_PARAM_DATA_AVAILABLE。 在检索所有流式处理参数的数据之前调用此函数。|  
|HY013|内存管理错误|未能处理函数调用，原因可能是由于内存不足而无法访问基础内存对象。|  
|HY090|字符串或缓冲区长度无效|（DM）为参数*BufferLength1*指定的值小于0。<br /><br /> （DM）为参数*BufferLength2*指定的值小于0或等于1。|  
|HY103|检索代码无效|（DM）为参数*方向*指定的值不等于 SQL_FETCH_FIRST 或 SQL_FETCH_NEXT。|  
|HY117|由于未知的事务状态，连接被挂起。 仅允许断开连接和只读函数。|（DM）有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
  
## <a name="comments"></a>注释  
 **SQLDrivers**返回\* *DriverDescription*缓冲区中的驱动程序说明。 它以关键字-值对列表的形式\*返回有关*DriverAttributes*缓冲区中的驱动程序的其他信息。 对于所有驱动程序，将返回所有驱动程序的系统信息中列出的所有关键字（ **CreateDSN**除外），这是用于提示创建数据源，因此是可选的。 每对都以 null 字节结束，并以 null 字节结束（即，两个 null 字节标记列表的末尾）。 例如，使用 C 语法的基于文件的驱动程序可能返回以下属性列表（"\ 0" 表示 null 字符）：  
  
```  
FileUsage=1\0FileExtns=*.dbf\0\0  
```  
  
 如果\* *DriverAttributes*的大小不足以容纳整个列表，则会截断列表， **SQLDrivers**返回 SQLSTATE 01004 （数据已截断），并且将在 **AttributesLengthPtr*中返回列表的长度（不包括最终的 null 终止字节）。  
  
 安装驱动程序时，会从系统信息中添加驱动程序属性关键字。 有关详细信息，请参阅[安装 ODBC 组件](../../../odbc/reference/install/installing-odbc-components.md)。  
  
 应用程序可以多次调用**SQLDrivers**来检索所有驱动程序说明。 驱动程序管理器从系统信息中检索此信息。 当没有更多驱动程序说明时， **SQLDrivers**将返回 SQL_NO_DATA。 如果在 SQL_FETCH_NEXT 返回 SQL_NO_DATA 后立即调用**SQLDrivers** ，则返回第一个驱动程序说明。 有关应用程序如何使用**SQLDrivers**返回的信息的信息，请参阅[选择数据源或驱动程序](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 如果在首次调用**SQLDrivers**时将 SQL_FETCH_NEXT 传递给，则**SQLDrivers**将返回第一个数据源名称。  
  
 由于**SQLDrivers**是在驱动程序管理器中实现的，因此无论特定驱动程序的标准符合性如何，所有驱动程序都支持它。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|请参阅|  
|---------------------------|---------|  
|发现和列出连接到数据源所需的值|[SQLBrowseConnect 函数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|连接到数据源|[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|返回数据源名称|[SQLDataSources 函数](../../../odbc/reference/syntax/sqldatasources-function.md)|  
|使用连接字符串或对话框连接到数据源|[SQLDriverConnect 函数](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
