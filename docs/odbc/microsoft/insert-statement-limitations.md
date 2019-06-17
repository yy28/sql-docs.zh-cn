---
title: INSERT 语句限制 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26d4be96ca4dabebd93ee96e2888e18d39257412
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62471822"
---
# <a name="insert-statement-limitations"></a>INSERT 语句限制
插入的数据进行截断而不发出警告右侧太长，无法适应列。  
  
 尝试插入不在范围内的列的数据类型的值会导致 NULL 插入列。  
  
 当使用 dBASE、 Microsoft Excel、 Paradox 或 Textdriver 时，将插入列的长度为零的字符串实际上将插入 NULL 改为。  
  
 使用 Microsoft Excel 驱动程序时，如果为空字符串插入到的列，则为空字符串转换为 NULL;使用空字符串的 WHERE 子句中执行的搜索选择语句将不会在该列上成功。  
  
 该表不能在两种情况下 Paradox 驱动程序更新：  
  
-   当未对表定义唯一索引。 这不是为一个空表，它可以更新与单一行，即使未对表定义唯一索引，则返回 true。 如果不具有唯一索引的空表中插入单个行，则应用程序不能创建唯一索引，或在插入单个行后插入其他数据。  
  
-   如果未实现 borland 公司数据库引擎，只读取和追加 Paradox 表上允许语句。  
  
 使用文本驱动程序时，NULL 值都是固定长度的文件中的填补空白的字符串，但没有空格分隔的文件中表示。 例如，在包含三个字段的以下行，第二个字段是一个 NULL 值：  
  
```  
"Smith:,, 123  
```  
  
 使用文本驱动程序时，可以用前导空格填充所有列的值。 任何行的长度必须小于或等于 65,543 字节。
