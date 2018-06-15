---
title: 列数据的长度 |Microsoft 文档
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
- column data [ODBC]
- length of column data [ODBC]
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: c762c881-ebe0-4eac-84d5-f30281fc3eca
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8075358f3675b201a7b8b0528b08de305bf587da
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32905688"
---
# <a name="length-of-column-data"></a>列数据的长度
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 游标库创建在缓存中用于绑定到结果集与每个长度/指示器缓冲区的缓冲区**SQLBindCol**。 它使用的值在这些缓冲区中构造**其中**子句在模拟定位的更新或删除语句时。 它会从数据源和它执行的定位的 update 语句时获取数据时，它会更新这些从行集缓冲区的缓冲区。  
  
 如果数据缓冲区的 C 类型是 SQL_C_CHAR 或 SQL_C_BINARY，且长度/指示器值 sql_nts 以，数据的字符串长度会处于长度/指示器缓冲区。  
  
> [!NOTE]  
>  游标库不会更新其缓存的列，如果 **StrLen_or_IndPtr*在相应的行集缓冲区是 SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 宏的结果。
