---
title: SQLFreeStmt （游标库） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeStmt function [ODBC], Cursor Library
ms.assetid: 47bfbd4d-9453-4609-958d-1e05794cb223
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d78075593926c15dbaeb1904603b08e990f64983
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302018"
---
# <a name="sqlfreestmt-cursor-library"></a>SQLFreeStmt（游标库）
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题讨论如何在游标库中使用**SQLFreeStmt**函数。 有关**SQLFreeStmt**的常规信息，请参阅[SQLFreeStmt 函数](../../../odbc/reference/syntax/sqlfreestmt-function.md)。  
  
 如果应用程序在调用**SQLExtendedFetch**、 **SQLFetch**或**SQLFetchScroll**后使用 SQL_UNBIND 选项调用**SQLFreeStmt** ，则游标库将返回错误。 应用程序必须使用 SQL_CLOSE 选项调用**SQLCloseCursor**或**SQLFreeStmt** ，然后才能取消对结果集列的绑定。
