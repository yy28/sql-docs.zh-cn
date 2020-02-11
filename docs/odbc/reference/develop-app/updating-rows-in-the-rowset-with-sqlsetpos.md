---
title: 用 SQLSetPos 更新行集中的行 |Microsoft Docs
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
ms.openlocfilehash: 0575c7ef7e380b1157640f9927e41192838c1ac0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68091601"
---
# <a name="updating-rows-in-the-rowset-with-sqlsetpos"></a>使用 SQLSetPos 更新行集中的行
**SQLSetPos**的更新操作使数据源可以更新表中的一个或多个选定行，并使用应用程序缓冲区中的数据作为每个绑定列（除非长度/指示器缓冲区中的值 SQL_COLUMN_IGNORE）。 不会更新未绑定的列。  
  
 若要更新**SQLSetPos**的行，应用程序执行以下操作：  
  
1.  将新数据值置于行集缓冲区中。 有关如何通过**SQLSetPos**发送长数据的信息，请参阅[Long data And SQLSetPos and SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
2.  根据需要设置每列的长度/指示器缓冲区中的值。 这是绑定到字符串缓冲区的列的数据或 SQL_NTS 的字节长度、绑定到二进制缓冲区的列的数据字节长度，以及要设置为 NULL 的所有列的 SQL_NULL_DATA。  
  
3.  设置那些列的长度/指示器缓冲区中的值，这些列不会更新为 SQL_COLUMN_IGNORE。 尽管应用程序可以跳过此步骤并重新发送现有数据，但这种情况很低效，将值发送到数据源（在读取时被截断）。  
  
4.  调用**** SQL_UPDATE SQLSetPos *，并将* *RowNumber*设置为要更新的行号。 如果*RowNumber*为0，则行集中的所有行都将被更新。  
  
 **SQLSetPos**返回后，将当前行设置为更新的行。  
  
 更新行集的所有行（*RowNumber*等于0）时，应用程序可以通过将行操作数组（由 SQL_ATTR_ROW_OPERATION_PTR 语句特性指向）的相应元素设置为 SQL_ROW_IGNORE 来禁用特定行的更新。 行操作数组对应于行状态数组的元素的大小和数量（由 SQL_ATTR_ROW_STATUS_PTR 语句特性指向）。 若要仅更新结果集中已成功获取并且尚未从行集中删除的那些行，应用程序将使用从提取行集的函数中的行状态数组作为行操作数组到**SQLSetPos**。  
  
 对于作为更新发送到数据源的每一行，应用程序缓冲区应具有有效的行数据。 如果已通过提取填充应用程序缓冲区，并且已维护行状态数组，则在这些行位置的每个位置上的值不应为 SQL_ROW_DELETED、SQL_ROW_ERROR 或 SQL_ROW_NOROW。  
  
 例如，以下代码允许用户滚动浏览 Customers 表，并更新、删除或添加新行。 它将新数据置于行集缓冲区中，然后再调用**SQLSetPos**以更新或添加新行。 在行集缓冲区末尾分配一个额外的行，以便保存新行;这可以防止在将新行的数据放置到缓冲区中时覆盖现有数据。  
  
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
