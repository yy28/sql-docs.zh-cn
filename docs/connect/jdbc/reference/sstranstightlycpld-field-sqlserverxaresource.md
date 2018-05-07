---
title: SSTRANSTIGHTLYCPLD 字段 (SQLServerXAResource) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SSTRANSTIGHTLYCPLD Field (SQLServerXAResource)
apilocation:
- SSTRANSTIGHTLYCPLD Field (SQLServerXAResource)
apitype: Assembly
ms.assetid: 379857c3-9de1-4964-8782-32df317cbfbb
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8323c328938188b16d56f9dfa05c3dfd2be16c75
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sstranstightlycpld-field-sqlserverxaresource"></a>SSTRANSTIGHTLYCPLD 字段 (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  用于允许使用紧密结合的 XA 事务，这些事务具有不同的 XA 分支事务 ID (XID)，但具有相同的全局事务 ID (GTRID)。  
  
## <a name="syntax"></a>语法  
  
```  
  
public static final int SSTRANSTIGHTLYCPLD  
```  
  
## <a name="field-value"></a>字段值  
 **Int** 32768 的值。  
  
## <a name="remarks"></a>注释  
 每个事务都由一个 XA 分支事务 ID (XID) 和全局事务 ID (GTRID) 标识。 若要允许应用程序使用具有不同 Xid 但相同 GTRID 紧密耦合的 XA 事务，必须设置[SSTRANSTIGHTLYCPLD](../../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md)对 XAResource.start 方法标志参数。 有关如何使用此标志的详细信息，请参阅[了解 XA 事务](../../../connect/jdbc/understanding-xa-transactions.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerXAResource 字段](../../../connect/jdbc/reference/sqlserverxaresource-fields.md)   
 [SQLServerXAResource 成员](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 类](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
