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
ms.openlocfilehash: 92fb7b0e9722c52c7f1e9fc071d434f531b2fc46
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47721905"
---
# <a name="update-delete-and-insert-statements"></a>UPDATE、DELETE 和 INSERT 语句
基于 SQL 的应用程序通过执行对表进行更改**更新**，**删除**，并**插入**语句。 这些语句是最小 SQL 语法的一致性级别的一部分，必须支持的所有驱动程序和数据源。  
  
 这些语句的语法是：  
  
 **更新***表名称*   
  
 **设置***列标识符* **=** {*表达式* &#124; **NULL**}  
  
 [**，** *列标识符* **=** {*表达式* &#124; **NULL**}]...  
  
 [**其中***搜索条件*]  
  
 **DELETE FROM** *l e-n*[**其中***搜索条件*]  
  
 **INSERT INTO** *l e-n*[**(* * * 列标识符*[* *，** *列标识符*]...**)**]  
  
 {*查询规范* &#124; **值 (***插入值* [**，** *插入值*]...**)**}  
  
 请注意，*查询规范*元素是仅在核心应用程序和扩展 SQL 语法和的中有效*表达式*并*搜索条件*元素变得更在核心应用程序和扩展 SQL 语法中复杂。  
  
 像其他 SQL 语句，请**更新**，**删除**，并**插入**语句是极具在使用参数时有效。 例如，下面的语句可以准备并重复执行订单表中插入多个行：  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 通过传递参数值的数组，可以增加此效率。 有关语句参数和参数值的数组的详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。
