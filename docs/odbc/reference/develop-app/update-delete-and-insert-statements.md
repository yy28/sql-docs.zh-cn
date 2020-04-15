---
title: 更新、删除和插入语句 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f12682a5d012d6981afce0085e9c920ed2f2ffbc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284257"
---
# <a name="update-delete-and-insert-statements"></a>UPDATE、DELETE 和 INSERT 语句
基于 SQL 的应用程序通过执行**更新**、**删除**和**INSERT**语句对表进行更改。 这些语句是最小 SQL 语法一致性级别的一部分，必须得到所有驱动程序和数据源的支持。  
  
 这些语句的语法是：  
  
 **更新**_表名称_  
  
 **设置**_列标识符_**=**= &#124; **NULL**的*表达式*|  
  
 [**，**_列标识符_**=**]*表达式*&#124; **NULL**_...  
  
 [**WHERE** _搜索条件_]  
  
 **从**_表名中删除_[**WHERE** _搜索条件_]  
  
 **插入表**_名_=**（**_列标识符_=**，** _列标识符_* ...**)**]  
  
 [*查询规范*&#124;**值 （**_插入值_#**，** _插入值_# ...**)**}  
  
 请注意，*查询规范*元素仅在核心和扩展 SQL 语法中有效，并且*表达式*和*搜索条件*元素在核心和扩展 SQL 语法中变得更加复杂。  
  
 与其他 SQL 语句一样，**更新**、**删除**和**INSERT**语句在使用参数时通常更有效率。 例如，可以准备并重复执行以下语句，以在"订单"表中插入多行：  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 通过传递参数值数组可以提高这种效率。 有关语句参数和参数值数组的详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。
