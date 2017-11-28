---
title: "参数标记 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- parameter markers [ODBC]
ms.assetid: 07213d04-cd31-45fd-a8c8-2e16e09eeaf4
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 58bde9217e293f1f3fb0a68a7cbf2c4aef6aac1e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="parameter-markers"></a>参数标记
根据 sql-92 规范中，应用程序无法将参数标记放置在以下位置。 有关更完整的列表，请参阅 sql-92 规范。  
  
-   在**选择**列表  
  
-   为这两者*表达式*中*比较谓词*  
  
-   作为二元运算符的两个操作数  
  
-   用作的第一个和第二个操作数**BETWEEN**操作  
  
-   作为第一个和第三个操作数的**BETWEEN**操作  
  
-   作为表达式的第一个值**IN**操作  
  
-   与操作数的一元 + 或 – 操作  
  
-   作为的自变量*集的函数参考*  
  
 有关参数标记的详细信息，请参阅 sql-92 规范。 有关参数的详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。
