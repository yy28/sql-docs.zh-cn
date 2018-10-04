---
title: 结果集元数据 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 6d134515-e34d-4563-96d7-8ad7714818fd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7dc88892fab2fd18dbcbec5ce54fa09c9c9b89e7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47819925"
---
# <a name="result-set-metadata"></a>结果集元数据
*元数据*是描述其他数据的数据。 例如，结果集元数据描述结果集，例如，在结果集中的列数、 这些列，其名称、 精度、 为 null 性和等等的数据类型。  
  
 可互操作应用程序应始终检查结果集列的元数据。 所返回的目录函数，结果集中的列的元数据可能不同于列的元数据。 例如，假设创建通过联接两个表的结果集时包含的可更新列。 虽然**SQLColumnPrivileges**可能指示用户可以更新列，结果集元数据可能不如果列是联接的"多"方上; 多个数据源可以更新的联接，但不是在的"一"方上列"多"方。 即使数据类型不能假定为相同的因为数据源创建结果集时可能会提升的数据类型。  
  
 本部分包含以下主题。  
  
-   [如何使用元数据？](../../../odbc/reference/develop-app/how-is-metadata-used.md)  
  
-   [SQLDescribeCol 和 SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)
