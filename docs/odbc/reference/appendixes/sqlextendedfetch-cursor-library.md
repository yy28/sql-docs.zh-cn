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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe39b2d2cbbaf72ce3844c35187040589d1dac58
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302058"
---
# <a name="sqlextendedfetch-cursor-library"></a>SQLExtendedFetch（游标库）
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题讨论如何在游标库中使用**SQLExtendedFetch**函数。 有关**SQLExtendedFetch**的常规信息，请参阅[SQLExtendedFetch 函数](../../../odbc/reference/syntax/sqlextendedfetch-function.md)。  
  
 游标库通过在驱动程序中重复调用**SQLFetch**来实现**SQLExtendedFetch** 。  
  
 游标库支持使用 SQL_FETCH_BOOKMARK 的*FetchOrientation*调用**SQLExtendedFetch** 。  
  
 使用游标库时，对**SQLExtendedFetch**的调用不能与**SQLFetchScroll**或**SQLFetch**的调用混合使用。
