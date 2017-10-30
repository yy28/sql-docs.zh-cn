---
title: "SQLColAttributes （Visual FoxPro ODBC 驱动程序） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLColAttribute function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: d403dfa0-c26d-47d4-91d9-2f29aa387399
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2f4fae186ea7880325f6e3a96aae29f1edef07e1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlcolattributes-visual-foxpro-odbc-driver"></a>SQLColAttributes （Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序相关的信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持： 完整  
  
 ODBC API 一致性： 核心级别  
  
 返回结果集中的列的描述符信息。 描述符信息作为字符串、 32 位依赖于描述符的值或一个整数值返回。  
  
> [!NOTE]  
>  **SQLColAttributes**不能用于返回有关书签列 （列 0） 的信息。  
  
 Visual FoxPro ODBC 驱动程序支持所有*fDescType*值。 下表包含对所选值在驱动程序的实现的注释。  
  
|*fDescType*|注释|  
|-----------------|-------------|  
|SQL_COLUMN_AUTO_INCREMENT|返回 FALSE: Visual FoxPro 没有任何计数器字段。|  
|SQL_COLUMN_CASE_SENSITIVE|如果列类型是字符，始终返回 TRUE。|  
|SQL_COLUMN_LABEL|返回 SQL_COLUMN_NAME 也会返回的列名称。|  
|SQL_COLUMN_MONEY|如果列类型是货币 （由 Visual FoxPro 语言中的"Y"），则返回 TRUE。|  
|SQL_COLUMN_OWNER_NAME|始终返回空字符串。|  
|SQL_COLUMN_QUALIFIER_NAME|始终返回空字符串。|  
|SQL_COLUMN_SEARCHABLE|常规; 类型的列，则返回 SQL_UNSEARCHABLE这些列不能在 WHERE 子句中使用。<br /><br /> 类型字符或与 NOCPTRANS 的备注的列，则返回 SQL_SEARCHABLE 未设置;可以使用任何比较运算符的 WHERE 子句中使用这些列。<br /><br /> 对于所有其他列类型; 返回 SQL_ALL_EXCEPT_LIKE可以使用所有除类似的比较运算符的 WHERE 子句中使用这些列。|  
|SQL_COLUMN_TABLE_NAME|始终返回空字符串。|  
  
 有关详细信息，请参阅[SQLColAttributes](../../odbc/reference/syntax/sqlcolattributes-function.md)中*ODBC 程序员参考*。

