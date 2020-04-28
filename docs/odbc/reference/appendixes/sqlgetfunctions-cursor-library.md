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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f993a08aae1656b8d373911299e75852de855419
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307818"
---
# <a name="sqlgetfunctions-cursor-library"></a>SQLGetFunctions（游标库）
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题讨论如何在游标库中使用**SQLGetFunctions**函数。 有关**SQLGetFunctions**的常规信息，请参阅[SQLGetFunctions 函数](../../../odbc/reference/syntax/sqlgetfunctions-function.md)。  
  
 当调用**SQLGetFunctions**时，游标库将返回它支持**SQLExtendedFetch**、 **SQLFetchScroll**、 **SQLSetPos**和**SQLSetScrollOptions**，以及驱动程序支持的函数。
