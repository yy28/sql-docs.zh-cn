---
title: SQLGetDescField 和 SQLGetDescRec （光标库） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLGetDescField function [ODBC], Cursor Library
- SQLGetDescRec function [ODBC], Cursor Library
ms.assetid: 1a801f22-6fea-48aa-a723-3187a2ad852b
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da57c5fb9f0ddb8d9e45651f9404d7825497d425
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetdescfield-and-sqlgetdescrec-cursor-library"></a>SQLGetDescField 和 SQLGetDescRec （光标库）
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题讨论使用**SQLGetDescField**和**SQLGetDescRec**光标库中的函数。 有关这些函数的常规信息，请参阅[SQLGetDescField 函数](../../../odbc/reference/syntax/sqlgetdescfield-function.md)和[SQLGetDescRec 函数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)。  
  
 游标库执行**SQLGetDescRec**返回书签列的元数据。 游标库执行**SQLGetDescField**返回返回的相同字段**SQLGetDescRec**，这是 SQL_DESC_NAME、 SQL_DESC_TYPE、 SQL_DESC_DATETIME_INTERVAL_CODE、 SQL_DESC_OCTET_长度、 SQL_DESC_PRECISION、 SQL_DESC_SCALE 和 SQL_DESC_NULLABLE。 为了保持一致性， **SQLGetDescField**也会返回 SQL_DESC_UNNAMED。  
  
 游标库执行**SQLGetDescField**时调用它可返回以下值的字段设置为绑定书签列： SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR、 SQL_DESC_OCTET_LENGTH_PTR，和SQL_DESC_LENGTH。  
  
 游标库执行**SQLGetDescField**时调用它可返回 SQL_DESC_BIND_OFFSET_PTR、 SQL_DESC_BIND_TYPE、 SQL_DESC_ROW_ARRAY_SIZE 或 SQL_DESC_ROW_STATUS_PTR 字段的值。 对于任何行，而不仅仅是书签行，可以返回这些字段。  
  
 如果应用程序调用**SQLGetDescField**若要返回的值之外，前面提到的任何字段，光标库，将传递到该驱动程序的调用。
