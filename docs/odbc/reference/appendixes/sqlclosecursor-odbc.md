---
title: "SQLCloseCursor_ODBC |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLCloseCursor function [ODBC], ODBC
ms.assetid: 5e47e3f7-e1b8-451f-bf75-daa19b7c7271
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fcc680ec815afa700c00c9d8a69c5826944153a4
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlclosecursorodbc"></a>SQLCloseCursor_ODBC
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题讨论使用**SQLCloseCursor**光标库中的函数。 有关常规信息**SQLCloseCursor**，请参阅[SQLCloseCursor 函数](../../../odbc/reference/syntax/sqlclosecursor-function.md)。  
  
 游标库不支持调用**SQLCloseCursor**而无需打开的游标。 尝试这将返回 SQLSTATE 24000 （无效的游标状态）。 调用**SQLFreeStmt**与*选项*SQL_CLOSE 的任何光标时打开受游标库。

