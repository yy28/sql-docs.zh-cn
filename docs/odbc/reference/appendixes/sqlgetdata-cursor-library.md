---
title: SQLGet数据（光标库） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], Cursor Library
ms.assetid: ff40c9c0-b847-4426-a099-1bff47e6e872
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07200d48f439c97003da7062fc218cd2f3081d1b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307838"
---
# <a name="sqlgetdata-cursor-library"></a>SQLGetData（游标库）
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。  
  
 本主题讨论在游标库中使用**SQLGetData**函数。 有关**SQLGetData**的一般信息，请参阅[SQLGetData 函数](../../../odbc/reference/syntax/sqlgetdata-function.md)。  
  
 游标库通过首先构造一个**SELECT**语句来实现**SQLGetData，** 该语句具有**WHERE**子句，该子句枚举当前行中每个绑定列存储在其缓存中的值。 然后，它执行**SELECT**语句以重新选择该行，并在驱动程序中调用**SQLGetData**以从数据源（而不是缓存）检索数据。  
  
> [!CAUTION]  
>  游标库为标识当前行而构造的**WHERE**子句可能无法标识任何行、标识其他行或标识多行。 有关详细信息，请参阅[构造搜索语句](../../../odbc/reference/appendixes/constructing-searched-statements.md)。  
  
 如果将SQL_ATTR_USE_BOOKMARKS语句属性设置为SQL_UB_VARIABLE，则可以在第 0 列上调用**SQLGetData**来返回书签数据。  
  
 对**SQLGetData 的**调用受以下限制：  
  
-   不能为仅转发游标调用**SQLGetData。**  
  
-   仅当满足以下条件时才能调用**SQLGetData：SELECT**语句**SELECT**生成结果集;**SELECT**语句不包含联接 **、UNION**子句或**GROUP BY**子句;并且在选择列表中使用别名或表达式的任何列未绑定到**SQLBindCol**。  
  
-   如果驱动程序仅支持一个活动语句，则游标库在执行**SELECT**语句并调用**SQLGetData**之前获取结果集的其余部分。
