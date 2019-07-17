---
title: SQLGetData （游标库） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5962882de08712dcff75790de7c58d69f965a3bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086386"
---
# <a name="sqlgetdata-cursor-library"></a>SQLGetData（游标库）
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题介绍如何使用**SQLGetData**游标库中的函数。 有关常规信息**SQLGetData**，请参阅[SQLGetData 函数](../../../odbc/reference/syntax/sqlgetdata-function.md)。  
  
 游标库实现**SQLGetData**通过第一个构造**选择**语句与**其中**枚举每个绑定其缓存中存储的值的子句当前行中的列。 然后执行**选择**语句来重新选择行并调用**SQLGetData**驱动程序以从数据源 （而不是缓存） 中检索数据中。  
  
> [!CAUTION]  
>  **其中**子句通过游标库来标识当前行来构造可能无法识别的任何行，标识不同的行，或标识多个行。 有关详细信息，请参阅[构造搜索语句](../../../odbc/reference/appendixes/constructing-searched-statements.md)。  
  
 如果 SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_VARIABLE， **SQLGetData**可以调用第 0 返回书签的数据列。  
  
 调用**SQLGetData**受到以下限制：  
  
-   **SQLGetData**不能调用为只进游标。  
  
-   **SQLGetData**仅在满足以下条件时可调用：**选择**语句生成的结果集;**选择**语句未包含一个联接， **UNION**子句，或**分组依据**子句; 以及所有选择列表中使用了别名或表达式的列与未绑定**SQLBindCol**。  
  
-   如果该驱动程序支持只有一个活动语句，该游标库会提取结果集执行之前的 rest**选择**语句，并调用**SQLGetData**。
