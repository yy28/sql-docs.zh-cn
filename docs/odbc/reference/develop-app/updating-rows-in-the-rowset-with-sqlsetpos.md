---
title: 使用 SQLSetPos 更新的行集中的行 |Microsoft 文档
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
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
- SQLSetPos function [ODBC], updating rows
ms.assetid: d83a8c2a-5aa8-4f19-947c-79a817167ee1
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 46335416ffa5c0b75388746e7e55493d9b09875d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="updating-rows-in-the-rowset-with-sqlsetpos"></a>使用 SQLSetPos 更新的行集中的行
更新操作的**SQLSetPos**使更新一个或多个选定的行的表，使用数据的应用程序缓冲区中的每个绑定列 （除非长度/指示器缓冲区中的值是 SQL_COLUMN_IGNORE） 的数据源。 未绑定的列将不会更新。  
  
 若要更新的行**SQLSetPos**，应用程序执行以下：  
  
1.  位置的行集缓冲区中的新数据值。 有关如何将长数据与发送信息**SQLSetPos**，请参阅[长数据、 SQLSetPos 和 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
2.  根据需要在每个列的长度/指示器缓冲区设置的值。 这是数据或 sql_nts 以绑定到字符串缓冲区的字节长度的列绑定到二进制缓冲区和 SQL_NULL_DATA 任何要设置为 NULL 的列的数据的列的字节长度。  
  
3.  这将不更新 SQL_COLUMN_IGNORE 为这些列的长度/指示器缓冲区中设置的值。 尽管应用程序可以跳过此步骤，并重新发送现有数据，这将是效率低下，风险将值发送到被截断时它们已读取的数据源。  
  
4.  调用**SQLSetPos**与*操作*设置为 SQL_UPDATE 和*RowNumber*设置为的行数，以更新。 如果*RowNumber*为 0，则更新的行集中的所有行。  
  
 后**SQLSetPos**返回时，当前行设置为更新的行。  
  
 更新的行集的所有行时 (*RowNumber*等于 0)，应用程序可以通过设置行操作数组 （由 SQL_ATTR_ROW_OPERATION_PTR 指向的相应元素来禁用对某些行的更新语句属性） 到 SQL_ROW_IGNORE。 行操作数组中的元素与行状态数组 （由 SQL_ATTR_ROW_STATUS_PTR 语句属性指向） 大小和数量相对应。 若要更新仅这些行在结果集中成功提取，尚未删除从行集中，该应用程序使用为行操作数组中提取行集的函数中的行状态数组**SQLSetPos**.  
  
 对于发送到数据源作为更新每一行，应用程序缓冲区应具有有效的行数据。 如果应用程序缓冲区已填写通过提取并保持了行状态数组，它在每个这些行位置的值不应为 SQL_ROW_DELETED、 SQL_ROW_ERROR 或 SQL_ROW_NOROW。  
  
 例如，下面的代码允许用户滚动 Customers 表和更新、 删除或添加新行。 它将之前调用的行集缓冲区中的新数据**SQLSetPos**若要更新或添加新行。 行集缓冲区来存放新行; 末尾分配额外的行这可以防止在缓冲区中放置的新行的数据时覆盖现有数据。  
  
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
