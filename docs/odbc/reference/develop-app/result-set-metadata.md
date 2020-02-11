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
ms.openlocfilehash: 1d8da8c15c861fff4767aa598e1b989d8f699c95
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020592"
---
# <a name="result-set-metadata"></a>结果集元数据
*元*数据是描述其他数据的数据。 例如，结果集元数据描述结果集，如结果集中的列数、这些列的数据类型、名称、精度、为 null 性等。  
  
 可互操作的应用程序应始终检查结果集列的元数据。 结果集中列的元数据可能不同于目录函数返回的列的元数据。 例如，假定可更新的列包含在通过联接两个表创建的结果集中。 尽管**SQLColumnPrivileges**可能指示用户可以更新列，但如果列位于联接的 "多" 方，则结果集元数据可能不会。许多数据源可以更新联接的 "一" 方上的列，但不能更新 "多" 端的列。 甚至不能假定数据类型是相同的，因为数据源在创建结果集时可能会升级数据类型。  
  
 本部分包含下列主题。  
  
-   [如何使用元数据？](../../../odbc/reference/develop-app/how-is-metadata-used.md)  
  
-   [SQLDescribeCol 和 SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)
