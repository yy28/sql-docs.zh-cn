---
title: 参数值的数组 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 9b572c5b-1dfe-40af-bebd-051548ab6d90
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 03479a0187c7720a595b550290a8f5ac8197fa9c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63288404"
---
# <a name="arrays-of-parameter-values"></a>参数值的数组
通常很有用的应用程序传递参数的数组。 例如，使用参数和参数化的数组**插入**语句中，应用程序可以在一次插入的行数。 有以下几个使用数组优点。 首先，因为单个数据包中发送多个语句数据，（如果数据源以本机方式支持参数数组） 减少网络流量。 第二，某些数据源可以执行 SQL 语句比执行相同数量的单独的 SQL 语句更快地使用数组。 最后，当数据存储到数组中，通常会是屏幕数据这种情况，应用程序可以绑定的所有行调用一次的特定列中**SQLBindParameter**并通过执行单个语句来更新它们。  
  
 遗憾的是，不多的数据源都支持参数数组。 但是，驱动程序可以通过执行一次为每个参数值集的 SQL 语句模拟参数数组。 这会导致增加的速度，因为该驱动程序然后准备它计划要为每个参数集一次执行的语句。 它还可能导致与更简单的应用程序代码。  
  
 本部分包含以下主题。  
  
-   [绑定参数的数组](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)  
  
-   [使用参数的数组](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)
