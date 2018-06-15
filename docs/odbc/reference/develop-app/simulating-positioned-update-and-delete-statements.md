---
title: Update 和 Delete 语句模拟定位 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- data updates [ODBC], positioned update or delete
- row identifiers [ODBC]
- positioned updates [ODBC]
- updating data [ODBC], positioned update or delete
ms.assetid: b24ed59f-f25b-4646-a135-5f3596abc1a4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1448481938ff0ef8e20ba4e6a85801b65024cbcc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913882"
---
# <a name="simulating-positioned-update-and-delete-statements"></a>模拟定位的 Update 和 Delete 语句
如果数据源不支持定位的更新和 delete 语句，该驱动程序可以模拟这些。 例如，ODBC 游标库模拟定位的 update 和 delete 语句。 用于模拟定位的 update 和 delete 语句的常规策略是将定位的语句转换到搜索的。 这通过替换**WHERE CURRENT OF**子句的搜索**其中**标识当前行的子句。  
  
 例如，由于 CustID 列唯一标识 Customers 表中的每一行，定位删除语句  
  
```  
DELETE FROM Customers WHERE CURRENT OF CustCursor  
```  
  
 可能转换为  
  
```  
DELETE FROM Customers WHERE (CustID = ?)  
```  
  
 驱动程序可以使用以下项之一*行标识符*中**其中**子句：  
  
-   其值用于标识唯一表中的每一行的列。 例如，调用**SQLSpecialColumns** SQL_BEST_ROWID 将返回的最佳列或一组用于此目的的列。  
  
-   伪列，提供的某些数据源，以便可以唯一地标识每个行。 这些也可能是检索，则可以通过调用**SQLSpecialColumns**。  
  
-   唯一索引是，如果可用时。  
  
-   在结果集中的所有列。  
  
 完全中，驱动程序应使用哪些列**其中**子句构造取决于该驱动程序。 对某些数据源，确定行标识符可以是代价高昂。 但是，它是更快地执行，并保证模拟的语句更新或删除最多行。 具体取决于基础 DBMS 的功能，使用行标识符可能很昂贵设置。 但是，它是更快地执行，并保证模拟的语句将更新或删除只包含一行。 在结果集中使用的所有列的选项是通常可以更轻松地设置。 但是，它会慢些，若要执行，并且如果列不唯一标识行，可能会导致正在无意中更新或删除的行，尤其是当结果的选择列表设置时，不包含基础表中存在的所有列。  
  
 根据其前面的策略驱动程序支持，应用程序可以选择哪种策略它想要将与 SQL_ATTR_SIMULATE_CURSOR 语句属性一起使用的驱动程序。 尽管可能看似奇怪风险无意中更新或删除行的应用程序，应用程序可以通过确保结果集中的列的唯一标识结果集中的每一行中删除此风险。 这可以节省驱动程序的无需执行此操作的工作量。  
  
 如果该驱动程序选择使用行标识符，它会截获**选择 FOR UPDATE**创建结果集的语句。 如果选择列表中的列不能有效地标识一行，驱动程序会将所需的列添加到选择列表的末尾。 某些数据源具有始终唯一标识一个行，例如 Oracle; 中的 ROWID 列的单个列这样的列是否可用，则该驱动程序将使用此。 否则，该驱动程序会调用**SQLSpecialColumns**中每个表**FROM**子句来检索的唯一标识每一行的列列表。 导致这种技术的一个常见限制是光标模拟失败中的多个表是否**FROM**子句。  
  
 无论驱动程序标识行的方式，它通常抽出**有关更新的**关闭子句**选择 FOR UPDATE**的语句才能将它发送到数据源。 **有关更新的**仅与定位 update 和 delete 语句使用子句。 数据源不支持定位更新和 delete 语句通常不支持它。  
  
 当应用程序提交的定位的更新或执行 delete 语句时，该驱动程序将替换**WHERE CURRENT OF**子句**其中**子句包含行标识符。 从每一列将驱动程序维护的它使用中的缓存中检索这些列的值**其中**子句。 驱动程序已替换为后**其中**子句，它将发送声明执行与数据源。  
  
 例如，假设应用程序提交以下语句以创建一个结果集：  
  
```  
SELECT Name, Address, Phone FROM Customers FOR UPDATE OF Phone, Address  
```  
  
 如果应用程序已设置 SQL_ATTR_SIMULATE_CURSOR 请求的保证唯一性，并且如果数据源不提供始终唯一标识行的伪列，该驱动程序调用**SQLSpecialColumns**为Customers 表，发现 CustID 是客户表的关键和将此添加到选择列表中，并且将去除**有关更新的**子句：  
  
```  
SELECT Name, Address, Phone, CustID FROM Customers  
```  
  
 如果应用程序不具有请求的保证唯一性，驱动程序去除仅**有关更新的**子句：  
  
```  
SELECT Name, Address, Phone FROM Customers  
```  
  
 假设应用程序滚动结果集并提交以下定位的 update 语句的执行，其中客户都位于结果集的光标的名称：  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust  
```  
  
 如果应用程序不具有请求的保证唯一性，驱动程序将替换**其中**子句并将 CustID 参数绑定到其缓存中的变量：  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE (CustID = ?)  
```  
  
 如果应用程序不具有请求的保证唯一性，驱动程序将替换**其中**子句和绑定到其缓存中的变量此子句中的名称、 地址和电话参数：  
  
```  
UPDATE Customers SET Address = ?, Phone = ?  
   WHERE (Name = ?) AND (Address = ?) AND (Phone = ?)  
```
