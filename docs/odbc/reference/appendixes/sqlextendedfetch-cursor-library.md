---
title: SQLExtendedFetch （光标库） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLExtendedFetch function [ODBC], Cursor Library
ms.assetid: 06fbf06f-127b-475c-b636-7b784918475d
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 08fa807fcbfd3c55df7edcc221131479edee3e0b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlextendedfetch-cursor-library"></a>SQLExtendedFetch （光标库）
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题讨论使用**SQLExtendedFetch**光标库中的函数。 有关常规信息**SQLExtendedFetch**，请参阅[SQLExtendedFetch 函数](../../../odbc/reference/syntax/sqlextendedfetch-function.md)。  
  
 游标库实现**SQLExtendedFetch**通过反复调用**SQLFetch**驱动程序中。  
  
 游标库支持调用**SQLExtendedFetch**与*FetchOrientation* SQL_FETCH_BOOKMARK。  
  
 当使用的是光标库时，调用**SQLExtendedFetch**不能与调用混合**SQLFetchScroll**或**SQLFetch**。
