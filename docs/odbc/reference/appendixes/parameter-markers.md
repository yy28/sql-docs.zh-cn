---
title: 参数标记 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.reviewer: ''
ms.openlocfilehash: 132473de586094f79dd34c999d44f6dd59aefaef
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303568"
---
# <a name="parameter-markers"></a>参数标记
根据 SQL-92 规范，应用程序不能在以下位置放置参数标记。 有关更全面的列表，请参阅 SQL-92 规范。  
  
-   在**SELECT**列表中  
  
-   作为*比较谓词*中的两个*表达式*  
  
-   作为二进制运算符的两个操作数  
  
-   作为**BETWEEN**操作的第一个和第二个操作数  
  
-   作为**BETWEEN**操作的第一个和第三个操作数  
  
-   作为**IN**操作的表达式和第一个值  
  
-   作为一个一元 + 或 - 操作的操作  
  
-   作为*集函数引用*的参数  
  
 有关参数标记的详细信息，请参阅 SQL-92 规范。 有关参数的详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。
