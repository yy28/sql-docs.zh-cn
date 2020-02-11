---
title: SQLGetDescField 和 SQLGetDescRec （游标库） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetDescField function [ODBC], Cursor Library
- SQLGetDescRec function [ODBC], Cursor Library
ms.assetid: 1a801f22-6fea-48aa-a723-3187a2ad852b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 853a364b61b63d58da93111c75db0d7d723ee49b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68073912"
---
# <a name="sqlgetdescfield-and-sqlgetdescrec-cursor-library"></a>SQLGetDescField 和 SQLGetDescRec（游标库）
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题讨论如何使用游标库中的**SQLGetDescField**和**SQLGetDescRec**函数。 有关这些函数的常规信息，请参阅[SQLGetDescField 函数](../../../odbc/reference/syntax/sqlgetdescfield-function.md)和[SQLGetDescRec 函数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)。  
  
 游标库执行**SQLGetDescRec**以返回书签列的元数据。 游标库执行**SQLGetDescField**以返回由**SQLGetDescRec**返回的相同字段，这些字段是 SQL_DESC_NAME、SQL_DESC_TYPE、SQL_DESC_DATETIME_INTERVAL_CODE、SQL_DESC_OCTET_LENGTH、SQL_DESC_PRECISION、SQL_DESC_SCALE 和 SQL_DESC_NULLABLE。 为了保持一致性， **SQLGetDescField**也返回 SQL_DESC_UNNAMED。  
  
 游标库在调用以返回为绑定书签列设置的以下字段的值时，将执行**SQLGetDescField** ： SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、SQL_DESC_OCTET_LENGTH_PTR 和 SQL_DESC_LENGTH。  
  
 当调用 SQLGetDescField、SQL_DESC_BIND_TYPE、SQL_DESC_ROW_ARRAY_SIZE 或 SQL_DESC_ROW_STATUS_PTR 字段的 SQL_DESC_BIND_OFFSET_PTR 值时，游标库会执行**** 。 对于任何行（而不仅仅是书签行），都可以返回这些字段。  
  
 如果应用程序调用**SQLGetDescField**来返回前面提到的任何字段的值，则游标库将调用该驱动程序。
