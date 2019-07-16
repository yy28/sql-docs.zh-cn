---
title: 列数据的长度 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8d2998eace4772624a1e6590ab2541577147f5c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041608"
---
# <a name="length-of-column-data"></a>列数据的长度
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 游标库创建在缓存中用于绑定到结果集与每个长度/指示器缓冲区的缓冲区**SQLBindCol**。 它使用这些缓冲区中的值构造**其中**子句来模拟定位的更新或删除语句。 它从数据源和执行定位的 update 语句时提取数据时，它会更新这些行集缓冲区的缓冲区。  
  
 如果数据缓冲区的 C 类型为 SQL_C_CHAR 或 SQL_C_BINARY，且长度/指示器值为 SQL_NTS，字符串长度的数据会处于长度/指示器缓冲区。  
  
> [!NOTE]  
>  游标库不会更新其缓存的列，如果 **StrLen_or_IndPtr*中相应行集缓冲区是 SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 宏的结果。
