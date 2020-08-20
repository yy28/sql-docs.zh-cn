---
description: 步骤 4b：提取行计数
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
ms.openlocfilehash: 1eab5e1e1bf7eba70e2d84b36349e2f982a0b14c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494600"
---
# <a name="step-4b-fetch-the-row-count"></a>步骤 4b：提取行计数
下一步是提取行计数，如下图所示。  
  
 ![显示如何提取行计数](../../../odbc/reference/develop-app/media/pr15.gif "pr15")  
  
 如果在步骤3中执行的语句是 **UPDATE**、 **DELETE**或 **INSERT** 语句，则应用程序将使用 **SQLRowCount**检索受影响行的计数。 有关详细信息，请参阅 [确定受影响的行数](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)。  
  
 现在，应用程序返回到步骤3来执行同一事务中的另一个语句，或继续执行步骤5以提交或回滚事务。
