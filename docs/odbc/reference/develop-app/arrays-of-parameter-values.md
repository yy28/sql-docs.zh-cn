---
title: 参数值数组 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb9389c769e3a7bb0c39959a559531e8051a7bec
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298792"
---
# <a name="arrays-of-parameter-values"></a>参数值的数组
对于应用程序来说，传递参数数组通常很有用。 例如，使用参数数组和参数化**的 INSERT**语句，应用程序可以同时插入多个行。 使用数组有几个优点。 首先，网络流量减少，因为许多语句的数据在单个数据包中发送（如果数据源本机支持参数数组）。 其次，某些数据源可以使用数组执行 SQL 语句，比执行相同数量的单独 SQL 语句更快。 最后，当数据存储在数组中时（就像屏幕数据通常的情况一样），应用程序可以使用对**SQLBindparameter**的单一调用绑定特定列中的所有行，并通过执行单个语句来更新它们。  
  
 遗憾的是，支持参数数组的数据源并不多。 但是，驱动程序可以通过为每个参数值集执行一次 SQL 语句来模拟参数数组。 这可能导致速度增加，因为驱动程序随后可以准备计划为每个参数集执行一次的语句。 它还可能导致更简单的应用程序代码。  
  
 本部分包含以下主题。  
  
-   [绑定参数的数组](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)  
  
-   [使用参数的数组](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)
