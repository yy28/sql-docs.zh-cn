---
title: SQLFetch（光标库） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFetch function [ODBC], Cursor Library
ms.assetid: 35a0d493-778b-4fb1-84ee-a13540e2fe0e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bee83ccb5497888b57a45673599af6b92931a704
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298717"
---
# <a name="sqlfetch-cursor-library"></a>SQLFetch（游标库）
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。  
  
 本主题讨论在游标库中使用**SQLFetch**函数。 有关**SQLFetch 的**一般信息，请参阅[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
 使用游标库时，对**SQLFetch 的**调用不能与**SQLFetchScroll 或** **SQL 扩展获取的**调用混合。  
  
 如果将**SQLFetch**调用SQL_ATTR_ROW_ARRAY_SIZE设置为大于 1 的值，则游标库将调用传递给驱动程序。 如果驱动程序是 ODBC 2。*x*驱动程序，将忽略行集大小，对**SQLFetch**的调用将返回一行数据。  
  
 如果光标库与 ODBC 2 一起使用。*x*驱动程序，在调用**SQLFetch**时不使用绑定偏移量（由SQL_ATTR_ROW_BIND_OFFSET_PTR语句属性定义）。  
  
 加载游标库时，应用程序无法调用**SQLFetch**来获取书签列。 游标库将**SQLFetch**的调用传递给驱动程序，但启用书签和绑定书签列的函数调用被游标库截获。
