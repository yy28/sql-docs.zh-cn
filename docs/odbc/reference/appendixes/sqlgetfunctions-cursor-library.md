---
title: SQLGet 函数（光标库） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetFunctions function [ODBC], Cursor Library
ms.assetid: 931acd12-4eb6-4a78-9a77-157a18a9a2d0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f993a08aae1656b8d373911299e75852de855419
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307818"
---
# <a name="sqlgetfunctions-cursor-library"></a>SQLGetFunctions（游标库）
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。  
  
 本主题讨论在游标库中使用**SQLGet 函数函数**。 有关**SQLGet 函数**的一般信息，请参阅[SQLGet 函数](../../../odbc/reference/syntax/sqlgetfunctions-function.md)。  
  
 调用**SQLGet 函数**时，光标库返回它支持**SQL 扩展获取****、SQLFetchScroll、SQLSetPos**和**SQLSetScrollOptions，** 以及驱动程序支持的函数。 **SQLSetPos**
