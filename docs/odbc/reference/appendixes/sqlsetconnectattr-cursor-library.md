---
title: "SQLSetConnectAttr （光标库） |Microsoft 文档"
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
- SQLSetConnectAttr function [ODBC], Cursor Library
ms.assetid: 6f70bbd0-a057-49ef-8b05-4c80b58fc6e6
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bf6a14b8215f981e5e0e9c0ca6e9b2e1a2269f65
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetconnectattr-cursor-library"></a>SQLSetConnectAttr （光标库）
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题讨论使用**SQLSetConnectAttr**光标库中的函数。 有关常规信息**SQLSetConnectAttr**，请参阅[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
 应用程序调用**SQLSetConnectAttr**具有 SQL_ATTR_ODBC_CURSORS 属性指定的是光标库是始终使用、 驱动程序不支持可滚动游标，如果使用或从未使用过。 游标库假定驱动程序支持可滚动游标，如果它返回 SQL_CA1_RELATIVE SQL_STATIC_CURSOR_ATTRIBUTES1 信息类型**SQLGetInfo**。  
  
 应用程序必须调用**SQLSetConnectAttr**以后它会调用指定的光标库使用情况**SQLAllocHandle**与*HandleType*的 SQL_HANDLE_DBC 分配连接和之后才会连接到数据源。 如果应用程序调用**SQLSetConnectAttr** SQL_ATTR_ODBC_CURSORS 属性与连接时仍处于活动状态，游标库返回错误。  
  
 若要将与连接相关联的所有语句光标 library 所支持的语句特性设置，应用程序必须调用**SQLSetConnectAttr**连接到数据源和之前它后该语句属性将打开光标。 如果应用程序调用**SQLSetConnectAttr**属性并且光标位于在与连接关联的语句上打开与语句一起使用，则不语句属性将应用于该语句中，直到关闭游标和重新打开。
