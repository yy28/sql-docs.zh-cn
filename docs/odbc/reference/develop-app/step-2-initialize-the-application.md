---
title: "步骤 2： 初始化应用程序 |Microsoft 文档"
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
- initializing applications [ODBC]
- application process [ODBC], initializing applications
ms.assetid: 23a7a230-ae2c-4a5e-9760-d2e17f92c389
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3aee15e4a528c7848a03ec4695a3ffd23edf106f
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="step-2-initialize-the-application"></a>步骤 2： 初始化应用程序
第二步是初始化应用程序，如下面的插图中所示。 完全什么上文所述因应用程序而异。  
  
 ![显示初始化 ODBC 应用程序](../../../odbc/reference/develop-app/media/pr12.gif "pr12")  
  
 此时，很少使用**SQLGetInfo**来发现该驱动程序的功能。 有关详细信息，请参阅[考虑要使用的数据库功能](../../../odbc/reference/develop-app/considering-database-features-to-use.md)。  
  
 所有应用程序需要分配语句句柄与**SQLAllocHandle**，许多应用程序设置语句属性，例如游标类型和**SQLSetStmtAttr**。 有关详细信息，请参阅[分配语句处理](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md)和[语句特性](../../../odbc/reference/develop-app/statement-attributes.md)。
