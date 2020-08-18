---
description: SQLSetScrollOptions（游标库）
title: SQLSetScrollOptions (游标库) |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f40e5cd3b62b91b1b0b832b9b8fcf36101487c10
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386553"
---
# <a name="sqlsetscrolloptions-cursor-library"></a>SQLSetScrollOptions（游标库）
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题讨论如何在游标库中使用 **SQLSetScrollOptions** 函数。 有关 **SQLSetScrollOptions**的常规信息，请参阅 [SQLSetScrollOptions 函数](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)。  
  
 游标库仅支持 **SQLSetScrollOptions** ，以实现向后兼容;应用程序应改为使用 SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE 和 SQL_ATTR_ROW_ARRAY_SIZE 语句特性。
