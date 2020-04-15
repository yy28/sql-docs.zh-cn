---
title: SQLEndTran（光标库） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLEndTran function [ODBC], Cursor Library
ms.assetid: 92340b87-9084-4838-a509-e9ca22d5fd5c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c2277a67cd5410ea3c2a5d5b03b16d4533ed6ee1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304765"
---
# <a name="sqlendtran-cursor-library"></a>SQLEndTran（游标库）
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。  
  
 本主题讨论在游标库中使用**SQLEndTran**函数。 有关**SQLEndTran**的一般信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。  
  
 游标库不支持事务，并将对**SQLEndTran**的调用直接传递给驱动程序。 但是，游标库确实支持数据源返回的带有SQL_CURSOR_ROLLBACK_BEHAVIOR和SQL_CURSOR_COMMIT_BEHAVIOR信息类型的游标提交和回滚行为：  
  
-   对于跨事务保留游标的数据源，在数据源中回滚的更改不会在游标库的缓存中回滚。 要使缓存与数据源中的数据匹配，应用程序必须关闭并重新打开游标。  
  
-   对于在事务边界关闭游标的数据源，游标库将关闭游标并删除连接上所有语句的缓存。  
  
-   对于在事务边界删除已准备好的语句的数据源，应用程序必须在重新执行连接之前重新准备连接上的所有准备好的语句。
