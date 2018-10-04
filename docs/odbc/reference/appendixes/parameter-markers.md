---
title: 参数标记 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- parameter markers [ODBC]
ms.assetid: 07213d04-cd31-45fd-a8c8-2e16e09eeaf4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5ac59cddb24d5e08e3b620c178f40e206460eb7e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47835415"
---
# <a name="parameter-markers"></a>参数标记
SQL-92 规范中，根据应用程序不能将参数标记放置在以下位置。 有关更全面的列表，请参阅 SQL-92 规范。  
  
-   在中**选择**列表  
  
-   为这两者*表达式*中*的比较谓词*  
  
-   作为二元运算符的两个操作数  
  
-   作为的第一个和第二个操作数**BETWEEN**操作  
  
-   作为第一个和第三操作数**BETWEEN**操作  
  
-   作为表达式的第一个值**IN**操作  
  
-   作为操作数的一元 + 或 – 操作  
  
-   作为自变量的*集函数引用*  
  
 有关参数标记的详细信息，请参阅 SQL-92 规范。 有关参数的详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。
