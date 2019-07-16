---
title: SQLSetScrollOptions （游标库） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Cursor Library
ms.assetid: c5c0ac6d-a6c1-4077-8186-1644df1944f8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 18a0bc111f6b4e8d82d0ed353837b499f920479e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023358"
---
# <a name="sqlsetscrolloptions-cursor-library"></a>SQLSetScrollOptions（游标库）
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题介绍如何使用**SQLSetScrollOptions**游标库中的函数。 有关常规信息**SQLSetScrollOptions**，请参阅[SQLSetScrollOptions 函数](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)。  
  
 游标库支持**SQLSetScrollOptions**仅为了向后兼容; 应用程序应改用 SQL_ATTR_CONCURRENCY、 SQL_ATTR_CURSOR_TYPE 和 SQL_ATTR_ROW_ARRAY_SIZE 语句属性。
