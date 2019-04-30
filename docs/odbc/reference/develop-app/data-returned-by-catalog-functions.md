---
title: 目录函数返回的数据 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], result sets
- functions [ODBC], catalog functions
ms.assetid: 399e1a64-8766-4c44-81ff-445399b7a1de
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10e3726d26e03da2f9f731babc105244dbf1ff05
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63267731"
---
# <a name="data-returned-by-catalog-functions"></a>目录函数返回的数据
每个目录函数返回的数据作为结果集。 此结果集是与任何其他结果集没有什么不同。 它通常生成的一个预定义参数化**选择**是硬编码在驱动程序或存储在数据源中的过程中的语句。 有关如何从结果集中检索数据的信息，请参阅[是一个结果集创建？](../../../odbc/reference/develop-app/was-a-result-set-created.md)。  
  
 该函数的引用项中描述的每个目录函数的结果集。 除了所列出的列，结果集可以包含特定于驱动程序的列，最后一个预定义列之后。 驱动程序文档中描述了这些列 （如果有）。  
  
 应用程序应将相对于结果集末尾的驱动程序特定列绑定。 应为最后一列-使用检索到的数字计算的特定于驱动程序的列数，即**SQLNumResultCols** -更少的所需的列后出现的列数。 这样无需更改应用程序的新列添加到结果时可以节省设置在将来版本的 ODBC 或驱动程序。 若要运行此方案，驱动程序必须添加新驱动程序特定列之前旧驱动程序特定列，以便列号不会更改相对于结果集的末尾。  
  
 不带引号的标识符，在结果集中返回，即使它们包含特殊字符。 例如，假定标识符引号字符 (这是特定于驱动程序和通过返回**SQLGetInfo**) 是双引号 （"） 和 Accounts Payable 表包含一个名为 Customer Name 列。 在返回的行**SQLColumns**为本专栏中，TABLE_NAME 列的值为 Accounts Payable 日，不 Accounts Payable，且 COLUMN_NAME 列的值是客户名称，不"Customer Name"。 若要检索 Accounts Payable 表中的客户的名称，该应用程序会引用这些名称：  
  
```  
SELECT "Customer Name" FROM "Accounts Payable"  
```  
  
 有关详细信息，请参阅[带引号的标识符](../../../odbc/reference/develop-app/quoted-identifiers.md)。  
  
 目录函数基于在其中建立了连接基于用户名和密码，并返回用户对其具有权限的数据的类似于 SQL 的授权模型。 密码保护的单独的文件，不适合此模型，是驱动程序定义的。  
  
 目录函数返回的结果集几乎始终可更新，其应用程序不应期望将无法通过更改这些的结果集中的数据更改的数据库的结构。
