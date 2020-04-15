---
title: 列数据 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ff89566efa65c88325d98422fe17788f27d2c8ca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306588"
---
# <a name="column-data"></a>列数据
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。  
  
 游标库在缓存中为每个使用**SQLBindCol**绑定到结果集的数据缓冲区创建一个缓冲区。 当它们模拟定位的更新或删除语句时，它使用这些缓冲区中的值来构造**WHERE**子句。 当从数据源获取数据并执行定位更新语句时，它会从行集缓冲区更新这些缓冲区。  
  
 当游标库从行集缓冲区更新其缓存时，它会根据**SQLBindCol**中指定的 C 数据类型传输数据。 例如，如果排集缓冲区的 C 数据类型SQL_C_SLONG，则游标库传输四个字节的数据;如果游标库传输四个字节的数据。如果它是SQL_C_CHAR缓冲区*长度*为 10，则游标库传输 10 字节的数据。 游标库不对传输的数据执行任何类型检查或转换。  
  
> [!NOTE]  
>  如果相应的行集*缓冲区中的*StrLen_or_IndPtrSQL_DATA_AT_EXEC或SQL_LEN_DATA_AT_EXEC宏的结果，则游标库不会更新列的缓存。  
  
 更新列时，数据源空白板固定长度字符数据和零垫固定长度二进制数据将根据需要进行。 例如，数据源将 CHAR （10） 列中的"Smith"存储为"Smith"。 游标库在执行定位的更新语句后将此数据复制到其缓存时，不会在行集缓冲区中出现空白板或零板数据。 因此，如果应用程序要求游标库缓存中的值为空白填充值或零填充值，则必须在执行定位的更新语句之前对行集缓冲区中的值进行空白填充或零填充。
