---
title: SQLGetFunctions （游标库） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1123a6497207f40bd210edf35b9b4477bc9c7b6b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188726"
---
# <a name="sqlgetfunctions-cursor-library"></a>SQLGetFunctions（游标库）
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题介绍如何使用**SQLGetFunctions**游标库中的函数。 有关常规信息**SQLGetFunctions**，请参阅[SQLGetFunctions 函数](../../../odbc/reference/syntax/sqlgetfunctions-function.md)。  
  
 当您调用**SQLGetFunctions**，该游标库返回它支持**SQLExtendedFetch**， **SQLFetchScroll**， **SQLSetPos**，并**SQLSetScrollOptions**，除了由驱动程序支持的函数。
