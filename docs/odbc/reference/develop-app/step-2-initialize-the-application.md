---
title: 步骤 2： 初始化应用程序 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- initializing applications [ODBC]
- application process [ODBC], initializing applications
ms.assetid: 23a7a230-ae2c-4a5e-9760-d2e17f92c389
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 85dff871a4b81551c699acc934aedb14c4f1725f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32915422"
---
# <a name="step-2-initialize-the-application"></a>步骤 2： 初始化应用程序
第二步是初始化应用程序，如下面的插图中所示。 完全什么上文所述因应用程序而异。  
  
 ![显示初始化 ODBC 应用程序](../../../odbc/reference/develop-app/media/pr12.gif "pr12")  
  
 此时，很少使用**SQLGetInfo**来发现该驱动程序的功能。 有关详细信息，请参阅[考虑要使用的数据库功能](../../../odbc/reference/develop-app/considering-database-features-to-use.md)。  
  
 所有应用程序需要分配语句句柄与**SQLAllocHandle**，许多应用程序设置语句属性，例如游标类型和**SQLSetStmtAttr**。 有关详细信息，请参阅[分配语句处理](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md)和[语句特性](../../../odbc/reference/develop-app/statement-attributes.md)。
