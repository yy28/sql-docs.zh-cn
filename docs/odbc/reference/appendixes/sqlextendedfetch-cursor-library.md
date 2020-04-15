---
title: SQL 扩展获取（光标库） |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302058"
---
# <a name="sqlextendedfetch-cursor-library"></a>SQLExtendedFetch（游标库）
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。  
  
 本主题讨论在游标库中使用**SQL 扩展获取**函数。 有关 SQL**扩展获取**的一般信息，请参阅[SQL 扩展获取函数](../../../odbc/reference/syntax/sqlextendedfetch-function.md)。  
  
 游标库通过在驱动程序中重复调用**SQLFetch**实现**SQL 扩展。**  
  
 游标库支持使用SQL_FETCH_BOOKMARK*的提取方向*调用**SQL 扩展获取**。  
  
 使用游标库时，对**SQLAaFetch 的**调用不能与**SQLFetchScroll 或** **SQLFetch**的调用混合。
