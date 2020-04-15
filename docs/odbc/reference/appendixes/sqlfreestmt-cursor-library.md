---
title: SQLFreeStmt（光标库） |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302018"
---
# <a name="sqlfreestmt-cursor-library"></a>SQLFreeStmt（游标库）
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。  
  
 本主题讨论在游标库中使用**SQLFreeStmt**函数。 有关**SQLFreeStmt 的**一般信息，请参阅[SQLFreeStmt 函数](../../../odbc/reference/syntax/sqlfreestmt-function.md)。  
  
 如果应用程序在调用**SQLAtFetch、SQLFetch**或**SQLFetchScroll****SQLFetch**后使用SQL_UNBIND选项调用**SQLFreeStmt，** 则游标库将返回一个错误。 在取消绑定结果集列之前，应用程序必须使用SQL_CLOSE选项调用**SQLCloseCursor**或**SQLFreeStmt。**
