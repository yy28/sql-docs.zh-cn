---
title: 步骤2：初始化应用程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- initializing applications [ODBC]
- application process [ODBC], initializing applications
ms.assetid: 23a7a230-ae2c-4a5e-9760-d2e17f92c389
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 843155ba6b641ea26717e63af55c8774f963a800
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81288263"
---
# <a name="step-2-initialize-the-application"></a>步骤 2：初始化应用程序
第二步是初始化应用程序，如下图所示。 此处所做的完全取决于应用程序。  
  
 ![显示如何初始化 ODBC 应用程序](../../../odbc/reference/develop-app/media/pr12.gif "pr12")  
  
 此时，通常使用**SQLGetInfo**来发现驱动程序的功能。 有关详细信息，请参阅[考虑要使用的数据库功能](../../../odbc/reference/develop-app/considering-database-features-to-use.md)。  
  
 所有应用程序都需要使用**SQLAllocHandle**来分配语句句柄，许多应用程序使用**SQLSetStmtAttr**设置语句属性（如游标类型）。 有关详细信息，请参阅[分配语句句柄](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md)和[语句属性](../../../odbc/reference/develop-app/statement-attributes.md)。
