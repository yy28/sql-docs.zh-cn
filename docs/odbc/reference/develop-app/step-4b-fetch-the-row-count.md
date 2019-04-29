---
title: 步骤 4b：提取行计数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3091d379bca6c061437e7767fdf6f99d69dc9861
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63149164"
---
# <a name="step-4b-fetch-the-row-count"></a>步骤 4b：提取行计数
下一步是提取行计数，如下图中所示。  
  
 ![显示如何提取行计数](../../../odbc/reference/develop-app/media/pr15.gif "pr15")  
  
 如果在步骤 3 中执行的语句**更新**，**删除**，或**插入**语句，该应用程序检索的受影响的行计数**SQLRowCount**。 有关详细信息，请参阅[确定受影响的行数](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)。  
  
 应用程序现在返回到步骤 3 以在同一事务中执行另一个语句，或继续到步骤 5 以提交或回滚事务。
