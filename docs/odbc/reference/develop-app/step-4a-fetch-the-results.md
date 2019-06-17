---
title: 步骤 4a：提取的结果 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cad33f1ccf798a08ef1f11667e59b4d5fb4888d8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149210"
---
# <a name="step-4a-fetch-the-results"></a>步骤 4a：提取结果
下一步是提取的结果，如以下插图所示。  
  
 ![显示如何提取 ODBC 应用程序中的结果](../../../odbc/reference/develop-app/media/pr14.gif "pr14")  
  
 如果该语句执行，则"步骤 3:生成并执行的 SQL 语句"已**选择**语句或目录函数，该应用程序首先调用**SQLNumResultCols**以确定结果集中的列数。 此步骤不是结果的必需的如果应用程序已知道设置列，例如，当 SQL 语句为垂直或自定义应用程序中硬编码数的。  
  
 接下来，应用程序检索名称、 数据类型、 精度和小数位数与每个结果集列**SQLDescribeCol**。 同样，这是不必要的应用程序，如垂直和自定义应用程序已经知道此信息。 应用程序传递到此信息**SQLBindCol**，这会将应用程序变量绑定到结果集中的列。  
  
 应用程序现在调用**SQLFetch**检索数据的第一行并将该行中的数据放在与绑定的变量**SQLBindCol**。 如果行中没有任何长整型数据，然后调用**SQLGetData**来检索该数据。 应用程序将继续调用**SQLFetch**并**SQLGetData**检索其他数据。 它已完成读取数据后，它会调用**SQLCloseCursor**以关闭游标。  
  
 检索结果的完整说明，请参阅[检索结果 （基本）](../../../odbc/reference/develop-app/retrieving-results-basic.md)并[检索结果 （高级）](../../../odbc/reference/develop-app/retrieving-results-advanced.md)。  
  
 应用程序现在返回到"步骤 3:生成并执行的 SQL 语句"以执行在同一个事务; 另一个语句或将继续到"步骤 5:提交事务"来提交或回滚事务。
