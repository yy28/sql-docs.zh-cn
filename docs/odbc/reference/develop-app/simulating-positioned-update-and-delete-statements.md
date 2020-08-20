---
description: 模拟定位更新和删除语句
title: 模拟定位的 Update 和 Delete 语句 |Microsoft Docs
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
ms.openlocfilehash: 06f6faad1b5b6cb83616575ea8732cac98b88ed0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499810"
---
# <a name="simulating-positioned-update-and-delete-statements"></a>模拟定位更新和删除语句
如果数据源不支持定位的 update 和 delete 语句，则驱动程序可以模拟这些语句。 例如，ODBC 游标库模拟定位的 update 和 delete 语句。 用于模拟定位的 update 和 delete 语句的常规策略是将定位语句转换为搜索语句。 这是通过将 **WHERE CURRENT** of 子句替换为用于标识当前行的搜索 **where** 子句来完成的。  
  
 例如，由于 CustID 列唯一标识 Customers 表中的每一行，因此定位的 delete 语句  
  
```  
DELETE FROM Customers WHERE CURRENT OF CustCursor  
```  
  
 可能被转换为  
  
```  
DELETE FROM Customers WHERE (CustID = ?)  
```  
  
 驱动程序可以在**WHERE**子句中使用以下*行标识符*之一：  
  
-   其值用于唯一标识表中的每一行的列。 例如，通过 SQL_BEST_ROWID 调用 **SQLSpecialColumns** 将返回为此目的而提供服务的最优列或一组列。  
  
-   由某些数据源提供的伪列，目的是唯一标识每个行。 它们还可以通过调用 **SQLSpecialColumns**来检索。  
  
-   唯一索引（如果可用）。  
  
-   结果集中的所有列。  
  
 驱动程序在其构造的 **WHERE** 子句中使用的确切列取决于驱动程序。 在某些数据源上，确定行标识符可能会很高。 但是，执行速度更快，并保证模拟语句最多更新或删除一行。 根据基础 DBMS 的功能，设置行标识符可能需要很高的成本。 但是，执行速度更快，并保证模拟语句仅更新或删除一行。 使用结果集中所有列的选项通常更容易进行设置。 但是，执行速度较慢，并且如果列没有唯一地标识行，则可能会导致意外更新或删除行，尤其是在结果集的选择列表不包含基础表中存在的所有列的情况下。  
  
 根据驱动程序支持的上述策略，应用程序可以选择它希望驱动程序与 SQL_ATTR_SIMULATE_CURSOR 语句属性一起使用的策略。 尽管应用程序可能会在无意中更新或删除行的情况下出现异常情况，但应用程序可以通过确保结果集中的列唯一标识结果集中的每一行来消除此风险。 这样就可以节省驱动程序的工作量。  
  
 如果驱动程序选择使用行标识符，则会截获创建结果集的 **SELECT FOR UPDATE** 语句。 如果选择列表中的列不能有效地标识行，则驱动程序会将所需的列添加到选择列表的末尾。 某些数据源具有始终唯一标识行的单列，如 Oracle 中的 ROWID 列;如果此类列可用，则驱动程序将使用此类。 否则，驱动程序将为**FROM**子句中的每个表调用**SQLSpecialColumns** ，以检索唯一标识每行的列的列表。 此方法产生的一个常见限制是，如果 **from** 子句中有多个表，则游标模拟失败。  
  
 无论驱动程序如何标识行，在将其发送到数据源之前，它通常会将子句 **更新为** **SELECT for update** 语句。 **FOR update** of 子句仅用于定位的 update 和 delete 语句。 不支持定位更新和删除语句的数据源通常不支持。  
  
 当应用程序提交要执行的定位更新或删除语句时，驱动程序会将 **WHERE CURRENT** of 子句替换为包含行标识符的 **where** 子句。 这些列的值是从驱动程序为在 **WHERE** 子句中使用的每个列维护的缓存中检索的。 驱动程序替换了 **WHERE** 子句后，它会将语句发送到数据源以便执行。  
  
 例如，假设应用程序提交以下语句以创建结果集：  
  
```  
SELECT Name, Address, Phone FROM Customers FOR UPDATE OF Phone, Address  
```  
  
 如果应用程序已将 SQL_ATTR_SIMULATE_CURSOR 设置为请求唯一性保证，并且如果数据源未提供始终唯一标识行的伪列，则该驱动程序将为 Customers 表调用 **SQLSpecialColumns** ，发现 CustID 是 customers 表的键，并将其添加到选择列表，并将其添加到 select 列表，并将其用于子句的 **UPDATE** 语句：  
  
```  
SELECT Name, Address, Phone, CustID FROM Customers  
```  
  
 如果应用程序未请求保证唯一性，驱动程序将仅去除子句 **更新** ：  
  
```  
SELECT Name, Address, Phone FROM Customers  
```  
  
 假设应用程序滚动结果集，并提交以下位置的 update 语句来执行，其中，"用户名" 是结果集上的游标的名称：  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust  
```  
  
 如果应用程序未请求保证唯一性，驱动程序将替换 **WHERE** 子句，并将 CustID 参数绑定到其缓存中的变量：  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE (CustID = ?)  
```  
  
 如果应用程序未请求保证唯一性，则驱动程序将替换 **WHERE** 子句，并将此子句中的名称、地址和电话参数绑定到其缓存中的变量：  
  
```  
UPDATE Customers SET Address = ?, Phone = ?  
   WHERE (Name = ?) AND (Address = ?) AND (Phone = ?)  
```
