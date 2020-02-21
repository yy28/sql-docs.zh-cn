---
title: SQLServerXAConnection 类 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5ecb4bf1-b8d1-47cf-9cb1-7a18acc11ce2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 32d538e31ca3f4a0d9b23411ebcb7b282df46b33
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67970318"
---
# <a name="sqlserverxaconnection-class"></a>SQLServerXAConnection 类
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  表示可参与分布式 (XA) 事务的 JDBC 连接。  
  
 **包：** com.microsoft.sqlserver.jdbc  
  
 **扩展：**[SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
 **实现：** javax.sql.XAConnection  
  
## <a name="syntax"></a>语法  
  
```  
  
public class SQLServerXAConnection  
```  
  
## <a name="remarks"></a>备注  
 SQLServerXAConnection 对象可以通过 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 对象登记到分布式事务中。 事务管理器通常是中间层服务器的一部分，它通过 SQLServerXAResource 对象管理 SQLServerXAConnection 对象。  
  
> [!NOTE]  
>  应用程序编程人员一般不直接使用此接口。 它主要由在中间层服务器中工作的事务管理器使用。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerXAConnection 成员](../../../connect/jdbc/reference/sqlserverxaconnection-members.md)   
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
