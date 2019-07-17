---
title: SQLCloseCursor_ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLCloseCursor function [ODBC], ODBC
ms.assetid: 5e47e3f7-e1b8-451f-bf75-daa19b7c7271
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a4d0f88d2d9eaba7d95ba887ffbe11e728320b17
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68123382"
---
# <a name="sqlclosecursorodbc"></a>SQLCloseCursor_ODBC
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题介绍如何使用**SQLCloseCursor**游标库中的函数。 有关常规信息**SQLCloseCursor**，请参阅[SQLCloseCursor 函数](../../../odbc/reference/syntax/sqlclosecursor-function.md)。  
  
 游标库不支持调用**SQLCloseCursor**而无需打开的游标。 这种尝试将返回 SQLSTATE 24000 （无效的游标状态）。 调用**SQLFreeStmt**与*选项*SQL_CLOSE 的任何游标打开时由游标库支持。
