---
title: 步骤 4b： 提取的行计数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- fetches [ODBC], fetching row count
- row count [ODBC]
- application process [ODBC], fetching row count
ms.assetid: 3af481b1-d694-446e-948d-e3a5edcad050
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 797920b512d117394c92fcc9c47006fbb84a22d5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="step-4b-fetch-the-row-count"></a>步骤 4b： 提取的行计数
下一步是提取的行计数，如下面的插图中所示。  
  
 ![显示如何提取的行计数](../../../odbc/reference/develop-app/media/pr15.gif "pr15")  
  
 如果在步骤 3 中执行的语句已**更新**，**删除**，或**插入**语句，应用程序检索的受影响的行计数**SQLRowCount**。 有关详细信息，请参阅[确定受影响的行数](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)。  
  
 应用程序现在返回到步骤 3 以在同一个事务中执行另一个语句，或将继续到步骤 5 以提交或回滚事务。
