---
title: "结果集元数据 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 6d134515-e34d-4563-96d7-8ad7714818fd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0f5de9f9b5b2a6da81fa175f24cd5bdf1b14e6e8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="result-set-metadata"></a>结果集元数据
*元数据*是描述其他数据的数据。 例如，结果集元数据描述结果集，如结果集中的列数、 数据类型的这些列，其名称、 精度、 可为 null，等等。  
  
 可互操作的应用程序应始终检查结果集中的列的元数据。 结果集中的列的元数据可能不同的列的元数据，如目录函数返回。 例如，假设，结果集中创建的联接两个表包含可更新列。 虽然**SQLColumnPrivileges**可能指示用户可以更新列，结果集元数据可能不如果该列为"多"侧的联接; 多个数据源可以更新的联接，但不是能在的"一"方上的列"多"端。 即使数据类型不能被认为在相同的因为数据源创建结果集时可能会提升的数据类型。  
  
 本部分包含以下主题。  
  
-   [是如何使用元数据？](../../../odbc/reference/develop-app/how-is-metadata-used.md)  
  
-   [SQLDescribeCol 和 SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)

