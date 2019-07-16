---
title: SQLColAttributes （Access 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], Access Driver
- Access driver [ODBC], SQLColAttributes
ms.assetid: adb6f81d-e8c7-4748-9b1d-f7a053788bbc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0c78229da8a577670ba31ae82c679bfefbef4f80
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67903983"
---
# <a name="sqlcolattributes-access-driver"></a>SQLColAttributes（Access 驱动程序）
> [!NOTE]  
>  本主题提供访问特定于驱动程序信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|特性|注释|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|对于 LONGVARBINARY 数据 SQL_COLUMN_DISPLAY_SIZE 是列，不乘以 2 列的最大长度的最大长度。|  
|SQL_OWNER_NAME|空字符串 ("") 因为所有者名称不支持此列中返回。|  
|SQL_QUALIFIER_NAME|返回数据库文件的路径。|  
|SQL_COLUMN_SEARCHABLE|LONGVARBINARY 和 LONGVARCHAR 列均报告为 SQL_UNSEARCHABLE。<br /><br /> 固定长度和可变长度二进制和字符数据类型是可搜索，即使 LONGVARBINARY 和 LONGVARCHAR 不是。|  
  
> [!NOTE]  
>  上述不是返回的属性的完整列表**SQLColAttributes**。
