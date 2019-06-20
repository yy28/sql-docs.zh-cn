---
title: UPDATE、 DELETE 和 INSERT 语句 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], about updating data
- DELETE [ODBC]
- UPDATE [ODBC]
- INSERT [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 5004ea72-4c49-4064-9752-f7032ba7f133
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 00732de7eca32dc8b2984fdda14163c77c66ad43
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62632475"
---
# <a name="update-delete-and-insert-statements"></a>UPDATE、DELETE 和 INSERT 语句
基于 SQL 的应用程序通过执行对表进行更改**更新**，**删除**，并**插入**语句。 这些语句是最小 SQL 语法的一致性级别的一部分，必须支持的所有驱动程序和数据源。  
  
 这些语句的语法是：  
  
 **更新** _表名称_  
  
 **SET** _column-identifier_ **=** {*expression* &#124; **NULL**}  
  
 [ **,** _column-identifier_ **=** {*expression* &#124; **NULL**}]...  
  
 [**WHERE** _search-condition_]  
  
 **DELETE FROM** _table-name_[**WHERE** _search-condition_]  
  
 **INSERT INTO** _table-name_[ **(** _column-identifier_ [ **,** _column-identifier_]... **)** ]  
  
 {*query-specification* &#124; **VALUES (** _insert-value_ [ **,** _insert-value_]... **)** }  
  
 请注意，*查询规范*元素是仅在核心应用程序和扩展 SQL 语法和的中有效*表达式*并*搜索条件*元素变得更在核心应用程序和扩展 SQL 语法中复杂。  
  
 像其他 SQL 语句，请**更新**，**删除**，并**插入**语句是极具在使用参数时有效。 例如，下面的语句可以准备并重复执行订单表中插入多个行：  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 通过传递参数值的数组，可以增加此效率。 有关语句参数和参数值的数组的详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。
