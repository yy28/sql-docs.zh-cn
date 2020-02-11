---
title: SQLColAttributes （dBASE 驱动程序） |Microsoft Docs
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
ms.openlocfilehash: 66a37f3c9ceccdf3fb226ea423552886d36ed99f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67903974"
---
# <a name="sqlcolattributes-dbase-driver"></a>SQLColAttributes（dBASE 驱动程序）
> [!NOTE]  
>  本主题提供了特定于 dBASE 驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
|Attribute|注释|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|对于 LONGVARBINARY 数据，SQL_COLUMN_DISPLAY_SIZE 是列的最大长度，而不是列的最大长度2。|  
|SQL_OWNER_NAME|此列中返回空字符串（""），因为不支持所有者名称。|  
|SQL_QUALIFIER_NAME|返回目录的路径。|  
|SQL_COLUMN_SEARCHABLE|LONGVARBINARY 和 LONGVARCHAR 列将报告为 SQL_UNSEARCHABLE。<br /><br /> 固定长度和可变长度的二进制和字符数据类型都是可搜索的，即使 LONGVARBINARY 和 LONGVARCHAR 不是如此。|  
  
> [!NOTE]  
>  以上不是**SQLColAttributes**返回的属性的完整列表。
