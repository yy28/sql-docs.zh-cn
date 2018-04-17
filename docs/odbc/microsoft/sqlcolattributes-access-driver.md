---
title: SQLColAttributes （Access 驱动程序） |Microsoft 文档
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
- SQLColAttribute function [ODBC], Access Driver
- Access driver [ODBC], SQLColAttributes
ms.assetid: adb6f81d-e8c7-4748-9b1d-f7a053788bbc
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9e49f15f74ff10311c5e3d2215ff99761c7afb5d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
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
