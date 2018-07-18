---
title: 处理字符转换时 ODBC 驱动程序行为更改 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client  - "database-engine" - "docset-sql-devref"
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 682a232a-bf89-4849-88a1-95b2fbac1467
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bcf868dde9f3ef6b019d06187696881509b9a568
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37415626"
---
# <a name="odbc-driver-behavior-change-when-handling-character-conversions"></a>处理字符转换时 ODBC 驱动程序行为的变化
  [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client ODBC 驱动程序 (SQLNCLI11.dll) 更改了它执行 SQL_WCHAR * (NCHAR/NVARCHAR/NVARCHAR(MAX)) 和 SQL_CHAR\* （CHAR/VARCHAR/NARCHAR(MAX)) 转换。 使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2012 Native Client ODBC 驱动程序时，ODBC 函数（如 SQLGetData、SQLBindCol、SQLBindParameter）返回 (-4) SQL_NO_TOTAL 作为长度/指示符参数。 以前版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序返回的长度值可能不正确。  
  
## <a name="sqlgetdata-behavior"></a>SQLGetData 行为  
 许多 Windows 函数允许指定缓冲区大小为 0，且返回的长度为返回的数据大小。 以下模式对于 Windows 程序员很常见：  
  
```  
int iSize = 0;  
BYTE * pBuffer = NULL;  
GetMyFavoriteAPI(pBuffer, &iSize);   // Returns needed size in iSize  
pBuffer = new BYTE[iSize];   // Allocate buffer   
GetMyFavoriteAPI(pBuffer, &iSize);   // Retrieve actual data  
```  
  
 但是， **SQLGetData**不应在此方案中使用。 不应使用以下模式：  
  
```  
// bad  
int iSize = 0;  
WCHAR * pBuffer = NULL;  
SQLGetData(hstmt, SQL_W_CHAR, ...., (SQLPOINTER*)0x1, 0, &iSize);   // Get storage size needed  
pBuffer = new WCHAR[(iSize/sizeof(WCHAR)) + 1];   // Allocate buffer  
SQLGetData(hstmt, SQL_W_CHAR, ...., (SQLPOINTER*)pBuffer, iSize, &iSize);   // Retrieve data  
```  
  
 **SQLGetData**仅可以调用以检索实际数据块区。 使用**SQLGetData**若要获取的数据大小不是不受支持。  
  
 下面说明当您使用不正确的模式时驱动程序变化的影响。 此应用程序将 `varchar` 列和绑定作为 Unicode (SQL_UNICODE/SQL_WCHAR) 查询：  
  
 查询：  `select convert(varchar(36), '123')`  
  
```  
SQLGetData(hstmt, SQL_WCHAR, ….., (SQLPOINTER*) 0x1, 0 , &iSize);   // Attempting to determine storage size needed  
```  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序版本|长度或指示符的结果|Description|  
|-----------------------------------------------------------------|---------------------------------|-----------------|  
|[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client 或更早版本|6|驱动程序错误地假定将 CHAR 转换为 WCHAR 可以通过长度 * 2 来实现。|  
|[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client（版本 11.0.2100.60）或更高版本|-4 (SQL_NO_TOTAL)|该驱动程序不再假定从 CHAR 到 WCHAR 或 CHAR 到 WCHAR 转换为 （乘） \*2 或 （除以） / 2 操作。<br /><br /> 调用**SQLGetData**不再返回预期的转换的长度。 驱动程序检测 CHAR 和 WCHAR 之间的转换并返回 (-4) SQL_NO_TOTAL 替代可能不正确的 *2 或 /2 行为。|  
  
 使用**SQLGetData**要检索的数据块。 （所示的伪代码：）  
  
```  
while( (SQL_SUCCESS or SQL_SUCCESS_WITH_INFO) == SQLFetch(...) ) {  
   SQLNumCols(...iTotalCols...)  
   for(int iCol = 1; iCol < iTotalCols; iCol++) {  
      WCHAR* pBufOrig, pBuffer = new WCHAR[100];  
      SQLGetData(.... iCol … pBuffer, 100, &iSize);   // Get original chunk  
      while(NOT ALL DATA RETREIVED (SQL_NO_TOTAL, ...) ) {  
         pBuffer += 50;   // Advance buffer for data retrieved  
         // May need to realloc the buffer when you reach current size  
         SQLGetData(.... iCol … pBuffer, 100, &iSize);   // Get next chunk  
      }  
   }  
}  
```  
  
## <a name="sqlbindcol-behavior"></a>SQLBindCol 行为  
 查询：  `select convert(varchar(36), '1234567890')`  
  
```  
SQLBindCol(… SQL_W_CHAR, …)   // Only bound a buffer of WCHAR[4] – Expecting String Data Right Truncation behavior  
```  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序版本|长度或指示符的结果|Description|  
|-----------------------------------------------------------------|---------------------------------|-----------------|  
|[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client 或更早版本|20|-   **SQLFetch**报告数据右侧被截断。<br />长度是返回非存储的数据的长度 (假定 * 2 CHAR 到 WCHAR 的转换可能不正确的标志符号)。<br />-存储在缓冲区中的数据为 123 \ 0。 缓冲区被保证为以 NULL 结束。|  
|[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client（版本 11.0.2100.60）或更高版本|-4 (SQL_NO_TOTAL)|-   **SQLFetch**报告数据右侧被截断。<br />长度指示-4 (SQL_NO_TOTAL)，因为未转换的数据的其余部分。<br />-存储在缓冲区中的数据为 123 \ 0。 - 缓冲区被保证为以 NULL 结束。|  
  
## <a name="sqlbindparameter-output-parameter-behavior"></a>SQLBindParameter（OUTPUT 参数行为）  
 查询：  `create procedure spTest @p1 varchar(max) OUTPUT`  
  
 `select @p1 = replicate('B', 1234)`  
  
```  
SQLBindParameter(… SQL_W_CHAR, …)   // Only bind up to first 64 characters  
```  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序版本|长度或指示符的结果|Description|  
|-----------------------------------------------------------------|---------------------------------|-----------------|  
|[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client 或更早版本|2468|-   **SQLFetch**返回没有更多的数据。<br />-   **SQLMoreResults**返回没有更多的数据。<br />长度指示在服务器上，不存储在缓冲区中返回的数据的大小。<br />-原始缓冲区包含 63 个字节和 NULL 终止符。 缓冲区被保证为以 NULL 结束。|  
|[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client（版本 11.0.2100.60）或更高版本|-4 (SQL_NO_TOTAL)|-   **SQLFetch**返回没有更多的数据。<br />-   **SQLMoreResults**返回没有更多的数据。<br />长度指示 (-4) SQL_NO_TOTAL，因为未转换的数据的其余部分。<br />-原始缓冲区包含 63 个字节和 NULL 终止符。 缓冲区被保证为以 NULL 结束。|  
  
## <a name="performing-char-and-wchar-conversions"></a>执行 CHAR 和 WCHAR 转换  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client ODBC 驱动程序提供几种执行 CHAR 和 WCHAR 转换的方式。 逻辑类似于处理 blob（varchar(max)、nvarchar(max)、…）：  
  
-   数据保存到或使用绑定时截断到指定的缓冲区**SQLBindCol**或**SQLBindParameter**。  
  
-   如果将未绑定，您可以使用检索区块中的数据**SQLGetData**并**SQLParamData**。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client 功能](sql-server-native-client-features.md)  
  
  
