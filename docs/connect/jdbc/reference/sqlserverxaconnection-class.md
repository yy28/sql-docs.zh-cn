---
title: SQLServerXAConnection 类 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5ecb4bf1-b8d1-47cf-9cb1-7a18acc11ce2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e095b498807412a40d4df1092b6c151c8c030c9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sqlserverxaconnection-class"></a>SQLServerXAConnection 类
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  表示可参与分布式 (XA) 事务的 JDBC 连接。  
  
 **包：** com.microsoft.sqlserver.jdbc  
  
 **扩展：** [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
 **实现：** javax.sql.XAConnection  
  
## <a name="syntax"></a>语法  
  
```  
  
public class SQLServerXAConnection  
```  
  
## <a name="remarks"></a>注释  
 可以在通过分布式事务中登记 SQLServerXAConnection 对象[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)对象。 事务管理器中，通常的中间层服务器上，一部分管理 SQLServerXAConnection 对象，通过 SQLServerXAResource 对象。  
  
> [!NOTE]  
>  应用程序编程人员一般不直接使用此接口。 它主要由在中间层服务器中工作的事务管理器使用。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerXAConnection 成员](../../../connect/jdbc/reference/sqlserverxaconnection-members.md)   
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
