---
title: 游标类型和并发组合 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280767"
---
# <a name="cursor-type-and-concurrency-combinations"></a>游标类型和并发组合
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 游标类型控制向用户提供的游标的功能。 并发选项控制结果集的更新和锁定行为。  
  
|游标类型|并发（允许值）|  
|-----------------|------------------------------------|  
|SQL_CURSOR_FORWARD_ONLY|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_STATIC|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_KEYSET_DRIVEN<sup>[1]</sup>|SQL_CONCUR_READ_ONLY SQL_CONCUR_LOCK<sup>[2]</sup> SQL_CONCUR_VALUES|  
  
 <sup>[1]</sup>请参阅[使用由键集驱动的游标的限制](../../odbc/microsoft/limitations-of-using-keyset-driven-cursors.md)。  
  
 仅当 SQL_AUTOCOMMIT 连接选项设置为 SQL_AUTOCOMMIT_OFF 时，才支持<sup>[2]</sup> SQL_CONCUR_LOCK。  
  
## <a name="see-also"></a>另请参阅  
 [连接选项](../../odbc/microsoft/connect-options.md)
