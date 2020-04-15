---
title: 插入语句限制 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, INSERT statement limitations
- INSERT statement limitations [ODBC]
- truncation of data [ODBC]
ms.assetid: dea05698-527a-41ab-8729-bbed85556185
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f903f15ec13baa28a789891c1527dc742daa68ac
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299998"
---
# <a name="insert-statement-limitations"></a>INSERT 语句限制
如果插入的数据太长，无法放入列，则在右侧截断数据，恕不另行通知。  
  
 尝试插入列数据类型范围外的值会导致将 NULL 插入到列中。  
  
 当使用 dBASE、Microsoft Excel、悖论或文本驱动程序时，将零长度字符串插入列实际上插入 NULL。  
  
 使用 Microsoft Excel 驱动程序时，如果将空字符串插入到列中，则空字符串将转换为 NULL;如果将空字符串插入到列中，则将空字符串转换为 NULL。使用 WHERE 子句中的空字符串执行的搜索 SELECT 语句将不会在该列上成功。  
  
 在以下两个条件下，悖论驱动程序无法启动表：  
  
-   未在表上定义唯一索引时。 对于空表，情况并非如此，即使表上未定义唯一索引，也可以用单个行进行更新。 如果单行插入于没有唯一索引的空表中，则应用程序无法创建唯一索引或在插入单行后插入其他数据。  
  
-   如果未实现 Borland 数据库引擎，则仅允许在 Paradox 表上读取和追加语句。  
  
 使用 Text 驱动程序时，NULL 值由固定长度文件中的空白填充字符串表示，但由分隔文件中的空格表示。 例如，在包含三个字段的行中，第二个字段是 NULL 值：  
  
```  
"Smith:,, 123  
```  
  
 使用文本驱动程序时，可以使用前导空格填充所有列值。 任何行的长度必须小于或等于 65，543 字节。
