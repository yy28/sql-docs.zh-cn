---
title: SQLGetData |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetData function
ms.assetid: 204848be-8787-45b4-816f-a60ac9d56fcf
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 27b8fe304f26c60697e5d6fb147be20e30c86094
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2019
ms.locfileid: "73786537"
---
# <a name="sqlgetdata"></a>SQLGetData
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **SQLGetData**用于检索结果集数据，而不绑定列值。 可以对同一列连续调用**SQLGetData** ，以从具有**text**、 **ntext**或**image**数据类型的列中检索大量数据。  
  
 此时，不要求应用程序绑定变量来提取结果集数据。 可以使用**SQLGetData**从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驱动程序检索任意列的数据。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序不支持使用**SQLGetData**以随机列顺序检索数据。 使用**SQLGetData**处理的所有未绑定列都必须具有比结果集中绑定列更高的列序号。 应用程序必须按照从未绑定列的最小序号值到最大序号值的顺序处理数据。 尝试从较小序号的列中检索数据将导致错误。 如果某个应用程序使用服务器游标报告结果集行，则该应用程序可重新提取当前行，然后提取列值。 如果对默认的只读、只进游标执行语句，则必须重新执行该语句来备份**SQLGetData**。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序准确报告使用**SQLGetData**检索到的**text**、 **ntext**和**image**数据的长度。 应用程序可以充分利用*StrLen_or_IndPtr*参数返回，以便快速检索长数据。  
  
> [!NOTE]  
>  对于大值类型，在数据截断的情况下*StrLen_or_IndPtr*将返回 SQL_NO_TOTAL。  
  
## <a name="sqlgetdata-support-for-enhanced-date-and-time-features"></a>SQLGetData 对日期和时间增强功能的支持  
 日期/时间类型的结果列值按[从 SQL 到 C 的转换](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)中所述进行转换。  
  
 有关详细信息，请参阅[日期和时间&#40;改进&#41;ODBC](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlgetdata-support-for-large-clr-udts"></a>SQLGetData 对大型 CLR UDT 的支持  
 **SQLGetData**支持大型 CLR 用户定义类型（udt）。 有关详细信息，请参阅[大型 CLR 用户定义类型&#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [SQLGetData 函数](https://go.microsoft.com/fwlink/?LinkId=59350)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
