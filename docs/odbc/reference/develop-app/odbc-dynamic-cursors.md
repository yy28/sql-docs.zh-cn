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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 64215cff750e39dc78ad1a695bbe553d900f4120
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52541866"
---
# <a name="odbc-dynamic-cursors"></a>ODBC 动态游标
动态游标只是： 动态。 它可以检测到的成员身份、 顺序和结果集打开游标后的值所做的任何更改。 例如，假设动态游标提取两个行，另一个应用程序，然后更新这些行之一并删除其他。 如果动态游标然后尝试重新提取这些行，它将找不到已删除的行，但将返回已更新的行的新值。  
  
 动态游标检测所有更新，删除和插入，同时其自己和所做的其他人。 （这是受限于隔离级别事务由 SQL_ATTR_TXN_ISOLATION 连接属性设置。）将 SQL_ATTR_ROW_STATUS_PTR 语句属性指定的行状态数组反映这些更改，并且可以包含 SQL_ROW_SUCCESS、 SQL_ROW_SUCCESS_WITH_INFO、 SQL_ROW_ERROR、 SQL_ROW_UPDATED 和 SQL_ROW_ADDED。 因为动态游标不会返回外部行集已删除的行，因此不再能识别的结果集中已删除的行或行状态数组中的对应元素存在，它不能返回 SQL_ROW_DELETED。 仅当通过调用更新了某行时返回 SQL_ROW_ADDED **SQLSetPos**、 不是在另一个游标更新时。  
  
 在数据库中实现动态游标的一种方法通过创建定义成员资格的选择性索引和排序结果的设置。 因为索引会更新其他人进行更改时，基于此类索引游标是敏感的所有更改。 可以通过沿索引的处理过程中定义此索引的结果集的其他选择。  
  
 动态游标可以模拟通过要求的结果集的唯一键进行排序。 此类限制，提取操作都通过执行**选择**语句每次该游标提取行。 例如，假设此语句定义结果集：  
  
```  
SELECT * FROM Customers ORDER BY Name, CustID  
```  
  
 若要提取此结果集中的下一个行集，模拟的游标设置的参数在下面的示例**选择**语句中的当前行集的最后一行的值，然后执行它：  
  
```  
SELECT * FROM Customers WHERE (Name > ?) AND (CustID > ?)  
   ORDER BY Name, CustID  
```  
  
 此语句在客户表中创建第二个结果集，第一个行集的原始结果集中的下一步的行集在这种情况下，行集。 将光标返回到应用程序如下行集。  
  
 有趣的是要注意这种方式实现的动态游标实际创建多个结果集，这使得它能够检测到原始的结果集的更改。 应用程序永远不会发现这些辅助结果集; 存在只需将显示如如果光标位于能够检测到对原始结果集进行更改。
