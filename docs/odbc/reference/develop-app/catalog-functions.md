---
title: 目录函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], about catalog functions
- data dictionary [ODBC]
- catalog functions [ODBC]
- functions [ODBC], catalog functions
ms.assetid: 81ba9453-c085-47c0-b411-90ca6a5ee428
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 268d5f00d787cef8dfdcb29bd9e091f81a5ed2c9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63125575"
---
# <a name="catalog-functions"></a>目录函数
所有数据库都有一个结构，其中概述了如何将数据库中存储数据。 例如，简单的销售订单数据库可能具有在下图中，ID 列使用链接的表中所示的结构。  
  
 ![显示了一个简单的数据库的结构](../../../odbc/reference/develop-app/media/pr19.gif "pr19")  
  
 此结构，以及其他信息的权限，例如存储在名为数据库的系统表的一组*目录，* 也称为*数据字典*。  
  
 应用程序可以发现此结构通过调用*目录函数*。 目录函数返回结果集和进行中的信息通常通过实现**选择**目录中的表的语句。 例如，应用程序可以请求包含系统上所有表的相关信息的结果集或包含特定表中的所有列的相关信息的结果集。  
  
 本部分包含以下主题。  
  
-   [目录数据的用法](../../../odbc/reference/develop-app/uses-of-catalog-data.md)  
  
-   [ODBC 中的目录函数](../../../odbc/reference/develop-app/catalog-functions-in-odbc.md)
