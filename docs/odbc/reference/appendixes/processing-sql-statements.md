---
title: 处理 SQL 语句 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], statement processing
- SQL statements [ODBC], cursor library
- cursor library [ODBC], statement processing
ms.assetid: 54dad6a3-e86c-477b-ba7c-4e95e0385ec1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5d5aa94062f90154126fb18c3658adb39bb1d5c0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63057042"
---
# <a name="processing-sql-statements"></a>处理 SQL 语句
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 ODBC 游标库的所有 SQL 语句将直接都传递到除以下驱动程序：  
  
-   定位 update 和 delete 语句  
  
-   **SELECT FOR UPDATE**语句  
  
-   批处理的 SQL 语句  
  
 若要执行定位的更新和删除语句并将光标置于行以调用**SQLGetData**该行，游标库构造搜索的语句，标识的行。  
  
 本部分包含以下主题。  
  
-   [处理定位更新和删除语句](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)  
  
-   [处理 SELECT FOR UPDATE 语句](../../../odbc/reference/appendixes/processing-select-for-update-statements.md)  
  
-   [批处理 SQL 语句](../../../odbc/reference/appendixes/processing-batches-of-sql-statements.md)  
  
-   [构造搜索语句](../../../odbc/reference/appendixes/constructing-searched-statements.md)
