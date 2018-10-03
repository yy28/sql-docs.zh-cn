---
title: SQLGetData | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetData function
ms.assetid: 204848be-8787-45b4-816f-a60ac9d56fcf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 208687bdc243b596b4b47d1696fdcea472552af3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48115082"
---
# <a name="sqlgetdata"></a>SQLGetData
  **SQLGetData**用于检索结果集数据，而无需绑定列的值。 **SQLGetData**可以从具有的列中检索大量的数据对同一列连续调用**文本**， **ntext**，或**映像**数据类型。  
  
 此时，不要求应用程序绑定变量来提取结果集数据。 可以从检索的任何列的数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序通过使用**SQLGetData**。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序不支持使用**SQLGetData**来检索随机列顺序中的数据。 使用处理所有未绑定的列**SQLGetData**必须具有在结果集中绑定列比更高版本的列序号。 应用程序必须按照从未绑定列的最小序号值到最大序号值的顺序处理数据。 尝试从较小序号的列中检索数据将导致错误。 如果某个应用程序使用服务器游标报告结果集行，则该应用程序可重新提取当前行，然后提取列值。 如果对默认只读的、 只进游标执行某个语句，必须重新执行该语句以备份**SQLGetData**。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序可准确报告的长度**文本**， **ntext**，并且**映像**使用检索的数据**SQLGetData**. 应用程序可以很好地利用*StrLen_or_IndPtr*参数返回内容来快速检索长整型数据。  
  
> [!NOTE]  
>  对于大值类型*StrLen_or_IndPtr*在数据截断的情况下将返回 SQL_NO_TOTAL。  
  
## <a name="sqlgetdata-support-for-enhanced-date-and-time-features"></a>SQLGetData 对日期和时间增强功能的支持  
 结果列的日期/时间类型的值将转换中所述[从 SQL 到 C 转换](../native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)。  
  
 有关详细信息，请参阅[日期和时间改进&#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlgetdata-support-for-large-clr-udts"></a>SQLGetData 对大型 CLR UDT 的支持  
 **SQLGetData**支持大型 CLR 用户定义类型 (Udt)。 有关详细信息，请参阅[Large CLR User-Defined 类型&#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="example"></a>示例  
  
```  
SQLHDBC     hDbc = NULL;  
SQLHSTMT    hStmt = NULL;  
long        lEmpID;  
PBYTE       pPicture;  
SQLINTEGER  pIndicators[2];  
  
// Get an environment, connection, and so on.  
...  
  
// Get a statement handle and execute a command.  
SQLAllocHandle(SQL_HANDLE_STMT, hDbc, &hStmt);  
  
if (SQLExecDirect(hStmt,  
    (SQLCHAR*) "SELECT EmployeeID, Photo FROM Employees",  
    SQL_NTS) == SQL_ERROR)  
    {  
    // Handle error and return.  
    }  
  
// Retrieve data from row set.  
SQLBindCol(hStmt, 1, SQL_C_LONG, (SQLPOINTER) &lEmpID, sizeof(long),  
    &pIndicators[0]);  
  
while (SQLFetch(hStmt) == SQL_SUCCESS)  
    {  
    cout << "EmployeeID: " << lEmpID << "\n";  
  
    // Call SQLGetData to determine the amount of data that's waiting.  
    if (SQLGetData(hStmt, 2, SQL_C_BINARY, pPicture, 0, &pIndicators[1])  
        == SQL_SUCCESS_WITH_INFO)  
        {  
        cout << "Photo size: " pIndicators[1] << "\n\n";  
  
        // Get all the data at once.  
        pPicture = new BYTE[pIndicators[1]];  
        if (SQLGetData(hStmt, 2, SQL_C_DEFAULT, pPicture,  
            pIndicators[1], &pIndicators[1]) != SQL_SUCCESS)  
            {  
            // Handle error and continue.  
            }  
  
        delete [] pPicture;  
        }  
    else  
        {  
        // Handle error on attempt to get data length.  
        }  
    }  
```  
  
## <a name="see-also"></a>请参阅  
 [SQLGetData 函数](http://go.microsoft.com/fwlink/?LinkId=59350)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
