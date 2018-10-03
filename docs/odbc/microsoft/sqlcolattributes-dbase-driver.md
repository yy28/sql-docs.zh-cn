---
title: SQLColAttributes (dBASE 驱动程序) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLColAttributes
ms.assetid: ed44de2b-0b01-4dce-a340-f5eb3aac30b7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 56d6a7cb3c2c071191a956c6aaf11479810698f8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47619615"
---
# <a name="sqlcolattributes-dbase-driver"></a>SQLColAttributes（dBASE 驱动程序）
> [!NOTE]  
>  本主题提供 dBASE 驱动程序特定信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|Attribute|注释|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|对于 LONGVARBINARY 数据 SQL_COLUMN_DISPLAY_SIZE 是列，不乘以 2 列的最大长度的最大长度。|  
|SQL_OWNER_NAME|空字符串 ("") 因为所有者名称不支持此列中返回。|  
|SQL_QUALIFIER_NAME|返回到目录的路径。|  
|SQL_COLUMN_SEARCHABLE|LONGVARBINARY 和 LONGVARCHAR 列均报告为 SQL_UNSEARCHABLE。<br /><br /> 固定长度和可变长度二进制和字符数据类型是可搜索，即使 LONGVARBINARY 和 LONGVARCHAR 不是。|  
  
> [!NOTE]  
>  上述不是返回的属性的完整列表**SQLColAttributes**。
