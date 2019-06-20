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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3e83cb131f37dd2901b77e70d19f5ed95ef596bb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63151293"
---
# <a name="cursor-type-and-concurrency-combinations"></a>游标类型和并发组合
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 游标类型控制光标向用户提供的功能。 并发选项控制可更新性和锁定行为的结果集。  
  
|游标类型|并发 （允许的值）|  
|-----------------|------------------------------------|  
|SQL_CURSOR_FORWARD_ONLY|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_STATIC|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_KEYSET_DRIVEN<sup>[1]</sup>|SQL_CONCUR_READ_ONLY SQL_CONCUR_LOCK<sup>[2]</sup> SQL_CONCUR_VALUES|  
  
 <sup>[1]</sup>请参阅[使用由键集驱动的游标的限制](../../odbc/microsoft/limitations-of-using-keyset-driven-cursors.md)。  
  
 <sup>[2]</sup> SQL_CONCUR_LOCK 仅 SQL_AUTOCOMMIT 连接选项设置为 SQL_AUTOCOMMIT_OFF 时支持。  
  
## <a name="see-also"></a>请参阅  
 [连接选项](../../odbc/microsoft/connect-options.md)
