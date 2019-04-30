---
title: SQLSetConnectAttr （游标库） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d4023c513ffda04a3cf499110185d3746ca40d9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63299189"
---
# <a name="sqlsetconnectattr-cursor-library"></a>SQLSetConnectAttr（游标库）
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题介绍如何使用**SQLSetConnectAttr**游标库中的函数。 有关常规信息**SQLSetConnectAttr**，请参阅[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
 应用程序调用**SQLSetConnectAttr**与 SQL_ATTR_ODBC_CURSORS 属性来指定游标库是始终使用、 驱动程序不支持可滚动游标，如果使用或从未使用过。 游标库假设使用驱动程序支持可滚动游标，如果它返回 SQL_STATIC_CURSOR_ATTRIBUTES1 信息类型 SQL_CA1_RELATIVE **SQLGetInfo**。  
  
 应用程序必须调用**SQLSetConnectAttr**来指定游标库使用情况之后它将调用, **SQLAllocHandle**与*HandleType*设为 SQL_HANDLE_DBC 以分配连接和之后才会连接到数据源。 如果应用程序调用**SQLSetConnectAttr** SQL_ATTR_ODBC_CURSORS 属性与连接时仍处于活动状态，该游标库将返回错误。  
  
 若要设置的游标库与连接关联的所有语句的支持的语句属性，应用程序必须调用**SQLSetConnectAttr**后它连接到数据源和之前该语句属性打开游标。 如果应用程序调用**SQLSetConnectAttr**属性和游标是打开与连接关联的语句上使用语句、 语句属性将不会应用于该语句之前关闭游标和重新打开。
