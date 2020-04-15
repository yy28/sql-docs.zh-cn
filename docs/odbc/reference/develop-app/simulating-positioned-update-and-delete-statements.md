---
title: 模拟定位更新和删除语句 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e1eb498a99180d145147e67c8955eeb7a0027024
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301988"
---
# <a name="simulating-positioned-update-and-delete-statements"></a>模拟定位更新和删除语句
如果数据源不支持定位更新和删除语句，驱动程序可以模拟这些语句。 例如，ODBC 游标库模拟定位更新和删除语句。 模拟定位更新和删除语句的一般策略是将定位语句转换为搜索的语句。 这是通过将**WHERE CURRENT OF**子句替换为标识当前行的搜索**WHERE**子句来实现的。  
  
 例如，由于 CustID 列唯一标识了"客户"表中的每一行，因此定位删除语句  
  
```  
DELETE FROM Customers WHERE CURRENT OF CustCursor  
```  
  
 可能转换为  
  
```  
DELETE FROM Customers WHERE (CustID = ?)  
```  
  
 驱动程序可以使用**WHERE**子句中的以下*行标识符*之一：  
  
-   其值用于唯一标识表中每行的列。 例如，使用SQL_BEST_ROWID调用**SQL 特别列**将返回用于此目的的最佳列或列集。  
  
-   伪列，由某些数据源提供，用于唯一标识每行。 通过调用**SQL 特殊列，** 也可以检索这些。  
  
-   唯一索引（如果可用）。  
  
-   结果集中的所有列。  
  
 驱动程序在它构造的**WHERE**子句中应使用的确切列取决于驱动程序。 在某些数据源上，确定行标识符可能成本高昂。 但是，执行并保证模拟语句最多更新或删除一行会更快。 根据基础 DBMS 的功能，使用行标识符设置可能非常昂贵。 但是，执行速度更快，并且保证模拟语句将仅更新或删除一行。 使用结果集中的所有列的选项通常更易于设置。 但是，执行速度较慢，如果列不唯一标识行，则可能导致意外更新或删除行，尤其是当结果集的 Select 列表不包含基础表中存在的所有列时。  
  
 根据驱动程序支持的前策略，应用程序可以选择希望驱动程序与SQL_ATTR_SIMULATE_CURSOR语句属性一起使用的策略。 尽管应用程序可能会无意中更新或删除行，但应用程序可以通过确保结果集中的列唯一标识结果集中的每一行来消除此风险。 这节省了驱动程序必须执行此操作的努力。  
  
 如果驱动程序选择使用行标识符，它将拦截创建结果集的 **"选择更新**"语句。 如果选择列表中的列无法有效地标识行，则驱动程序将必要的列添加到选择列表的末尾。 某些数据源具有一个列，该列始终唯一标识行，例如 Oracle 中的 ROWID 列;如果此类列可用，驱动程序将使用此列。 否则，驱动程序会为**FROM**子句中的每个表调用**SQL 特别列**，以检索唯一标识每一行的列的列表。 此技术产生的一个常见限制是，如果**FROM**子句中有多个表，则游标模拟将失败。  
  
 无论驱动程序如何标识行，它通常会在将"选择更新"语句发送到数据源之前，将**FOR UPDATE OF**子句从 **"选择更新"** 语句中剥离。 **FOR 更新子**句仅用于定位的更新和删除语句。 不支持定位更新和删除语句的数据源通常不支持它。  
  
 当应用程序提交定位的更新或删除语句以执行时，驱动程序将**WHERE CURRENT OF**子句替换为包含行标识符的**WHERE**子句。 这些列的值是从驱动程序为其在**WHERE**子句中使用的每个列维护的缓存中检索的。 驱动程序替换**WHERE**子句后，它将语句发送到数据源进行执行。  
  
 例如，假设应用程序提交以下语句以创建结果集：  
  
```  
SELECT Name, Address, Phone FROM Customers FOR UPDATE OF Phone, Address  
```  
  
 如果应用程序已设置SQL_ATTR_SIMULATE_CURSOR请求唯一性保证，并且数据源未提供始终唯一标识行的伪列，则驱动程序将调用客户表的**SQL 特别列**，发现 CustID 是客户表的键，并将其添加到选择列表中，并删除**FOR UPDATE OF**子句：  
  
```  
SELECT Name, Address, Phone, CustID FROM Customers  
```  
  
 如果应用程序未请求唯一性保证，则驱动程序仅删除 FOR 更新**OF**子句：  
  
```  
SELECT Name, Address, Phone FROM Customers  
```  
  
 假设应用程序滚动浏览结果集并提交以下定位的更新语句进行执行，其中 Cust 是结果集上的游标名称：  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust  
```  
  
 如果应用程序未请求唯一性保证，驱动程序将替换**WHERE**子句并将 CustID 参数绑定到其缓存中的变量：  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE (CustID = ?)  
```  
  
 如果应用程序未请求唯一性保证，驱动程序将替换**WHERE**子句，并将此子句中的名称、地址和 Phone 参数绑定到其缓存中的变量：  
  
```  
UPDATE Customers SET Address = ?, Phone = ?  
   WHERE (Name = ?) AND (Address = ?) AND (Phone = ?)  
```
