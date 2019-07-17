---
title: 步骤 2：初始化应用程序 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 41030015645bda11242a703a163f26104e66dba0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114252"
---
# <a name="step-2-initialize-the-application"></a>步骤 2：初始化应用程序
第二步是初始化应用程序，如以下插图所示。 与应用程序完全什么此处这样做是各不相同。  
  
 ![显示正在初始化 ODBC 应用程序](../../../odbc/reference/develop-app/media/pr12.gif "pr12")  
  
 此时，它是通常使用**SQLGetInfo**来发现该驱动程序的功能。 有关详细信息，请参阅[考虑要使用的数据库功能](../../../odbc/reference/develop-app/considering-database-features-to-use.md)。  
  
 所有应用程序需要以分配语句句柄与**SQLAllocHandle**，并且许多应用程序设置语句属性，例如游标类型与**SQLSetStmtAttr**。 有关详细信息，请参阅[分配的语句句柄](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md)并[语句属性](../../../odbc/reference/develop-app/statement-attributes.md)。
