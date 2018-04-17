---
title: SQLFreeStmt （光标库） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLFreeStmt function [ODBC], Cursor Library
ms.assetid: 47bfbd4d-9453-4609-958d-1e05794cb223
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 04d1ef277a75720f75e15b77d7bb8c5e7b96fafa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sqlfreestmt-cursor-library"></a>SQLFreeStmt （光标库）
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题讨论使用**SQLFreeStmt**光标库中的函数。 有关常规信息**SQLFreeStmt**，请参阅[SQLFreeStmt 函数](../../../odbc/reference/syntax/sqlfreestmt-function.md)。  
  
 如果应用程序调用**SQLFreeStmt** SQL_UNBIND 选项后，它调用具有**SQLExtendedFetch**， **SQLFetch**，或**SQLFetchScroll**，光标库返回错误。 它可以取消绑定结果集中的列之前，必须调用应用程序**SQLCloseCursor**或**SQLFreeStmt** SQL_CLOSE 选项。
