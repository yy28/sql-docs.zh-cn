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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125714"
---
# <a name="sqlnativesql-cursor-library"></a>SQLNativeSql（游标库）
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题讨论如何在游标库中使用**SQLNativeSql**函数。 有关**SQLNativeSql**的常规信息，请参阅[SQLNativeSql 函数](../../../odbc/reference/syntax/sqlnativesql-function.md)。  
  
 如果驱动程序支持此函数，则游标库在驱动程序中调用**SQLNativeSql** ，并向其传递 SQL 语句。 对于定位更新、定位 delete 和**SELECT FOR update**语句，游标库会在将其传递给驱动程序之前修改语句。  
  
> [!NOTE]  
>  如果在**SQLNativeSql**的*InStatementText*参数中传递了定位的 update 或 delete 语句中的游标名称无效，则游标库将错误地返回 SQLSTATE 34000 （无效的游标名称）。 **SQLNativeSql**不打算返回语法错误，这些错误仅在语句准备或执行时返回。
