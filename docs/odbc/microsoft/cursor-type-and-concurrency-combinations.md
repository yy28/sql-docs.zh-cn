---
title: 光标类型和并发组合 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], concurrency options
- cursors [ODBC], ODBC driver for Oracle
- concurrency options [ODBC]
- ODBC driver for Oracle [ODBC], cursor options
ms.assetid: db63d610-f86f-4029-9d66-fed616c8a818
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b6397b5d675546bf41102f037b68c0022bec74df
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280767"
---
# <a name="cursor-type-and-concurrency-combinations"></a>游标类型和并发组合
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 而是使用 Oracle 提供的 ODBC 驱动程序。  
  
 游标类型控制提供给用户的游标的功能。 并发选项控制结果集的高数据性和锁定行为。  
  
|光标类型|并发（允许的值）|  
|-----------------|------------------------------------|  
|SQL_CURSOR_FORWARD_ONLY|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_STATIC|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_KEYSET_DRIVEN<sup>[1]</sup>|SQL_CONCUR_READ_ONLYSQL_CONCUR_LOCK<sup>[2]</sup> SQL_CONCUR_VALUES|  
  
 <sup>[1]</sup>请参阅[使用键集驱动光标的限制](../../odbc/microsoft/limitations-of-using-keyset-driven-cursors.md)。  
  
 <sup>[2]</sup>仅当SQL_AUTOCOMMIT连接选项设置为SQL_AUTOCOMMIT_OFF时，才支持SQL_CONCUR_LOCK。  
  
## <a name="see-also"></a>另请参阅  
 [连接选项](../../odbc/microsoft/connect-options.md)
