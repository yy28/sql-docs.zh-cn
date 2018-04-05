---
title: SQLNativeSql （光标库） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
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
- SQLNativeSql function [ODBC], Cursor Library
ms.assetid: c4459092-1177-4b2a-b7f5-e0083d3bf2b2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a2bd3fd6851cd3d59187a239d7d6aad2ffd269ac
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sqlnativesql-cursor-library"></a>SQLNativeSql （光标库）
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题讨论使用**SQLNativeSql**光标库中的函数。 有关常规信息**SQLNativeSql**，请参阅[SQLNativeSql 函数](../../../odbc/reference/syntax/sqlnativesql-function.md)。  
  
 游标库的驱动程序支持此函数，如果调用**SQLNativeSql**驱动程序中并将其传递的 SQL 语句。 对于定位更新，定位 delete 和**选择更新**语句，光标库修改的语句，然后再将它传递到该驱动程序。  
  
> [!NOTE]  
>  游标库错误地返回 SQLSTATE 34000 （无效的临时表名称），如果游标名称无效定位的 update 或 delete 语句中传递中*InStatementText*参数**SQLNativeSql**. **SQLNativeSql**不是要返回语法错误，仅在语句准备或执行时返回。
