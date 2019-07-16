---
title: SQLExtendedFetch （游标库） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExtendedFetch function [ODBC], Cursor Library
ms.assetid: 06fbf06f-127b-475c-b636-7b784918475d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a3fd7d02d74b0e19d91871c5df7c9c5915d028f5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064453"
---
# <a name="sqlextendedfetch-cursor-library"></a>SQLExtendedFetch（游标库）
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题介绍如何使用**SQLExtendedFetch**游标库中的函数。 有关常规信息**SQLExtendedFetch**，请参阅[SQLExtendedFetch 函数](../../../odbc/reference/syntax/sqlextendedfetch-function.md)。  
  
 游标库实现**SQLExtendedFetch**通过反复调用**SQLFetch**驱动程序中。  
  
 游标库支持调用**SQLExtendedFetch**与*FetchOrientation*的 SQL_FETCH_BOOKMARK。  
  
 当使用游标库时，调用**SQLExtendedFetch**不能在其中调用**SQLFetchScroll**或**SQLFetch**。
