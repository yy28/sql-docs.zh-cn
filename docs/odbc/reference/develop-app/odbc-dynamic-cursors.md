---
title: "ODBC 动态游标 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursors [ODBC], dynamic
- dynamic cursors [ODBC]
ms.assetid: de709fd3-9eb2-44e1-a2f0-786e2b9602a6
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5b5d294aaeebab45e0ff0ce36db0fa39b9738571
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="odbc-dynamic-cursors"></a>ODBC 动态游标
动态游标就是： 动态。 它可以检测到成员资格、 顺序和值的结果集打开光标后所做的任何更改。 例如，假设动态游标提取两行，另一个应用程序，然后更新这些行之一并删除其他。 如果动态游标然后尝试重新提取这些行，它不会查找删除的行，但会返回更新的行的新值。  
  
 动态游标检测所有更新，删除和插入，同时其自己和其他人所做的那些。 （这由提供的隔离级别的事务，如所 SQL_ATTR_TXN_ISOLATION 连接属性设置。）SQL_ATTR_ROW_STATUS_PTR 语句属性指定的行状态数组反映这些更改，并且可以包含 SQL_ROW_SUCCESS、 SQL_ROW_SUCCESS_WITH_INFO、 SQL_ROW_ERROR、 SQL_ROW_UPDATED 和 SQL_ROW_ADDED。 因为动态游标不返回行集以外的已删除的行，并因此不再识别的结果集中删除的行或行状态数组中的对应元素存在，它不能返回 SQL_ROW_DELETED。 仅当通过调用更新了某行时，才返回 SQL_ROW_ADDED **SQLSetPos**、 不是在由另一个游标更新时。  
  
 在数据库中实施动态游标的一种方法通过创建一个选择性索引，它定义的成员资格和排序结果的设置。 由于索引也将更新其他人在更改时，此类索引所基于的游标的更改比较敏感所有。 在结果集中定义的此索引的其他选择是可以通过处理沿索引。  
  
 可以通过要求集由唯一键进行排序的结果模拟动态游标。 包含此类限制，提取都通过执行**选择**语句游标提取行每次。 例如，假设由此语句定义结果集：  
  
```  
SELECT * FROM Customers ORDER BY Name, CustID  
```  
  
 若要提取此结果集中的下一步的行集，模拟的光标设置的参数在下面的示例**选择**语句中的当前行集的最后一行的值，然后执行：  
  
```  
SELECT * FROM Customers WHERE (Name > ?) AND (CustID > ?)  
   ORDER BY Name, CustID  
```  
  
 此语句将创建第二个结果集，其中第一个行集是原始结果集中的下一步的行集-在此情况下，客户表中的行集。 光标返回到应用程序的下一个行集合。  
  
 有趣的是需要注意这种方式实现的动态游标实际创建多个结果集，这使得它能够检测到原始的结果集的更改。 应用程序永远不会了解这些辅助结果集; 存在它只需显示光标就像是能够检测到对原始结果集的更改。
