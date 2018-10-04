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
manager: craigg
ms.openlocfilehash: 66361572427c3264a1b25fe1c851685a07b2e029
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47765015"
---
# <a name="sqlgetdescfield-and-sqlgetdescrec-cursor-library"></a>SQLGetDescField 和 SQLGetDescRec（游标库）
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题介绍如何使用**SQLGetDescField**并**SQLGetDescRec**游标库中的函数。 有关这些函数的常规信息，请参阅[SQLGetDescField 函数](../../../odbc/reference/syntax/sqlgetdescfield-function.md)并[SQLGetDescRec 函数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)。  
  
 游标库执行**SQLGetDescRec**返回书签列的元数据。 游标库执行**SQLGetDescField**返回相同的字段返回**SQLGetDescRec**，哪些是 SQL_DESC_NAME、 SQL_DESC_TYPE、 SQL_DESC_DATETIME_INTERVAL_CODE、 SQL_DESC_OCTET_长度、 SQL_DESC_PRECISION、 SQL_DESC_SCALE 和 SQL_DESC_NULLABLE。 为了保持一致， **SQLGetDescField**也会返回 SQL_DESC_UNNAMED。  
  
 游标库执行**SQLGetDescField**调用返回的值的以下字段设置为绑定书签列： SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR，和SQL_DESC_LENGTH。  
  
 游标库执行**SQLGetDescField**时被调用以返回 SQL_DESC_BIND_OFFSET_PTR、 SQL_DESC_BIND_TYPE、 SQL_DESC_ROW_ARRAY_SIZE 或 SQL_DESC_ROW_STATUS_PTR 字段的值。 对于任何行，而不仅仅是书签行，可以返回这些字段。  
  
 如果应用程序调用**SQLGetDescField**返回以前提及的其他任何字段的值，游标库，将传递给驱动程序的调用。
