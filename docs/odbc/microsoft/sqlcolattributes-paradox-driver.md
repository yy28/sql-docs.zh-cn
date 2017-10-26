---
title: "SQLColAttributes （Paradox 驱动程序） |Microsoft 文档"
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
- SQLColAttribute function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLColAttributes
ms.assetid: bbeef024-d470-4d28-b61b-26997ef41007
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 414ad2afeb627b413ecfc3ee166f694813e2676a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlcolattributes-paradox-driver"></a>SQLColAttributes （Paradox 驱动程序）
> [!NOTE]  
>  本主题提供 Paradox 特定于驱动程序信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|Attribute|注释|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|对于 LONGVARBINARY 数据，SQL_COLUMN_DISPLAY_SIZE 是列中，不时间 2 列的最大长度的最大长度。|  
|SQL_OWNER_NAME|空字符串 ("") 因为所有者名称不支持在此列中返回。|  
|SQL_QUALIFIER_NAME|返回到目录的路径。|  
|SQL_COLUMN_SEARCHABLE|LONGVARBINARY 和 LONGVARCHAR 列被报告为 SQL_UNSEARCHABLE。<br /><br /> 固定长度和可变长度的二进制和字符数据类型是可搜索，即使 LONGVARBINARY 和 LONGVARCHAR 不是。|  
  
> [!NOTE]  
>  上述是不返回的属性的完整列表**SQLColAttributes**。

