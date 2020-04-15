---
title: SQLColattributes（可视化狐狸Pro ODBC驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: d403dfa0-c26d-47d4-91d9-2f29aa387399
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9508fa7b9ada8273e1250d7584e577892acf5c51
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307908"
---
# <a name="sqlcolattributes-visual-foxpro-odbc-driver"></a>SQLColAttributes（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 特定于驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 支持： 完整  
  
 ODBC API 一致性：核心级别  
  
 返回结果集中列的描述符信息。 描述符信息将作为字符串、32 位描述符相关值或整数值返回。  
  
> [!NOTE]  
>  **SQLColAttributes**不能用于返回有关书签列（列 0）的信息。  
  
 可视化 FoxPro ODBC 驱动程序支持所有*fDescType*值。 下表包括有关驱动程序实现选定值的注释。  
  
|*fDescType*|注释|  
|-----------------|-------------|  
|SQL_COLUMN_AUTO_INCREMENT|返回 FALSE： 可视化 FoxPro 没有计数器字段。|  
|SQL_COLUMN_CASE_SENSITIVE|如果列类型为"字符"，则始终返回 TRUE。|  
|SQL_COLUMN_LABEL|返回列名称，该列名称也由SQL_COLUMN_NAME返回。|  
|SQL_COLUMN_MONEY|如果列类型为货币（由 Visual FoxPro 语言中的"Y"表示）则返回 TRUE。|  
|SQL_COLUMN_OWNER_NAME|始终返回空字符串。|  
|SQL_COLUMN_QUALIFIER_NAME|始终返回空字符串。|  
|SQL_COLUMN_SEARCHABLE|返回"常规"类型的列SQL_UNSEARCHABLE;这些列不能在 WHERE 子句中使用。<br /><br /> 返回未设置 NOCPTRANS 的类型"字符"或"备忘录"的列SQL_SEARCHABLE;这些列可以在 WHERE 子句中与任何比较运算符一起使用。<br /><br /> 返回所有其他列类型的SQL_ALL_EXCEPT_LIKE;这些列可以在 WHERE 子句中使用，除 LIKE 之外，所有比较运算符除外。|  
|SQL_COLUMN_TABLE_NAME|始终返回空字符串。|  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQLColattributes。](../../odbc/reference/syntax/sqlcolattributes-function.md)
