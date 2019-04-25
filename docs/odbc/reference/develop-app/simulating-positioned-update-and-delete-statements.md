---
title: 模拟定位更新和删除语句 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- data updates [ODBC], positioned update or delete
- row identifiers [ODBC]
- positioned updates [ODBC]
- updating data [ODBC], positioned update or delete
ms.assetid: b24ed59f-f25b-4646-a135-5f3596abc1a4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d98d40ae24c68f90a304edb0293febfe76fac2c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62445889"
---
# <a name="simulating-positioned-update-and-delete-statements"></a>模拟定位更新和删除语句
如果数据源不支持定位的 update 和 delete 语句，该驱动程序可以模拟它们。 例如，ODBC 游标库模拟定位的更新和删除语句。 用于模拟定位的更新和删除语句的常规策略是将定位的语句转换为搜索的样式。 这是通过替换**WHERE CURRENT OF**与搜索子句**其中**标识的当前行的子句。  
  
 例如，因为 CustID 该列唯一标识 Customers 表中的每一行，定位 delete 语句  
  
```  
DELETE FROM Customers WHERE CURRENT OF CustCursor  
```  
  
 可能会转换为  
  
```  
DELETE FROM Customers WHERE (CustID = ?)  
```  
  
 该驱动程序可以使用下列任一*行标识符*中**其中**子句：  
  
-   其值用于标识唯一表中的每一行的列。 例如，调用**SQLSpecialColumns** SQL_BEST_ROWID 将返回最优列或一组列，以实现此目的。  
  
-   伪列，提供的某些数据源，以便可以唯一地标识每个行。 这些也可能是检索，则可以通过调用**SQLSpecialColumns**。  
  
-   唯一索引，如果可用。  
  
-   在结果集中的所有列。  
  
 完全在中，驱动程序应使用哪些列**其中**子句构造取决于驱动程序。 对某些数据源，确定行标识符可能代价高昂。 但是，它是更快地执行，并保证模拟的语句更新或删除了最多一行。 根据基础 DBMS 的功能，使用的行标识符可以是设置成本很高。 但是，它是更快地执行，并保证模拟的语句将更新或删除只占一行。 在结果集中使用的所有列的选项为通常更易于设置。 但是，若要执行的运行速度慢，并且如果列不唯一标识行，则可能会导致无意中被更新或删除的行，尤其是当结果的选择列表设置时，不包含基础表中存在的所有列。  
  
 根据其前面的策略驱动程序支持，应用程序可以选择哪种策略，它需要驱动程序用于 SQL_ATTR_SIMULATE_CURSOR 语句属性。 尽管它看起来有点奇怪的应用程序无意中更新或删除行的风险，但应用程序可以通过确保结果集中的列的唯一标识结果集中的每一行来消除这种风险。 这样，该驱动程序的无需执行此操作的工作。  
  
 如果该驱动程序选择使用行标识符，它会截获**SELECT FOR UPDATE**创建结果集的语句。 如果选择列表中的列不能有效地标识一行，该驱动程序会将必要的列添加到选择列表的末尾。 某些数据源具有始终唯一地标识一行，例如行 ID 列在 Oracle; 中的单个列如果此类列不可用，则驱动程序将此。 否则，该驱动程序会调用**SQLSpecialColumns**中每个表**FROM**子句来检索唯一地标识每个行的列的列表。 得出此技术的常见限制是，如果有多个表中的，游标模拟会失败**FROM**子句。  
  
 无论如何驱动程序标识行，它通常抽出**FOR UPDATE OF** off 子句**SELECT FOR UPDATE**语句，然后才能将其发送到数据源。 **的更新的**仅与定位 update 和 delete 语句使用子句。 不支持的数据源定位 update 和 delete 语句通常不支持它。  
  
 当应用程序提交时定位的 update 或 delete 语句的执行时，该驱动程序将替换**WHERE CURRENT OF**子句**其中**子句包含行标识符。 从使用中的每个列驱动程序维护的缓存中检索这些列的值**其中**子句。 该驱动程序已替换为后**其中**子句，它将语句发送到数据源进行执行。  
  
 例如，假设应用程序提交以下语句以创建结果集：  
  
```  
SELECT Name, Address, Phone FROM Customers FOR UPDATE OF Phone, Address  
```  
  
 如果应用程序已设置 SQL_ATTR_SIMULATE_CURSOR 请求保证唯一性的并且如果数据源不提供始终唯一地标识一行的伪列，驱动程序会调用**SQLSpecialColumns**为Customers 表，发现 CustID 是客户表的键并将这添加到选择列表中，并去除**FOR UPDATE OF**子句：  
  
```  
SELECT Name, Address, Phone, CustID FROM Customers  
```  
  
 如果应用程序未请求保证唯一性的该驱动程序仅抽出**FOR UPDATE OF**子句：  
  
```  
SELECT Name, Address, Phone FROM Customers  
```  
  
 假设应用程序滚动浏览结果集，并将以下定位的 update 语句的执行，其中 Cust，是对结果集的游标的名称：  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust  
```  
  
 如果应用程序未请求保证唯一性的该驱动程序将替换**其中**子句并将 CustID 参数绑定到其缓存中的变量：  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE (CustID = ?)  
```  
  
 如果应用程序未请求保证唯一性的该驱动程序将替换**其中**子句和绑定到其缓存中的变量的此子句中的名称、 地址和电话参数：  
  
```  
UPDATE Customers SET Address = ?, Phone = ?  
   WHERE (Name = ?) AND (Address = ?) AND (Phone = ?)  
```
