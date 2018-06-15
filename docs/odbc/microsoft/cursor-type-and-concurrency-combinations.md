---
title: 游标类型和并发组合 |Microsoft 文档
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
- ODBC driver for Oracle [ODBC], concurrency options
- cursors [ODBC], ODBC driver for Oracle
- concurrency options [ODBC]
- ODBC driver for Oracle [ODBC], cursor options
ms.assetid: db63d610-f86f-4029-9d66-fed616c8a818
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1c932f11bbf0098b9b599394751ef98d673a995b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32900392"
---
# <a name="cursor-type-and-concurrency-combinations"></a>游标类型和并发组合
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 游标类型控制光标向用户提供的功能。 并发选项控制的 updatability 和结果集的锁定行为。  
  
|游标类型|并发 （允许的值）|  
|-----------------|------------------------------------|  
|SQL_CURSOR_FORWARD_ONLY|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_STATIC|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_KEYSET_DRIVEN<sup>[1]</sup>|SQL_CONCUR_READ_ONLY SQL_CONCUR_LOCK<sup>[2]</sup> SQL_CONCUR_VALUES|  
  
 <sup>[1]</sup>请参阅[使用键集驱动游标的限制](../../odbc/microsoft/limitations-of-using-keyset-driven-cursors.md)。  
  
 <sup>[2]</sup> SQL_CONCUR_LOCK 支持仅在 SQL_AUTOCOMMIT 连接选项设置为 SQL_AUTOCOMMIT_OFF。  
  
## <a name="see-also"></a>另请参阅  
 [连接选项](../../odbc/microsoft/connect-options.md)
