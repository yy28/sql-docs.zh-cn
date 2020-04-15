---
title: SQLColattributes（Excel 驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLColAttributes
- SQLColAttribute function [ODBC], Excel Driver
ms.assetid: 7c4833e3-ff0c-4313-9ab8-21379ceab656
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 218c442af6292b665764ed60dc5586710d820de6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307938"
---
# <a name="sqlcolattributes-excel-driver"></a>SQLColAttributes（Excel 驱动程序）
> [!NOTE]  
>  本主题提供特定于 Excel 驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
|特性|注释|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|对于 LONGVARBINARY 数据，SQL_COLUMN_DISPLAY_SIZE是列的最大长度，而不是列乘以 2 的最大长度。|  
|SQL_OWNER_NAME|此列中返回一个空字符串 （""），因为不支持所有者名称。|  
|SQL_QUALIFIER_NAME|返回目录的路径。|  
|SQL_COLUMN_SEARCHABLE|朗瓦里卡和朗瓦尔查尔列报告为SQL_UNSEARCHABLE。<br /><br /> 固定长度和可变长度二进制和字符数据类型是可搜索的，即使 LONGVARBINARY 和 LONGVARCHAR 不。|  
  
> [!NOTE]  
>  上述不是**SQLColAttributes**返回的属性的完整列表。
