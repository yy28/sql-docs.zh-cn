---
title: "SQLGetFunctions （光标库） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLGetFunctions function [ODBC], Cursor Library
ms.assetid: 931acd12-4eb6-4a78-9a77-157a18a9a2d0
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6d8ca656e63183df424de2ec45c823ac275ef69f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetfunctions-cursor-library"></a>SQLGetFunctions （光标库）
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题讨论使用**SQLGetFunctions**光标库中的函数。 有关常规信息**SQLGetFunctions**，请参阅[SQLGetFunctions 函数](../../../odbc/reference/syntax/sqlgetfunctions-function.md)。  
  
 当调用**SQLGetFunctions**，光标库返回它支持**SQLExtendedFetch**， **SQLFetchScroll**， **SQLSetPos**，和**SQLSetScrollOptions**，除了支持由驱动程序的函数。

