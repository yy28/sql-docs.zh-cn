---
title: SQLExtendedFetch （光标库） |Microsoft 文档
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
- SQLExtendedFetch function [ODBC], Cursor Library
ms.assetid: 06fbf06f-127b-475c-b636-7b784918475d
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4e478970e33917202493b194ff2ac2663edde016
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sqlextendedfetch-cursor-library"></a>SQLExtendedFetch （光标库）
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题讨论使用**SQLExtendedFetch**光标库中的函数。 有关常规信息**SQLExtendedFetch**，请参阅[SQLExtendedFetch 函数](../../../odbc/reference/syntax/sqlextendedfetch-function.md)。  
  
 游标库实现**SQLExtendedFetch**通过反复调用**SQLFetch**驱动程序中。  
  
 游标库支持调用**SQLExtendedFetch**与*FetchOrientation* SQL_FETCH_BOOKMARK。  
  
 当使用的是光标库时，调用**SQLExtendedFetch**不能与调用混合**SQLFetchScroll**或**SQLFetch**。
