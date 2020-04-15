---
title: 目录功能 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb28ec6f4ea299dae8737fc707fd53e4d102442d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305198"
---
# <a name="catalog-functions"></a>目录函数
所有数据库都有一个结构，用于概述数据在数据库中的存储方式。 例如，简单的销售订单数据库可能具有下图中所示的结构，其中 ID 列用于链接表。  
  
 ![显示简单数据库的结构](../../../odbc/reference/develop-app/media/pr19.gif "pr19")  
  
 此结构以及其他信息（如特权）存储在一组称为数据库目录的系统表中 *，* 也称为*数据字典*。  
  
 应用程序可以通过调用*目录函数*来发现此结构。 目录函数返回结果集中的信息，通常通过针对目录中的表的**SELECT**语句实现。 例如，应用程序可以请求包含系统上所有表的相关信息的结果集或包含特定表中的所有列的相关信息的结果集。  
  
 本部分包含以下主题。  
  
-   [目录数据的用法](../../../odbc/reference/develop-app/uses-of-catalog-data.md)  
  
-   [ODBC 中的目录函数](../../../odbc/reference/develop-app/catalog-functions-in-odbc.md)
