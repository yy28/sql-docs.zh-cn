---
title: 直接连接到驱动程序 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SqlDriverConnect
- SQLDriverConnect function [ODBC], connecting directly to drivers
- connecting to driver [ODBC], drivers
ms.assetid: f86e198f-a088-4401-9106-aa62a0eb8f6e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d6aacb5d3df985949e04cdd47a9fe460cddbde6a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299077"
---
# <a name="connecting-directly-to-drivers"></a>直接连接到驱动程序
如本节前面在[选择数据源或驱动程序](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)时所讨论的那样，某些应用程序根本不希望使用数据源。 相反，他们希望直接连接到驱动程序。 **SQLDriverConnect**为应用程序提供了一种直接连接到驱动程序的方法，而无需指定数据源。 从概念上讲，在运行时创建临时数据源。  
  
 要直接连接到驱动程序，应用程序在连接字符串中指定**DRIVER**关键字，而不是**DSN**关键字。 **DRIVER**关键字的值是**SQLDriver**返回的驱动程序的说明。 例如，假设驱动程序具有描述悖论驱动程序，并且需要包含数据文件的目录的名称。 要连接到此驱动程序，应用程序可能使用以下连接字符串之一：  
  
```  
DRIVER={Paradox Driver};Directory=C:\PARADOX;  
DRIVER={Paradox Driver};  
```  
  
 使用第一个字符串时，驱动程序不需要任何其他信息。 使用第二个字符串时，驱动程序需要提示包含数据文件的目录的名称。
