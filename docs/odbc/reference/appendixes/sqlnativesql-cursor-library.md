---
title: SQLNativeSql （游标库） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLNativeSql function [ODBC], Cursor Library
ms.assetid: c4459092-1177-4b2a-b7f5-e0083d3bf2b2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0a8c42efbd87296cf7157d75d1848e4655247818
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125714"
---
# <a name="sqlnativesql-cursor-library"></a>SQLNativeSql（游标库）
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题介绍如何使用**SQLNativeSql**游标库中的函数。 有关常规信息**SQLNativeSql**，请参阅[SQLNativeSql 函数](../../../odbc/reference/syntax/sqlnativesql-function.md)。  
  
 如果该驱动程序支持此函数，该游标库会调用**SQLNativeSql**驱动程序中并将其传递的 SQL 语句。 对于定位更新，定位删除，并**选择更新**语句，该游标库修改的语句，然后再将它传递给驱动程序。  
  
> [!NOTE]  
>  游标库错误地返回 SQLSTATE 34000 （无效的游标名称），如果游标名称无效中定位的 update 或 delete 语句中传递*InStatementText*自变量的**SQLNativeSql**. **SQLNativeSql**不应返回语法错误，仅在语句的准备或执行时返回。
