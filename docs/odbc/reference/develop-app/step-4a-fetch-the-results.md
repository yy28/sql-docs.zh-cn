---
title: 步骤 4a： 提取结果 |Microsoft 文档
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
- application process [ODBC], fetching results
- fetches [ODBC], fetching results
ms.assetid: 77d30142-c774-473c-96fb-b364bb92ac60
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7d8d2e5bd80e47db5a5e3484aebfe2bf1d6fff9a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32915742"
---
# <a name="step-4a-fetch-the-results"></a>步骤 4a： 提取结果
下一步是提取结果，如下面的插图中所示。  
  
 ![显示如何提取 ODBC 应用程序中的结果](../../../odbc/reference/develop-app/media/pr14.gif "pr14")  
  
 如果在"步骤 3:: 生成并执行 SQL 语句"中执行的语句已**选择**语句或目录函数，在应用程序首先调用**SQLNumResultCols**来确定的列数在结果集中。 此步骤不需要如果应用程序已知道设置列，例如 SQL 语句时硬编码在垂直或自定义应用程序中的结果数。  
  
 接下来，应用程序检索名称、 数据类型、 精度和小数位数为与每个结果集列**SQLDescribeCol**。 同样，这不是如已经知道此信息的垂直和自定义应用程序的应用程序所需的。 应用程序传递到此信息**SQLBindCol**，这会将应用程序变量绑定到结果集中的列。  
  
 应用程序现在调用**SQLFetch**检索数据的第一行并将该行中的数据放在通过绑定变量**SQLBindCol**。 如果行中没有任何长整型数据，然后调用**SQLGetData**以检索此数据。 应用程序将继续调用**SQLFetch**和**SQLGetData**无法检索其他数据。 它已完成提取数据后，它会调用**SQLCloseCursor**要关闭游标。  
  
 检索结果的完整说明，请参阅[检索结果 (Basic)](../../../odbc/reference/develop-app/retrieving-results-basic.md)和[检索结果 （高级）](../../../odbc/reference/develop-app/retrieving-results-advanced.md)。  
  
 在应用程序现在返回到"步骤 3:: 生成并执行 SQL 语句"以在同一个事务; 中执行另一个语句或转到"步骤 5:: 提交事务"以提交或回滚事务。
