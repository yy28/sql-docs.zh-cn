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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 07d56e9b77c7e7e34b0de98ef5704b26aa2b86dd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199460"
---
# <a name="sqlfreestmt-cursor-library"></a>SQLFreeStmt（游标库）
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题介绍如何使用**SQLFreeStmt**游标库中的函数。 有关常规信息**SQLFreeStmt**，请参阅[SQLFreeStmt 函数](../../../odbc/reference/syntax/sqlfreestmt-function.md)。  
  
 如果应用程序调用**SQLFreeStmt** SQL_UNBIND 选项后，它调用**SQLExtendedFetch**， **SQLFetch**，或**SQLFetchScroll**，该游标库将返回错误。 它可以取消绑定结果集列之前，应用程序必须调用**SQLCloseCursor**或**SQLFreeStmt** SQL_CLOSE 选项。
