---
title: "INSERT 语句限制 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC SQL grammar, INSERT statement limitations
- INSERT statement limitations [ODBC]
- truncation of data [ODBC]
ms.assetid: dea05698-527a-41ab-8729-bbed85556185
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f9233e7582083ba08fb1239120e63db819b8724b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="insert-statement-limitations"></a>插入语句的限制
如果太长，无法适应列，而不发出警告右侧截断插入的数据。  
  
 尝试插入一个值，超出的列的数据类型范围会导致 NULL 插入到列。  
  
 当使用 dBASE、 Microsoft Excel、 Paradox 或 Textdriver 时，将一个零长度字符串插入列实际上将插入 NULL 改为。  
  
 当使用 Microsoft Excel 驱动程序时，如果列中插入一个空字符串时，将空字符串转换为 NULL;使用空字符串的 WHERE 子句中执行的搜索 SELECT 语句将对该列不会成功。  
  
 表不可更新由两个条件下 Paradox 驱动程序：  
  
-   当表上未定义唯一索引。 不能为一个空表，它可以更新与单个行中，即使唯一索引未定义表上同时运行。 如果在没有唯一索引的空表中插入一行，应用程序无法创建唯一索引或在插入单个行后插入其他数据。  
  
-   如果未实现高数据库引擎，仅读取和追加 Paradox 表上允许语句。  
  
 使用文本驱动程序时，NULL 值将由在固定长度的文件，填补空白的字符串表示，但没有空格分隔的文件中表示。 例如，在以下行中包含三个字段，第二个字段为 NULL 值：  
  
```  
"Smith:,, 123  
```  
  
 当使用文本驱动程序时，可以用前导空格填充所有列的值。 任何行的长度必须小于或等于 65,543 字节。
