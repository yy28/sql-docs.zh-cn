---
title: UPDATE、 DELETE 和 INSERT 语句 |Microsoft 文档
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
ms.topic: article
helpviewer_keywords:
- updating data [ODBC], about updating data
- DELETE [ODBC]
- UPDATE [ODBC]
- INSERT [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 5004ea72-4c49-4064-9752-f7032ba7f133
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1b590f45a6cb7bb3e80b5b52835bd7fd65ba27af
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="update-delete-and-insert-statements"></a>UPDATE、 DELETE 和 INSERT 语句
基于 SQL 的应用程序通过执行对表进行更改**更新**，**删除**，和**插入**语句。 这些语句是最小 SQL 语法一致性级别的一部分，并且必须支持的所有驱动程序和数据源。  
  
 这些语句的语法是：  
  
 **更新***表名称*  
  
 **设置***列标识符* **=** {*表达式* &#124; **NULL**}  
  
 [**，** *列标识符* **=** {*表达式* &#124; **NULL**}]...  
  
 [**其中***搜索条件*]  
  
 **DELETE FROM** *表名*[**其中***搜索条件*]  
  
 **INSERT INTO** *表名*[**(* * * 列标识符*[* *，** *列标识符*]...**)**]  
  
 {*查询规范* &#124; **值 (***插入值* [**，** *插入值*]...**)**}  
  
 请注意，*查询规范*元素是仅在核心和扩展 SQL 语法中，且中有效*表达式*和*搜索条件*元素变得更核心和扩展 SQL 语法中的复杂。  
  
 像其他 SQL 语句，请**更新**，**删除**，和**插入**语句通常是更多在使用参数时有效。 例如，下面的语句可以准备并重复执行，以在订单表中插入多个行：  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 传递的参数值的数组可以增加此效率。 有关语句参数和参数值的数组的详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。
