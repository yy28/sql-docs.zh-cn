---
title: 步骤4b：提取行计数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- fetches [ODBC], fetching row count
- row count [ODBC]
- application process [ODBC], fetching row count
ms.assetid: 3af481b1-d694-446e-948d-e3a5edcad050
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31ccbd15ae435165ea007fa9f3c0505c1dcc5aa0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302958"
---
# <a name="step-4b-fetch-the-row-count"></a>步骤 4b：提取行计数
下一步是提取行计数，如下图所示。  
  
 ![显示如何提取行计数](../../../odbc/reference/develop-app/media/pr15.gif "pr15")  
  
 如果在步骤3中执行的语句是**UPDATE**、 **DELETE**或**INSERT**语句，则应用程序将使用**SQLRowCount**检索受影响行的计数。 有关详细信息，请参阅[确定受影响的行数](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)。  
  
 现在，应用程序返回到步骤3来执行同一事务中的另一个语句，或继续执行步骤5以提交或回滚事务。
