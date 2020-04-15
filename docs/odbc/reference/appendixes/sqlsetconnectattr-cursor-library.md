---
title: SQLSetConnectAttr（光标库） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectAttr function [ODBC], Cursor Library
ms.assetid: 6f70bbd0-a057-49ef-8b05-4c80b58fc6e6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a87c85d727fb9eb2fc27613b9eecd3fe0ec51b58
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300537"
---
# <a name="sqlsetconnectattr-cursor-library"></a>SQLSetConnectAttr（游标库）
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。  
  
 本主题讨论在游标库中使用**SQLSetConnectAttr**函数。 有关**SQLSetConnectAttr**的一般信息，请参阅[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
 应用程序使用SQL_ATTR_ODBC_CURSORS属性调用**SQLSetConnectAttr，** 以指定是否始终使用游标库、驱动程序不支持可滚动游标或从未使用过。 游标库假定驱动程序支持可滚动游标，如果它返回 SQL_CA1_RELATIVE在**SQLGetInfo**中SQL_STATIC_CURSOR_ATTRIBUTES1信息类型。  
  
 应用程序必须调用**SQLSetConnectAttr**来指定使用 SQLAllocHandle 的游标库使用情况，在调用**SQLAllocHandle**时，它使用 SQL_HANDLE_DBC*的句柄类型*来分配连接，然后再连接到数据源。 如果应用程序在连接仍处于活动状态时使用 SQL_ATTR_ODBC_CURSORS 属性调用**SQLSetConnectAttr，** 则游标库将返回错误。  
  
 要为与连接关联的所有语句设置游标库支持的语句属性，应用程序必须在连接到数据源并在打开游标之前为该语句属性调用**SQLSetConnectAttr。** 如果应用程序使用语句属性调用**SQLSetConnectAttr，** 并且与连接关联的语句上打开游标，则在关闭和重新打开游标之前，语句属性将不会应用于该语句。
