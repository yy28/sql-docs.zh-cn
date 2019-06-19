---
title: 参数标记 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- parameter markers [ODBC]
ms.assetid: 07213d04-cd31-45fd-a8c8-2e16e09eeaf4
author: MightyPen
ms.author: genemi
ms.reviewer: ''
manager: craigg
ms.openlocfilehash: cda6719eb46a4a05222bd54062e6cab98459d7dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63181778"
---
# <a name="parameter-markers"></a>参数标记
SQL-92 规范中，根据应用程序不能将参数标记放置在以下位置。 有关更全面的列表，请参阅 SQL-92 规范。  
  
-   在中**选择**列表  
  
-   为这两者*表达式*中*的比较谓词*  
  
-   作为二元运算符的两个操作数  
  
-   作为的第一个和第二个操作数**BETWEEN**操作  
  
-   作为第一个和第三操作数**BETWEEN**操作  
  
-   作为表达式的第一个值**IN**操作  
  
-   作为操作数的一元 + 或-操作  
  
-   作为自变量的*集函数引用*  
  
 有关参数标记的详细信息，请参阅 SQL-92 规范。 有关参数的详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。
