---
title: 步骤 4a：获取结果 |微软文档
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
ms.openlocfilehash: c4f810e5c42b54ec871c233ab498936abae610dc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302968"
---
# <a name="step-4a-fetch-the-results"></a>步骤 4a：提取结果
下一步是获取结果，如下图所示。  
  
 ![显示如何在 ODBC 应用程序中提取结果](../../../odbc/reference/develop-app/media/pr14.gif "pr14")  
  
 如果在"步骤 3：生成和执行 SQL 语句"中执行的语句是**SELECT**语句或目录函数，则应用程序首先调用**SQLNumResultCols**以确定结果集中的列数。 如果应用程序已经知道结果集列的数量（例如，在垂直或自定义应用程序中硬编码 SQL 语句时），则不需要此步骤。  
  
 接下来，应用程序使用**SQLDescribeCol**检索每个结果集列的名称、数据类型、精度和比例。 同样，对于已经知道此信息的垂直和自定义应用程序，这同样是必需的。 应用程序将此信息传递给 SQLBindCol ，该**SQLBindCol**将应用程序变量绑定到结果集中的列。  
  
 应用程序现在调用**SQLFetch**来检索第一行数据，并将该行中的数据放在与**SQLBindCol**绑定的变量中。 如果行中有任何长数据，则调用**SQLGetData**来检索该数据。 应用程序继续调用**SQLFetch**和**SQLGetData**来检索其他数据。 完成数据提取后，它将调用**SQLCloseCursor**关闭光标。  
  
 有关检索结果的完整说明，请参阅[检索结果（基本）](../../../odbc/reference/develop-app/retrieving-results-basic.md)和[检索结果（高级）。](../../../odbc/reference/develop-app/retrieving-results-advanced.md)  
  
 应用程序现在返回到"步骤 3：生成和执行 SQL 语句"，以在同一事务中执行另一个语句;或继续"步骤 5：提交事务"以提交或回滚事务。
