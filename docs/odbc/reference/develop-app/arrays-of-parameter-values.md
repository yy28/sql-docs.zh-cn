---
title: "参数值的数组 |Microsoft 文档"
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
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 9b572c5b-1dfe-40af-bebd-051548ab6d90
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7a0bb497044e9800461b60021fc9a6c8db4e9cca
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="arrays-of-parameter-values"></a>参数值的数组
通常很有用的应用程序传递的参数数组。 例如，使用参数和参数化的数组**插入**语句，应用程序可以在一次插入的行数。 有以下几个使用数组优点。 首先，网络流量减少，因为 （如果数据源以本机方式支持参数数组），以单个数据包发送很多语句的数据。 其次，某些数据源可以执行使用数组快于执行相同数量的单独的 SQL 语句的 SQL 语句。 最后，在数据存储在数组中，因为通常是屏幕数据这种情况，应用程序绑定的所有行进行单个调用特定列中**SQLBindParameter**并通过执行单个语句对其进行更新。  
  
 遗憾的是，不多的数据源都支持参数数组。 但是，驱动程序可以通过执行 SQL 语句对于每个组的参数值执行一次模拟参数数组。 这会导致速度的增加，因为该驱动程序可以然后准备它打算执行一次为每个参数集的语句。 它还可能导致更简易的应用程序代码。  
  
 本部分包含以下主题。  
  
-   [绑定参数的数组](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)  
  
-   [使用参数的数组](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)

