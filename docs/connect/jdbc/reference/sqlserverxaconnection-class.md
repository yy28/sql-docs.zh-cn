---
title: SQLServerXAConnection 类 |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 177b10c9657c4cb8d6b37f7dec9d3b860308dcb7
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66788902"
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
  
## <a name="remarks"></a>Remarks  
 SQLServerXAConnection 对象可以通过 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 对象登记到分布式事务中。 事务管理器，通常是中间层服务器的一部分管理通过 SQLServerXAResource 对象的 SQLServerXAConnection 对象。  
  
> [!NOTE]  
>  应用程序编程人员一般不直接使用此接口。 它主要由在中间层服务器中工作的事务管理器使用。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerXAConnection 成员](../../../connect/jdbc/reference/sqlserverxaconnection-members.md)   
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
