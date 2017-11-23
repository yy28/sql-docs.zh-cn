---
title: "目录函数返回的数据 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- catalog functions [ODBC], result sets
- functions [ODBC], catalog functions
ms.assetid: 399e1a64-8766-4c44-81ff-445399b7a1de
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 46b8a628b6b8e6ad9a2eb3164e6935f3f3401ec8
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="data-returned-by-catalog-functions"></a>目录函数返回的数据
每个目录函数返回数据作为结果集。 此结果集是与任何其他结果集中没有什么不同。 它通常生成通过预定义参数化**选择**是硬编码在驱动程序或存储在数据源中的过程的语句。 有关如何从结果集中检索数据的信息，请参阅[已结果设置创建？](../../../odbc/reference/develop-app/was-a-result-set-created.md)。  
  
 每个目录函数的结果集是该函数的引用项中所述。 除了所列出的列，结果集可以包含特定于驱动程序的列，最后一个的预定义列之后。 驱动程序文档描述了这些列 （如果有）。  
  
 应用程序应绑定相对于结果集的末尾的驱动程序的特定列。 应为最后一列数计算的特定于驱动程序的列数，即-使用检索**SQLNumResultCols** -较晚所需的列的列数。 这无需更改应用程序，新列添加到结果时可以节省设置在将来版本的 ODBC 或驱动程序。 对于此方案中工作，驱动程序必须添加新的驱动程序的特定列之前旧驱动程序的特定列，以便将列号不会更改相对于结果集的末尾。  
  
 不带引号的标识符，在结果集中返回，即使它们包含特殊字符。 例如，假定标识符引号字符 (这是特定于驱动程序和通过返回**SQLGetInfo**) 是双引号 （"） 和 Accounts Payable 表包含一个名为客户名称列。 在返回的行**SQLColumns**对于此列，TABLE_NAME 列的值为应付帐款不"Accounts Payable"，而 COLUMN_NAME 列的值是客户名称，不"客户名称"。 若要检索的应付帐款表中的客户的名称，该应用程序将引用这些名称定义：  
  
```  
SELECT "Customer Name" FROM "Accounts Payable"  
```  
  
 有关详细信息，请参阅[带引号的标识符](../../../odbc/reference/develop-app/quoted-identifiers.md)。  
  
 目录函数基于在其中连接将进行基于用户名和密码，并仅为其用户具有权限的数据返回的类似 SQL 的授权模型。 密码保护的单个文件，不适合此模型，是驱动程序定义的。  
  
 目录函数返回结果集几乎从未可更新，并且应用程序不应期望能够通过更改中这些结果集的数据更改数据库的结构。
