---
title: ODBC 动态游标 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], dynamic
- dynamic cursors [ODBC]
ms.assetid: de709fd3-9eb2-44e1-a2f0-786e2b9602a6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f94b83ef1458cd9f8368d1bea3a39682bd80b1a2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302319"
---
# <a name="odbc-dynamic-cursors"></a>ODBC 动态游标
动态游标就是动态游标。 它可以检测到打开游标后对结果集的成员资格、顺序和值所做的任何更改。 例如，假设动态游标提取两行，然后另一个应用程序将更新这两行之一并删除另一行。 如果动态游标尝试重新提取这些行，则它将找不到已删除的行，但会返回已更新行的新值。  
  
 动态游标会检测所有更新、删除和插入操作，它们都是它们自己的，而是由其他人进行的。 （这取决于由 SQL_ATTR_TXN_ISOLATION 连接属性设置的事务隔离级别。）SQL_ATTR_ROW_STATUS_PTR 语句特性指定的行状态数组反映了这些更改，并可包含 SQL_ROW_SUCCESS、SQL_ROW_SUCCESS_WITH_INFO、SQL_ROW_ERROR、SQL_ROW_UPDATED 和 SQL_ROW_ADDED。 它无法返回 SQL_ROW_DELETED，因为动态游标不返回行集外部的已删除行，因此不再识别结果集中的已删除行或该行状态数组中的相应元素是否存在。 仅当通过调用**SQLSetPos**更新行时才返回 SQL_ROW_ADDED，而不是在另一个游标更新行时返回。  
  
 在数据库中实现动态游标的一种方法是创建一个选择性索引，用于定义结果集的成员资格和排序。 由于在其他人进行更改时更新索引，因此基于此类索引的游标对所有更改都是敏感的。 通过在索引中进行处理，可以在此索引定义的结果集中进行其他选择。  
  
 通过要求按唯一键对结果集进行排序，可以模拟动态游标。 通过此类限制，每次游标提取行时，都会执行**SELECT**语句。 例如，假设此语句定义了结果集：  
  
```  
SELECT * FROM Customers ORDER BY Name, CustID  
```  
  
 若要在此结果集中提取下一个行集，模拟游标会将以下**SELECT**语句中的参数设置为当前行集的最后一行中的值，然后执行它：  
  
```  
SELECT * FROM Customers WHERE (Name > ?) AND (CustID > ?)  
   ORDER BY Name, CustID  
```  
  
 此语句将创建另一个结果集，该结果集是原始结果集中的下一个行集-在本例中，是 Customers 表中的行集。 光标将此行集返回到应用程序。  
  
 值得注意的是，以这种方式实现的动态游标实际上会创建多个结果集，这使它可以检测对原始结果集所做的更改。 应用程序从不了解这些辅助结果集是否存在;它看起来好像游标能够检测到对原始结果集所做的更改。
