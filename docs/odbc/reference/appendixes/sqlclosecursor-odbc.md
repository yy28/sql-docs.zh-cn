---
title: SQLCloseCursor_ODBC |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLCloseCursor function [ODBC], ODBC
ms.assetid: 5e47e3f7-e1b8-451f-bf75-daa19b7c7271
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e1b61267d093e11bf7ea25158f5dc6a29ccba6a1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296297"
---
# <a name="sqlclosecursor_odbc"></a>SQLCloseCursor_ODBC
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。  
  
 本主题讨论在游标库中使用**SQLCloseCursor**函数。 有关**SQLCloseCursor 的**一般信息，请参阅[SQLCloseCursor 函数](../../../odbc/reference/syntax/sqlclosecursor-function.md)。  
  
 没有打开的游标，游标库不支持调用**SQLCloseCursor。** 尝试此将返回 SQLSTATE 24000（无效游标状态）。 在未打开游标时，使用SQL_CLOSE*选项*调用**SQLFreeStmt，** 光标库支持。
