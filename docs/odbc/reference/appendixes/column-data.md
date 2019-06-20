---
title: 列数据 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column data [ODBC]
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: 0425818c-9469-493f-9e3c-fc03d9411c5c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 95f80c82d3804e31d5ea29d55af0fbedd4184e6c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63213841"
---
# <a name="column-data"></a>列数据
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 游标库创建在缓存中用于绑定到结果集与每个数据缓冲区的缓冲区**SQLBindCol**。 它使用这些缓冲区中的值构造**其中**子句时模拟定位更新或删除语句。 它从数据源和执行定位的 update 语句时提取数据时，它会更新这些行集缓冲区的缓冲区。  
  
 当游标库更新其缓存中的行集缓冲区时，根据指定的 C 数据类型将数据传输**SQLBindCol**。 例如，如果行集缓冲区的 C 数据类型，SQL_C_SLONG 游标库传输的数据; 四个字节如果它为 SQL_C_CHAR 和*BufferLength*为 10，游标库传输数据的 10 个字节。 游标库不传输的数据执行任何类型检查或转换。  
  
> [!NOTE]  
>  游标库不会更新其缓存的列，如果 **StrLen_or_IndPtr*中相应行集缓冲区是 SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 宏的结果。  
  
 当它更新列、 数据源为空面板固定长度的字符数据和零填充根据需要固定长度二进制数据。 例如，数据源将 char （10） 列"Smith"存储为"Smith"。 游标库执行操作时它此将数据复制到其缓存在执行定位的更新语句后不空白填充或用零填充行集缓冲区中的数据。 因此，如果应用程序需要游标库缓存中的值是空白填充或零填充，它必须空白填充或用零填充行集缓冲区中的值执行定位的更新语句之前。
