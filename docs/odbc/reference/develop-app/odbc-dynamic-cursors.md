---
title: ODBC动态光标 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302319"
---
# <a name="odbc-dynamic-cursors"></a>ODBC 动态游标
动态光标就是：动态。 它可以检测打开游标后对结果集的成员身份、顺序和值所做的任何更改。 例如，假设动态游标提取两行，然后另一个应用程序将更新这两行之一并删除另一行。 如果动态游标然后尝试重新提取这些行，它将找不到已删除的行，但将返回更新行的新值。  
  
 动态游标检测所有更新、删除和插入，包括它们自己和他人所做的更新。 （这受事务的隔离级别的约束，由SQL_ATTR_TXN_ISOLATION连接属性设置。SQL_ATTR_ROW_STATUS_PTR语句属性指定的行状态数组反映这些更改，可以包含SQL_ROW_SUCCESS、SQL_ROW_SUCCESS_WITH_INFO、SQL_ROW_ERROR、SQL_ROW_UPDATED和SQL_ROW_ADDED。 它不能返回SQL_ROW_DELETED，因为动态游标不会返回行集外的已删除行，因此不再识别结果集中的已删除行或其相应元素在行状态数组中是否存在。 仅当对**SQLSetPos**的调用更新行时，才会返回SQL_ROW_ADDED，而不是由另一个游标更新时返回该行。  
  
 在数据库中实现动态游标的一种方法是创建一个选择性索引，用于定义结果集的成员身份和顺序。 由于当其他人进行更改时，索引会更新，因此基于此类索引的游标对所有更改都敏感。 通过沿索引处理，可以在此索引定义的结果集中进行其他选择。  
  
 可以通过要求由唯一键排序结果集来模拟动态游标。 在此类限制下，每次游标获取行时，都会通过执行**SELECT**语句进行提取。 例如，假设结果集由以下语句定义：  
  
```  
SELECT * FROM Customers ORDER BY Name, CustID  
```  
  
 要获取此结果集中的下一个行集，模拟游标将以下**SELECT**语句中的参数设置为当前行集最后一行中的值，然后执行它：  
  
```  
SELECT * FROM Customers WHERE (Name > ?) AND (CustID > ?)  
   ORDER BY Name, CustID  
```  
  
 此语句创建第二个结果集，其中第一个行集是原始结果集中的下一个行集 -在这种情况下，是客户表中的行集。 光标将此行集返回到应用程序。  
  
 值得注意的是，以这种方式实现的动态游标实际上创建了许多结果集，从而可以检测对原始结果集的更改。 应用程序从不了解这些辅助结果集的存在;它只是显示，如果光标能够检测对原始结果集的更改。
