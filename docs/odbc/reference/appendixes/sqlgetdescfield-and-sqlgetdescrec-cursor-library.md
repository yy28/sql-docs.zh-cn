---
title: SQLGetDescField 和 SQLGetDescRec（光标库） |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 49ceea6b6180e1b51f2f103f74412c3e2b4cbe02
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307828"
---
# <a name="sqlgetdescfield-and-sqlgetdescrec-cursor-library"></a>SQLGetDescField 和 SQLGetDescRec（游标库）
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。  
  
 本主题讨论在游标库中使用**SQLGetDescField**和**SQLGetDescRec**函数。 有关这些函数的一般信息，请参阅[SQLGetDescField 函数](../../../odbc/reference/syntax/sqlgetdescfield-function.md)和[SQLGetDescRec 函数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)。  
  
 游标库执行**SQLGetDescRec**以返回书签列的元数据。 游标库执行**SQLGetDescField**返回**SQLGetDescRec**返回的相同字段，这些字段SQL_DESC_NAME、SQL_DESC_TYPE、SQL_DESC_DATETIME_INTERVAL_CODE、SQL_DESC_OCTET_LENGTH、SQL_DESC_PRECISION、SQL_DESC_SCALE和SQL_DESC_NULLABLE。 为保持一致性 **，SQLGetDescField**还会返回SQL_DESC_UNNAMED。  
  
 游标库在调用**SQLGetDescField 时执行 SQLGetDescField**以返回为绑定书签列设置的以下字段的值：SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、SQL_DESC_OCTET_LENGTH_PTR和SQL_DESC_LENGTH。  
  
 在调用游标库以返回SQL_DESC_BIND_OFFSET_PTR、SQL_DESC_BIND_TYPE、SQL_DESC_ROW_ARRAY_SIZE或SQL_DESC_ROW_STATUS_PTR字段的值时，游标库将执行**SQLGetDescField。** 可以为任何行返回这些字段，而不仅仅是书签行。  
  
 如果应用程序调用**SQLGetDescField**返回上述字段以外的任何字段的值，则游标库将调用传递给驱动程序。
