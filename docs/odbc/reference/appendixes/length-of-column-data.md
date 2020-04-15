---
title: 列数据的长度 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column data [ODBC]
- length of column data [ODBC]
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: c762c881-ebe0-4eac-84d5-f30281fc3eca
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d0b7ad515661cce4c5b1d407be768cc3da131bb4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304928"
---
# <a name="length-of-column-data"></a>列数据的长度
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。  
  
 光标库在缓存中为每个长度/指示器缓冲区创建一个缓冲区，该缓冲区绑定到使用**SQLBindCol**绑定到结果集。 当它们模拟定位的更新或删除语句时，它使用这些缓冲区中的值来构造**WHERE**子句。 当从数据源获取数据并执行定位更新语句时，它会从行集缓冲区更新这些缓冲区。  
  
 如果数据缓冲区的 C 类型SQL_C_CHAR或SQL_C_BINARY，并且长度/指示器值SQL_NTS，则数据的字符串长度将放入长度/指示器缓冲区中。  
  
> [!NOTE]  
>  如果相应的行集*缓冲区中的*StrLen_or_IndPtrSQL_DATA_AT_EXEC或SQL_LEN_DATA_AT_EXEC宏的结果，则游标库不会更新列的缓存。
