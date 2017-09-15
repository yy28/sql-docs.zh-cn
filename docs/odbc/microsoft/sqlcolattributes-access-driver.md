---
title: "SQLColAttributes （Access 驱动程序） |Microsoft 文档"
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
- SQLColAttribute function [ODBC], Access Driver
- Access driver [ODBC], SQLColAttributes
ms.assetid: adb6f81d-e8c7-4748-9b1d-f7a053788bbc
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e2531bbc58e55c3c58452701f1dd66ac6702a535
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlcolattributes-access-driver"></a>SQLColAttributes （Access 驱动程序）
> [!NOTE]  
>  本主题提供访问特定于驱动程序信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|Attribute|注释|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|对于 LONGVARBINARY 数据，SQL_COLUMN_DISPLAY_SIZE 是列中，不时间 2 列的最大长度的最大长度。|  
|SQL_OWNER_NAME|空字符串 ("") 因为所有者名称不支持在此列中返回。|  
|SQL_QUALIFIER_NAME|返回数据库文件的路径。|  
|SQL_COLUMN_SEARCHABLE|LONGVARBINARY 和 LONGVARCHAR 列被报告为 SQL_UNSEARCHABLE。<br /><br /> 固定长度和可变长度的二进制和字符数据类型是可搜索，即使 LONGVARBINARY 和 LONGVARCHAR 不是。|  
  
> [!NOTE]  
>  上述是不返回的属性的完整列表**SQLColAttributes**。
