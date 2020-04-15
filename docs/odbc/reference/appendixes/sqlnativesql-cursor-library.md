---
title: SQLNativeSql（光标库） |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 41f7617530f34d49852ca67db9f47cab94292385
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300567"
---
# <a name="sqlnativesql-cursor-library"></a>SQLNativeSql（游标库）
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。  
  
 本主题讨论在游标库中使用**SQLNativeSql**函数。 有关**SQLNativeSql**的一般信息，请参阅[SQLNativeSql 函数](../../../odbc/reference/syntax/sqlnativesql-function.md)。  
  
 如果驱动程序支持此功能，光标库将在驱动程序中调用**SQLNativeSql**并将其传递给 SQL 语句。 对于定位更新、定位删除和**选择更新**语句，光标库在将语句传递给驱动程序之前修改该语句。  
  
> [!NOTE]  
>  如果游标名称在**SQLNativeSql**的*InofText*参数中传递的定位更新或删除语句中无效，则游标库错误地返回 SQLSTATE 34000（无效游标名称）。 **SQLNativeSql**不打算返回语法错误，这些错误仅在语句准备或执行时返回。
