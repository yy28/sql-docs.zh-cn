---
description: 参数值的数组
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 230f15f1c9cae0509ba7d616ab61ed5d8d7a370b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483110"
---
# <a name="arrays-of-parameter-values"></a>参数值的数组
它通常可用于应用程序传递参数数组。 例如，使用参数数组和参数化 **INSERT** 语句，应用程序可以一次插入多个行。 使用数组有几个优点。 首先，降低网络流量，因为如果数据源) 本身支持参数数组，则会在单个数据包 (中发送多个语句的数据。 其次，某些数据源可以比执行相同数目的不同 SQL 语句，使用数组更快地执行 SQL 语句。 最后，当数据存储在数组中时，通常是屏幕数据的情况，应用程序可以将特定列中的所有行绑定到 **SQLBindParameter** ，并通过执行单个语句来更新这些行。  
  
 遗憾的是，不是许多数据源支持参数数组。 但是，驱动程序可以通过对每组参数值执行一次 SQL 语句来模拟参数数组。 这可能会导致速度提高，因为驱动程序随后可以准备它计划为每个参数集执行一次的语句。 它还可能导致应用程序代码更简单。  
  
 本部分包含以下主题。  
  
-   [绑定参数的数组](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)  
  
-   [使用参数的数组](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)
