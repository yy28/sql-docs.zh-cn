---
title: SQLColAttributes （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307908"
---
# <a name="sqlcolattributes-visual-foxpro-odbc-driver"></a>SQLColAttributes（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含特定于 Visual FoxPro ODBC 驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 支持：完全  
  
 ODBC API 一致性：核心级别  
  
 返回结果集中列的描述符信息。 说明符信息以字符串、32位说明符相关值或整数值的形式返回。  
  
> [!NOTE]  
>  **SQLColAttributes**不能用于返回书签列（列0）的相关信息。  
  
 Visual FoxPro ODBC 驱动程序支持所有*fDescType*值。 下表包括对驱动程序的选定值实现的注释。  
  
|*fDescType*|注释|  
|-----------------|-------------|  
|SQL_COLUMN_AUTO_INCREMENT|返回 FALSE： Visual FoxPro 没有计数器字段。|  
|SQL_COLUMN_CASE_SENSITIVE|如果列类型为 "字符"，则始终返回 TRUE。|  
|SQL_COLUMN_LABEL|返回列名称，它也由 SQL_COLUMN_NAME 返回。|  
|SQL_COLUMN_MONEY|如果列类型为货币，则返回 TRUE （在 Visual FoxPro 语言中用 "Y" 表示）。|  
|SQL_COLUMN_OWNER_NAME|始终返回空字符串。|  
|SQL_COLUMN_QUALIFIER_NAME|始终返回空字符串。|  
|SQL_COLUMN_SEARCHABLE|返回类型为 General 的列 SQL_UNSEARCHABLE;不能在 WHERE 子句中使用这些列。<br /><br /> 返回 NOCPTRANS 不设置的字符或备注列的 SQL_SEARCHABLE;这些列可以在 WHERE 子句中与任何比较运算符一起使用。<br /><br /> 返回所有其他列类型的 SQL_ALL_EXCEPT_LIKE;这些列可用于包含所有比较运算符（如除外）的 WHERE 子句。|  
|SQL_COLUMN_TABLE_NAME|始终返回空字符串。|  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQLColAttributes](../../odbc/reference/syntax/sqlcolattributes-function.md) 。
