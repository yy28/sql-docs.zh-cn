---
description: 步骤 4a：提取结果
title: 步骤4a：提取结果 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], fetching results
- fetches [ODBC], fetching results
ms.assetid: 77d30142-c774-473c-96fb-b364bb92ac60
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 91a81809d07faafac6511bb5ec96c97d4f59d654
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491354"
---
# <a name="step-4a-fetch-the-results"></a>步骤 4a：提取结果
下一步是提取结果，如下图所示。  
  
 ![显示如何在 ODBC 应用程序中提取结果](../../../odbc/reference/develop-app/media/pr14.gif "pr14")  
  
 如果在 "步骤3：生成并执行 SQL 语句" 中执行的语句是 **SELECT** 语句或目录函数，则该应用程序首先调用 **SQLNumResultCols** 以确定结果集中的列数。 如果应用程序已知道结果集列的数目，则不需要执行此步骤，例如，当 SQL 语句在垂直或自定义应用程序中硬编码时。  
  
 接下来，应用程序通过 **SQLDescribeCol**检索每个结果集列的名称、数据类型、精度和小数位数。 同样，对于已知道此信息的应用程序（如垂直和自定义应用程序），这并不是必需的。 应用程序将此信息传递给 **SQLBindCol**，这会将应用程序变量绑定到结果集中的列。  
  
 现在，应用程序会调用 **SQLFetch** 来检索第一行数据，并将该行中的数据置于与 **SQLBindCol**绑定的变量中。 如果行中有任何长数据，则它会调用 **SQLGetData** 来检索该数据。 应用程序继续调用 **SQLFetch** 和 **SQLGetData** 以检索其他数据。 完成数据提取后，它将调用 **SQLCloseCursor** 以关闭游标。  
  
 有关检索结果的完整说明，请参阅 [ (基本) 检索结果 ](../../../odbc/reference/develop-app/retrieving-results-basic.md) 和 [ (高级) 检索结果 ](../../../odbc/reference/develop-app/retrieving-results-advanced.md)。  
  
 应用程序现在返回到 "步骤3：生成和执行 SQL 语句" 以在同一事务中执行另一个语句;或转到 "步骤5：提交事务" 以提交或回滚事务。
