---
title: SQLColattributes （dBASE 驱动程序） |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9e9d5adb75a99784d7244852bfda0499e481fc4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307948"
---
# <a name="sqlcolattributes-dbase-driver"></a>SQLColAttributes（dBASE 驱动程序）
> [!NOTE]  
>  本主题提供特定于 dBASE 驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
|特性|注释|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|对于 LONGVARBINARY 数据，SQL_COLUMN_DISPLAY_SIZE是列的最大长度，而不是列乘以 2 的最大长度。|  
|SQL_OWNER_NAME|此列中返回一个空字符串 （""），因为不支持所有者名称。|  
|SQL_QUALIFIER_NAME|返回目录的路径。|  
|SQL_COLUMN_SEARCHABLE|朗瓦里卡和朗瓦尔查尔列报告为SQL_UNSEARCHABLE。<br /><br /> 固定长度和可变长度二进制和字符数据类型是可搜索的，即使 LONGVARBINARY 和 LONGVARCHAR 不。|  
  
> [!NOTE]  
>  上述不是**SQLColAttributes**返回的属性的完整列表。
