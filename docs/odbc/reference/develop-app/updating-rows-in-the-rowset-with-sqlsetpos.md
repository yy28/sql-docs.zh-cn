---
title: 使用 SQLSetPos 更新行集中的行 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
- SQLSetPos function [ODBC], updating rows
ms.assetid: d83a8c2a-5aa8-4f19-947c-79a817167ee1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dfb57a6512245c9adb36a511ce48721dd901995c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63313102"
---
# <a name="updating-rows-in-the-rowset-with-sqlsetpos"></a>使用 SQLSetPos 更新行集中的行
更新操作的**SQLSetPos**使数据源进行更新的表，在中使用数据的应用程序缓冲区对于每个绑定的列 （除非长度/指示器缓冲区中的值为 SQL_COLUMN_IGNORE） 的一个或多个所选的行。 未绑定的列将不会更新。  
  
 若要更新的行**SQLSetPos**，应用程序执行以下：  
  
1.  将新的数据值放在行集缓冲区中。 有关如何将长数据与发送的信息**SQLSetPos**，请参阅[长整型数据和 SQLSetPos 及 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
2.  根据需要在每个列的长度/指示器缓冲区中设置的值。 这是 sql_nts; 的数据的列绑定到字符串缓冲区绑定到二进制缓冲区和 SQL_NULL_DATA 的任何列设置为 NULL 的列的数据的字节长度的字节长度。  
  
3.  这不会更新为 SQL_COLUMN_IGNORE 这些列的长度/指示器缓冲区中设置的值。 不过应用程序可以跳过此步骤，并重新发送的现有数据，这会导致效率低下，并将值发送到已被截断，在读取时的数据源的风险。  
  
4.  调用**SQLSetPos**与*操作*设置为 SQL_UPDATE 并*RowNumber*设置为的行数，以更新。 如果*RowNumber*为 0，则更新行集中的所有行。  
  
 之后**SQLSetPos**返回当前行设置为已更新的行。  
  
 当更新行集的所有行时 (*RowNumber*等于 0)，应用程序可以通过设置 （由 SQL_ATTR_ROW_OPERATION_PTR 指向行操作数组的相应元素禁用对特定行的更新语句属性） 到 SQL_ROW_IGNORE。 行操作数组的大小和行状态数组 （由 SQL_ATTR_ROW_STATUS_PTR 语句属性指向） 的元素数与相对应。 若要更新仅行中的结果集已成功提取的和尚未从行集中删除，应用程序使用从函数到行操作数组的形式中提取行集的行状态数组**SQLSetPos**.  
  
 对于发送到数据源作为更新提供，每个行，应用程序缓冲区应具有有效的行数据。 如果应用程序缓冲区被提取并保持了行状态数组，它在每个这些行位置的值不应 SQL_ROW_DELETED、 SQL_ROW_ERROR 或 SQL_ROW_NOROW。  
  
 例如，下面的代码允许用户滚动浏览客户表和更新、 删除或添加新行。 它将新数据之前调用的行集缓冲区**SQLSetPos**要更新或添加新行。 额外的行分配末尾的行集的缓冲区来存放新行;这可防止在缓冲区中放置新行数据时覆盖现有数据。  
  
```  
#define UPDATE_ROW   100  
#define DELETE_ROW   101  
#define ADD_ROW      102  
  
SQLUINTEGER    CustIDArray[11];  
SQLCHAR        NameArray[11][51], AddressArray[11][51],   
               PhoneArray[11][11];  
SQLINTEGER     CustIDIndArray[11], NameLenOrIndArray[11],   
               AddressLenOrIndArray[11],  
               PhoneLenOrIndArray[11];  
SQLUSMALLINT   RowStatusArray[10], Action, RowNum;  
SQLRETURN      rc;  
SQLHSTMT       hstmt;  
  
// Set the SQL_ATTR_ROW_BIND_TYPE statement attribute to use column-wise   
// binding. Declare the rowset size with the SQL_ATTR_ROW_ARRAY_SIZE   
// statement attribute. Set the SQL_ATTR_ROW_STATUS_PTR statement   
// attribute to point to the row status array.  
SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_KEYSET_DRIVEN, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_TYPE, SQL_BIND_BY_COLUMN, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, 10, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
  
// Bind arrays to the CustID, Name, Address, and Phone columns.  
SQLBindCol(hstmt, 1, SQL_C_ULONG, CustIDArray, 0, CustIDIndArray);  
SQLBindCol(hstmt, 2, SQL_C_CHAR, NameArray, sizeof(NameArray[0]), NameLenOrIndArray);  
SQLBindCol(hstmt, 3, SQL_C_CHAR, AddressArray, sizeof(AddressArray[0]),  
            AddressLenOrIndArray);  
SQLBindCol(hstmt, 4, SQL_C_CHAR, PhoneArray, sizeof(PhoneArray[0]),  
            PhoneLenOrIndArray);  
  
// Execute a statement to retrieve rows from the Customers table.  
SQLExecDirect(hstmt, "SELECT CustID, Name, Address, Phone FROM Customers", SQL_NTS);  
  
// Fetch and display the first 10 rows.  
rc = SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
DisplayData(CustIDArray, CustIDIndArray, NameArray, NameLenOrIndArray, AddressArray,  
            AddressLenOrIndArray, PhoneArray, PhoneLenOrIndArray, RowStatusArray);  
  
// Call GetAction to get an action and a row number from the user.  
while (GetAction(&Action, &RowNum)) {  
   switch (Action) {  
  
      case SQL_FETCH_NEXT:  
      case SQL_FETCH_PRIOR:  
      case SQL_FETCH_FIRST:  
      case SQL_FETCH_LAST:  
      case SQL_FETCH_ABSOLUTE:  
      case SQL_FETCH_RELATIVE:  
         // Fetch and display the requested data.  
         SQLFetchScroll(hstmt, Action, RowNum);  
         DisplayData(CustIDArray, CustIDIndArray,  
                     NameArray, NameLenOrIndArray,  
                     AddressArray, AddressLenOrIndArray,  
                     PhoneArray, PhoneLenOrIndArray, RowStatusArray);  
         break;  
  
      case UPDATE_ROW:  
         // Place the new data in the rowset buffers and update the   
         // specified row.  
         GetNewData(&CustIDArray[RowNum - 1], &CustIDIndArray[RowNum - 1],  
                  NameArray[RowNum - 1], &NameLenOrIndArray[RowNum - 1],  
                  AddressArray[RowNum - 1], &AddressLenOrIndArray[RowNum - 1],  
                  PhoneArray[RowNum - 1], &PhoneLenOrIndArray[RowNum - 1]);  
         SQLSetPos(hstmt, RowNum, SQL_UPDATE, SQL_LOCK_NO_CHANGE);  
         break;  
  
      case DELETE_ROW:  
         // Delete the specified row.  
         SQLSetPos(hstmt, RowNum, SQL_DELETE, SQL_LOCK_NO_CHANGE);  
         break;  
  
      case ADD_ROW:  
         // Place the new data in the rowset buffers at index 10.   
         // This is an extra element for new rows so rowset data is   
         // not overwritten. Insert the new row. Row 11 corresponds   
         // to index 10.  
         GetNewData(&CustIDArray[10], &CustIDIndArray[10],  
                     NameArray[10], &NameLenOrIndArray[10],  
                     AddressArray[10], &AddressLenOrIndArray[10],  
                     PhoneArray[10], &PhoneLenOrIndArray[10]);  
         SQLSetPos(hstmt, 11, SQL_ADD, SQL_LOCK_NO_CHANGE);  
         break;  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```
