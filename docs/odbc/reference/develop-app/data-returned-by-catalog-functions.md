---
title: 目录函数返回的数据 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a0d9b63de04f79fd95c1b06d8e84d85c6f4fea02
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305222"
---
# <a name="data-returned-by-catalog-functions"></a>目录函数返回的数据
每个目录函数作为结果集返回数据。 此结果集与任何其他结果集没有什么不同。 它通常由预定义的参数化**SELECT**语句生成，该语句在驱动程序中硬编码或存储在数据源中的一个过程中。 有关如何从结果集中检索数据的信息，请参阅["已创建结果集？"。](../../../odbc/reference/develop-app/was-a-result-set-created.md)  
  
 每个目录函数的结果集在该函数的引用条目中描述。 除了列出的列外，结果集还可以包含最后一个预定义列之后的特定于驱动程序的列。 驱动程序文档中描述了这些列（如果有）。  
  
 应用程序应绑定相对于结果集末尾的特定于驱动程序的列。 也就是说，它们应计算特定于驱动程序的列的数量，因为最后一列的编号 （使用**SQLNumResultCols**检索 ） 减去在所需列之后发生的列数。 这样，当在 ODBC 或驱动程序的未来版本中将新列添加到结果集时，无需更改应用程序。 要使此方案正常工作，驱动程序必须在旧特定于驱动程序的列之前添加新的特定于驱动程序的列，以便列号不会相对于结果集的末尾更改。  
  
 在结果集中返回的标识符不会引用，即使它们包含特殊字符。 例如，假设标识符报价字符（特定于驱动程序并通过**SQLGetInfo**返回）是一个双引号 （"），并且应付帐款表包含名为"客户名称"的列。 在**SQLColumn**为此列返回的行中，TABLE_NAME列的值是应付帐款，而不是"应付帐款"，COLUMN_NAME列的值是客户名称，而不是"客户名称"。 若要检索应付帐款表中的客户名称，应用程序将引用以下名称：  
  
```  
SELECT "Customer Name" FROM "Accounts Payable"  
```  
  
 有关详细信息，请参阅[引用标识符](../../../odbc/reference/develop-app/quoted-identifiers.md)。  
  
 目录函数基于类似 SQL 的授权模型，其中基于用户名和密码建立连接，并且仅返回用户具有权限的数据。 单个文件的密码保护（不适合此模型）是驱动程序定义的。  
  
 目录函数返回的结果集几乎永远不会升级，应用程序不应期望通过更改这些结果集中的数据来更改数据库的结构。
