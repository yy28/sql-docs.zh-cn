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
manager: craigg
ms.openlocfilehash: e1fe6765c0ff8a057aac8e86ea5ad4aa1ac388b4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47739665"
---
# <a name="sqlsetscrolloptions-cursor-library"></a>SQLSetScrollOptions（游标库）
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题介绍如何使用**SQLSetScrollOptions**游标库中的函数。 有关常规信息**SQLSetScrollOptions**，请参阅[SQLSetScrollOptions 函数](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)。  
  
 游标库支持**SQLSetScrollOptions**仅为了向后兼容; 应用程序应改用 SQL_ATTR_CONCURRENCY、 SQL_ATTR_CURSOR_TYPE 和 SQL_ATTR_ROW_ARRAY_SIZE 语句属性。
